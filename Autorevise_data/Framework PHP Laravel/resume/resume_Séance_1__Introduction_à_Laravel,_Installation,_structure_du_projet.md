Cette séance d'introduction à Laravel couvre les concepts fondamentaux des frameworks, en particulier l'architecture MVC, ainsi que les étapes pratiques pour démarrer : l'installation des prérequis comme Composer, la création d'un nouveau projet, la découverte de sa structure de dossiers, et l'utilisation de l'outil en ligne de commande Artisan. Elle aborde également les briques essentielles d'une application Laravel (routes, contrôleurs, vues, modèles) et les bases de la configuration et du déploiement.

## Séance 1 : Introduction à Laravel

### 1. Concepts Fondamentaux

#### Qu'est-ce qu'un Framework PHP ?
- Un **framework** est une base logicielle qui fournit une **structure** et des **bibliothèques** pour développer des applications plus rapidement.
- **Avantages** : gain de temps, code mieux organisé, réutilisable, plus sécurisé et respectant les bonnes pratiques.
- **Prérequis** : Maîtrise de **PHP**, de la **POO**, des bases de données (**SQL**) et de l'architecture **MVC**.

#### Pourquoi choisir Laravel ?
- Laravel, créé par Taylor Otwell, est un framework **moderne**, **élégant** et **puissant**.
- Il est basé sur des composants fiables (ex: ceux de **Symfony**).
- **Fonctionnalités clés** :
    - Un système de **routage** simple et rapide.
    - Un ORM (Object-Relational Mapper) performant : **Eloquent**.
    - Un moteur de template efficace : **Blade**.
    - Des systèmes intégrés pour l'**authentification**, la **validation**, la gestion du **cache**, l'envoi d'**emails**, etc.
    - Une grande **communauté** et une **documentation** complète (Laracasts, Laravel News).

#### L'Architecture MVC (Modèle-Vue-Contrôleur)
- C'est un **patron d'architecture** qui sépare une application en trois couches logiques :
    - **Modèle (Model)** : Gère les **données** et les interactions avec la base de données. Dans Laravel, une classe de modèle correspond souvent à une table SQL.
    - **Vue (View)** : Gère l'**affichage** et l'interface utilisateur (HTML). Dans Laravel, on utilise le moteur de template **Blade** (`.blade.php`).
    - **Contrôleur (Controller)** : Fait l'**intermédiaire** entre le Modèle et la Vue. Il reçoit les requêtes, demande les données au Modèle et les transmet à la Vue.

### 2. Installation et Création d'un Projet

#### Prérequis de l'environnement
- **PHP** : Version >= 7.3 (selon la version de Laravel).
- **Extensions PHP** : `PDO`, `Mbstring`, `OpenSSL`, `Tokenizer`, `XML`, `JSON`, `Ctype`, `BCMath`, `Fileinfo`.
- **Composer** : Un **gestionnaire de dépendances** pour PHP. Il est indispensable pour installer Laravel et ses paquets.

#### Création d'un projet Laravel
- Il existe deux méthodes principales via le terminal :
    1.  **Avec Composer** :
        ```bash
        composer create-project laravel/laravel nom-du-projet
        ```
    2.  **Avec l'installateur Laravel** (à installer une seule fois) :
        ```bash
        composer global require laravel/installer
        laravel new nom-du-projet
        ```

#### Lancer l'application
- Une fois dans le dossier du projet, utilisez la commande **Artisan** pour démarrer le serveur de développement local :
    ```bash
    cd nom-du-projet
    php artisan serve
    ```
- L'application est alors accessible par défaut à l'adresse `http://localhost:8000`.

### 3. Structure d'un Projet Laravel

- **`app/`** : Le cœur de votre application.
    - **`Http/Controllers/`** : Contient les **contrôleurs**.
    - **`Models/`** : Contient les **modèles Eloquent**.
    - `Http/Middleware/` : Contient les middlewares (filtres de requêtes).
    - `Http/Requests/` : Contient les classes de validation de formulaires.
- **`config/`** : Contient tous les fichiers de **configuration** de l'application (base de données, mail, cache...).
- **`database/`** : Contient les **migrations** (structure des tables), les *seeders* (données de test) et les *factories*.
- **`public/`** : Le **point d'entrée** de l'application (`index.php`). C'est le seul dossier accessible publiquement. Contient les fichiers compilés (CSS, JS) et les fichiers statiques (images).
- **`resources/`** : Contient les fichiers sources non compilés.
    - **`views/`** : Contient les **vues Blade**.
    - `css/`, `js/` : Contiennent les sources CSS et JavaScript avant compilation.
- **`routes/`** : Contient la définition de toutes les **routes** (URL) de l'application. Le fichier `web.php` est utilisé pour les routes web.
- **`storage/`** : Contient les fichiers générés par le framework (logs, cache, fichiers uploadés par les utilisateurs). Doit avoir les droits d'écriture.
- **`tests/`** : Contient les tests automatisés (unitaires, fonctionnels).
- **`vendor/`** : Contient les **dépendances Composer**, y compris le code source de Laravel lui-même.
- **`.env`** : Fichier de **configuration de l'environnement**. Contient les variables sensibles (clés d'API, accès à la BDD). Ce fichier **ne doit jamais être versionné** (il est dans `.gitignore`).

### 4. Outils et Composants Clés

#### Artisan : L'Interface en Ligne de Commande
- **Artisan** est un outil puissant pour automatiser les tâches courantes.
- Quelques commandes essentielles :
    - `php artisan list` : Lister toutes les commandes disponibles.
    - `php artisan serve` : Démarrer le serveur de développement.
    - `php artisan route:list` : Afficher toutes les routes de l'application.
    - `php artisan make:controller NomController` : Créer un nouveau contrôleur.
    - `php artisan make:model NomModele -m` : Créer un modèle et sa migration associée.
    - `php artisan migrate` : Exécuter les migrations pour créer les tables en base de données.
    - `php artisan cache:clear` : Vider le cache de l'application.

#### Configuration et Sessions
- La configuration est gérée via les fichiers du dossier `config/` et le fichier `.env`.
- On accède aux valeurs de configuration avec l'aide `config('fichier.cle')`.
- Les **sessions** permettent de stocker des informations spécifiques à un utilisateur entre plusieurs requêtes.
- On manipule la session avec la façade `Session` ou l'aide `session()` :
    - `session(['cle' => 'valeur'])` pour stocker une donnée.
    - `session('cle')` pour récupérer une donnée.
    - `session()->has('cle')` pour vérifier si une donnée existe.

### 5. Déploiement
- Le déploiement consiste à mettre l'application en **production**.
- Il est crucial de gérer les **environnements** : un fichier `.env` pour le développement (`APP_DEBUG=true`) et un autre pour la production (`APP_DEBUG=false`).
- Le dossier `storage` doit avoir les **droits d'écriture** sur le serveur.
- La racine du serveur web (ex: Apache, Nginx) doit pointer vers le dossier `public/` du projet Laravel pour des raisons de **sécurité**.