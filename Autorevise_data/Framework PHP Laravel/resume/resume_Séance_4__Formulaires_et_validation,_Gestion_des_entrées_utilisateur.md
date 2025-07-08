# Séance 4 : Formulaires, Validation et Gestion des Entrées Utilisateur

Cette séance aborde la gestion des formulaires dans un projet web, en se concentrant sur le framework Laravel. Elle couvre la création des routes, la construction des formulaires, la récupération des données utilisateur, la protection contre les failles de sécurité (CSRF) et la validation des informations soumises. Des rappels sur la gestion des formulaires en PHP natif sont également inclus.

## Les Entrées Utilisateur avec Laravel

### Scénario et Routage
- Un formulaire nécessite généralement deux routes pour une même URL :
    - Une route avec la méthode **`GET`** pour afficher le formulaire à l'utilisateur.
    - Une route avec la méthode **`POST`** pour traiter les données soumises par l'utilisateur.
- **Exemple de routes** dans `routes/web.php` :
    ```php
    // Affiche le formulaire
    Route::get('users', 'UsersController@getInfos');
    // Traite les données du formulaire
    Route::post('users', 'UsersController@postInfos');
    ```
- Laravel supporte d'autres verbes HTTP comme **`PUT`**, **`PATCH`**, et **`DELETE`** pour les applications de type API REST.

### Le Middleware
- Un **middleware** est un code qui s'exécute à l'arrivée d'une requête pour effectuer des traitements spécifiques (sécurité, sessions, cookies).
- Par défaut, les routes du groupe `web` bénéficient automatiquement des middlewares pour :
    - La gestion des **sessions**.
    - La gestion des **cookies**.
    - La protection contre les attaques **CSRF**.

### Création du Formulaire
- L'utilisation du package **`Laravelcollective/Html`** est encouragée pour simplifier la création de formulaires.
- **Ouverture du formulaire** : ` {!! Form::open(['url' => 'users']) !!} `
    - La méthode par défaut est **`POST`**.
- **Création des champs** :
    - Étiquette (label) : ` {!! Form::label('nom', 'Entrez votre nom :') !!} `
    - Champ de texte : ` {!! Form::text('nom') !!} `
    - Bouton de soumission : ` {!! Form::submit('Envoyer !') !!} `
- **Fermeture du formulaire** : ` {!! Form::close() !!} `
- L'utilisation de ce package génère automatiquement un **champ `hidden`** contenant le **jeton CSRF**, essentiel pour la sécurité.
- **Alternative manuelle** :
    ```html
    <form method="POST" action="{!! url('users') !!}">
        @csrf
        <!-- ou {!! csrf_field() !!} -->
        ...
    </form>
    ```

### Le Contrôleur et la Récupération des Données
- Le contrôleur gère la logique du formulaire avec deux méthodes distinctes (une pour `GET`, une pour `POST`).
- Pour récupérer les données soumises, on utilise l'objet **`Request`** injecté dans la méthode du contrôleur.
- **Exemple de récupération** d'une entrée :
    ```php
    public function postInfos(Request $request)
    {
        // Récupère la valeur du champ 'nom'
        $nom = $request->input('nom');
        return 'Le nom est ' . $nom;
    }
    ```

## La Protection CSRF (Cross-Site Request Forgery)

- **Définition** : Attaque qui consiste à faire exécuter une requête par un utilisateur authentifié à son insu.
- **Protection dans Laravel** : Laravel génère un **jeton (token) de sécurité unique** pour chaque session utilisateur.
- Ce jeton est inclus automatiquement dans les formulaires créés avec `Form::open()` ou manuellement avec la directive Blade **`@csrf`**.
- À la soumission, le middleware `VerifyCsrfToken` compare le jeton envoyé avec celui stocké en session. S'ils ne correspondent pas, la requête est rejetée avec une erreur.

## La Validation des Données

### Principe Fondamental
- **Ne jamais faire confiance aux données qui arrivent sur le serveur**.
- La **validation côté serveur** est indispensable, même si une validation côté client (en JavaScript) est déjà en place.

