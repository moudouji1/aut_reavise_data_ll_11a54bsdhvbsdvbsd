Voici un résumé de la séance sur le routage et les contrôleurs dans Laravel, conçu pour la révision d'un étudiant.

## Résumé de la Séance 2 : Routage, Contrôleurs et Vues

Cette séance couvre les concepts fondamentaux de la gestion des requêtes HTTP dans une application Laravel. Nous apprenons comment intercepter une URL et la diriger vers la logique appropriée. Elle aborde la création des **routes** pour définir les "chemins" de l'application, l'utilisation des **contrôleurs** pour organiser le code métier, et la génération de réponses HTML dynamiques avec les **vues** et le moteur de template **Blade**.

---

## 1. Le Routage dans Laravel

Le routage est le mécanisme qui associe une **URI** (l'adresse dans le navigateur) à une **action** à exécuter (une fonction ou une méthode de contrôleur).

### Principe et Fichiers de Routes

-   Les routes web sont définies dans le fichier `routes/web.php`.
-   Le routage permet de "trier" les requêtes HTTP entrantes.
-   Grâce au fichier `.htaccess` (pour Apache), Laravel utilise des URLs propres (ex: `monsite.fr/mapage` au lieu de `monsite.fr/index.php/mapage`).

### Définir des Routes de Base

-   On utilise la façade `Route` pour déclarer les routes en fonction de la **méthode HTTP**.
-   **`GET`** : Pour demander une ressource (afficher une page).
    ```php
    use Illuminate\Support\Facades\Route;

    Route::get('/', function () {
        return 'Bienvenue sur le site !';
    });
    ```
-   **`POST`** : Pour envoyer des données afin de créer une ressource (soumettre un formulaire).
-   **`PUT`** : Pour mettre à jour une ressource existante.
-   **`DELETE`** : Pour supprimer une ressource.
-   **Autres méthodes** :
    -   `Route::match(['get', 'post'], ...)` : Répond à plusieurs méthodes HTTP.
    -   `Route::any(...)` : Répond à toutes les méthodes HTTP.

### Paramètres des Routes

On peut capturer des segments variables de l'URI.

-   **Paramètres obligatoires** : Définis entre accolades `{}`.
    ```php
    Route::get('article/{n}', function ($n) {
        return 'Affichage de l\'article numéro ' . $n;
    });
    ```
-   **Paramètres optionnels** : On ajoute un `?` et on donne une valeur par défaut à la variable dans la fonction.
    ```php
    Route::get('page/{n?}', function ($n = null) {
        if ($n) {
            return 'Je suis la page ' . $n;
        }
        return 'Je suis une page sans numéro !';
    });
    ```
-   **Contraintes sur les paramètres** : On utilise la méthode `where()` avec une **expression régulière** pour valider le format d'un paramètre.
    ```php
    Route::get('article/{n}', function ($n) {
        // ...
    })->where('n', '[0-9]+'); // N'accepte que les chiffres
    ```

### Routes Nommées

Nommer une route facilite la génération d'URLs ou de redirections.

-   **Déclaration** : On enchaîne la méthode `name()`.
    ```php
    Route::get('/accueil', [HomeController::class, 'index'])->name('home');
    ```
-   **Utilisation** : On utilise la fonction `route()` pour générer l'URL.
    ```php
    $url = route('home'); // Génère l'URL complète vers '/accueil'
    ```

### Commandes Artisan pour les Routes

-   **Lister toutes les routes** : `php artisan route:list`.
-   **Mettre en cache les routes** (en production pour de meilleures performances) : `php artisan route:cache`.
-   **Effacer le cache des routes** : `php artisan route:clear`.

---

## 2. Les Contrôleurs

Un contrôleur est une classe dont les méthodes répondent aux requêtes HTTP. Il permet de regrouper la logique métier et de garder le fichier de routes propre.

### Rôle et Utilité

-   **Séparation des responsabilités** : Le fichier de routes se contente de rediriger les requêtes, le contrôleur contient la logique de traitement.
-   **Organisation du code** : Rend l'application plus lisible et maintenable.

### Création et Utilisation

-   **Créer un contrôleur** avec Artisan :
    ```bash
    php artisan make:controller ArticleController
    ```
-   Les contrôleurs sont créés dans le dossier `app/Http/Controllers`.
-   **Exemple de méthode** dans un contrôleur :
    ```php
    namespace App\Http\Controllers;

    class ArticleController extends Controller
    {
        public function show($id)
        {
            // La méthode reçoit le paramètre de la route
            return view('article', ['numero' => $id]);
        }
    }
    ```

### Lier une Route à un Contrôleur

-   Au lieu d'une fonction anonyme, on passe un tableau avec le nom de la classe du contrôleur et le nom de la méthode.
    ```php
    use App\Http\Controllers\ArticleController;

    Route::get('article/{id}', [ArticleController::class, 'show'])->where('id', '[0-9]+');
    ```

---

## 3. Les Réponses et les Vues

Une fois la requête traitée, le contrôleur doit renvoyer une réponse au navigateur.

### Types de Réponses

-   **Chaîne de caractères** ou **tableau** (automatiquement converti en JSON).
    ```php
    Route::get('/api/users', function () {
        return ['user1', 'user2', 'user3']; // Réponse JSON
    });
    ```
-   **Objet `Response`** : Permet de personnaliser le code de statut HTTP et les en-têtes.
    ```php
    return response('Contenu de la réponse', 200)
                  ->header('Content-Type', 'text/plain');
    ```
-   **Redirections** :
    -   `redirect('nouvelle-url')` : Redirection simple.
    -   `redirect()->route('nom.de.la.route')` : Redirection vers une route nommée.
    -   `redirect()->back()` : Redirection vers la page précédente.

### Les Vues

Les vues contiennent le code HTML de l'application. Elles sont situées dans `resources/views`.

-   **Retourner une vue** : On utilise la fonction `view()`.
    ```php
    // Dans un contrôleur
    public function index()
    {
        return view('welcome'); // Affiche le fichier resources/views/welcome.blade.php
    }
    ```
-   **Passer des données à une vue** : On passe un tableau associatif en second argument de la fonction `view()`.
    ```php
    return view('article', ['numero' => 42, 'titre' => 'Mon Super Article']);
    ```

---

## 4. Le Moteur de Template Blade

Blade est le moteur de template de Laravel. Il permet d'utiliser du PHP dans les vues avec une syntaxe plus simple et d'organiser le code de présentation. Les fichiers de vue Blade ont l'extension `.blade.php`.

### Affichage des Données

-   **Affichage échappé** (sécurisé contre les attaques XSS) : `{{ $variable }}`.
-   **Affichage non échappé** (à utiliser avec prudence) : `{!! $variable !!}`.
    ```blade
    <h1>Article : {{ $titre }}</h1>
    ```

### Structures de Contrôle (Directives)

-   **Conditions** : `@if`, `@elseif`, `@else`, `@endif`.
    ```blade
    @if ($isActive)
        <p>L'utilisateur est actif.</p>
    @else
        <p>L'utilisateur est inactif.</p>
    @endif
    ```
-   **Boucles** : `@for`, `@foreach`, `@while`, `@forelse` (un `@foreach` avec une condition si le tableau est vide).
    ```blade
    <ul>
        @foreach ($articles as $article)
            <li>{{ $article->titre }}</li>
        @endforeach
    </ul>
    ```
-   Dans une boucle, la variable `$loop` donne des informations utiles (`$loop->first`, `$loop->last`, `$loop->index`, etc.).

### Organisation des Vues avec Blade (Héritage)

-   **Layout (gabarit)** : C'est une vue "maître" qui définit la structure commune à plusieurs pages. On y place des "emplacements" avec `@yield('nom_section')`.
    ```blade
    <!-- resources/views/layouts/app.blade.php -->
    <html>
        <head><title>@yield('title')</title></head>
        <body>
            <div class="container">
                @yield('content')
            </div>
        </body>
    </html>
    ```
-   **Vue enfant** : Une vue qui "hérite" du layout avec `@extends('nom.du.layout')` et remplit les sections avec `@section('nom_section') ... @endsection`.
    ```blade
    <!-- resources/views/articles/show.blade.php -->
    @extends('layouts.app')

    @section('title', 'Titre de mon article')

    @section('content')
        <h1>Contenu de l'article</h1>
        <p>...</p>
    @endsection
    ```