### Mise en Œuvre dans Laravel
- La validation se fait généralement dans la méthode du contrôleur qui traite la soumission du formulaire, via la méthode **`validate()`**.
- **Exemple de validation** :
    ```php
    public function store(Request $request)
    {
        $validated = $request->validate([
            'title' => 'required|max:255',
            'body' => 'required',
            'email' => 'required|email|unique:users'
        ]);
        // Le code ici ne s'exécute que si la validation réussit.
    }
    ```
- **Règles de validation** : Elles sont définies dans un tableau associatif. Plusieurs règles pour un même champ sont séparées par le caractère `|`.
- **En cas d'échec** de la validation, Laravel :
    1.  Redirige automatiquement l'utilisateur vers la page du formulaire.
    2.  Transmet les **messages d'erreur** à la vue dans une variable **`$errors`**.
    3.  Repopule les champs du formulaire avec les anciennes données (**old input**).

### Affichage des Erreurs dans la Vue
- La variable **`$errors`** est un objet disponible dans toutes les vues.
- **Vérifier la présence d'une erreur** pour un champ : `$errors->has('nom')`
- **Afficher le premier message d'erreur** pour un champ : `$errors->first('nom', '<small class="error">:message</small>')`

### Localisation des Messages
- Par défaut, les messages d'erreur sont en anglais.
- Pour les traduire, il faut placer les fichiers de langue (par exemple, le dossier `fr`) dans le répertoire `resources/lang` et modifier la locale dans `config/app.php` : `'locale' => 'fr'`.

## Fonctionnalités Avancées des Formulaires

### Méthodes HTTP (PUT, PATCH, DELETE)
- Les formulaires HTML ne supportent nativement que les méthodes `GET` et `POST`.
- Pour simuler d'autres verbes HTTP, on utilise la directive Blade **`@method('VERBE_HTTP')`**.
- **Exemple pour une suppression** :
    ```html
    <form action="/resource/1" method="POST">
        @csrf
        @method('DELETE')
        <button type="submit">Supprimer</button>
    </form>
    ```

### Upload de Fichiers
- Le formulaire doit avoir l'attribut **`enctype="multipart/form-data"`**.
- La validation se fait avec des règles spécifiques :
    - **`file`** : le champ doit être un fichier.
    - **`image`** : le fichier doit être une image (jpeg, png, bmp, gif, svg, or webp).
    - **`mimetypes:video/avi,...`** : restreint le type de fichier.
    - **`dimensions:max_width=320,...`** : valide les dimensions d'une image.

## Rappels sur la Gestion en PHP Natif

### Méthodes GET et POST
- **`GET`** : Les données sont transmises dans l'URL (visibles, limitées en taille). Utile pour des liens ou des recherches.
- **`POST`** : Les données sont transmises dans le corps de la requête HTTP (invisibles, adaptées aux données sensibles ou volumineuses).

### Récupération des Données
- PHP utilise des variables **superglobales** pour accéder aux données des formulaires :
    - **`$_GET`** : Tableau associatif contenant les données envoyées via la méthode `GET`.
    - **`$_POST`** : Tableau associatif contenant les données envoyées via la méthode `POST`.
    - **`$_REQUEST`** : Contient les données de `$_GET`, `$_POST` et `$_COOKIE`.
    - **`$_FILES`** : Contient les informations sur les fichiers uploadés.
- Il est crucial de vérifier l'existence des données avec **`isset()`** ou **`empty()`** avant de les utiliser.

### Sessions et Cookies
- **Sessions (`$_SESSION`)** : Mécanisme pour stocker des informations sur le serveur et les conserver à travers plusieurs pages pour un même utilisateur. On démarre une session avec `session_start()`.
- **Cookies (`$_COOKIE`)** : Petit fichier texte stocké sur l'ordinateur du client pour retenir des informations (pseudo, préférences...). On crée un cookie avec `setcookie()`.