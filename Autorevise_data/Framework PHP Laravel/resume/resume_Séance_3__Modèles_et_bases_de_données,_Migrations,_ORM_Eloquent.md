## Résumé de la Séance 3 : Modèles et bases de données, Migrations, ORM Eloquent

Cette séance explore la gestion des bases de données avec Laravel. Elle couvre les **migrations** pour construire et versionner le schéma de la base, l'**ORM Eloquent** pour interagir avec les données de manière intuitive via des **modèles**, et le **Query Builder** pour des requêtes plus complexes. Les concepts de **relations** (1-N, N-N), de **seeding** pour peupler la base, et des bonnes pratiques comme l'**injection de dépendances** sont également abordés.

---

## 1. Migrations : Gérer le Schéma de la Base de Données

Les migrations permettent de créer, modifier et versionner la structure de votre base de données directement depuis votre code.

### ### Principes des Migrations
- Chaque migration est un fichier PHP décrivant des modifications de schéma.
- Permet de garder la structure de la base de données synchronisée entre les développeurs.
- Les fichiers de migration se trouvent dans `database/migrations`.

### ### Commandes Artisan pour les Migrations
- **Créer une migration** : `php artisan make:migration nom_de_la_migration`
- **Exécuter les migrations** : `php artisan migrate`
- **Annuler la dernière migration** : `php artisan migrate:rollback`
- **Annuler toutes les migrations** : `php artisan migrate:reset`
- **Annuler et relancer toutes les migrations** : `php artisan migrate:refresh`
- **Supprimer toutes les tables et relancer les migrations** : `php artisan migrate:fresh`

### ### Structure d'un fichier de Migration
Chaque migration contient deux méthodes principales :
- `up()` : Contient le code pour **créer ou modifier** des tables et des colonnes.
- `down()` : Contient le code pour **annuler** les opérations de la méthode `up()`.

*Exemple de création de table :*
```php
public function up()
{
    Schema::create('articles', function (Blueprint $table) {
        $table->id(); // ID auto-incrémenté (équivalent à increments('id'))
        $table->string('title', 255);
        $table->text('contenu');
        $table->foreignId('user_id')->constrained()->onDelete('cascade');
        $table->timestamps(); // Crée les colonnes created_at et updated_at
    });
}

public function down()
{
    Schema::dropIfExists('articles');
}
```

---

## 2. Modèles Eloquent : Le Mappage Objet-Relationnel (ORM)

Eloquent est l'ORM de Laravel. Il permet de représenter chaque table de la base de données par une classe (un "Modèle") pour manipuler les données de manière orientée objet.

### ### Création et Configuration d'un Modèle
- **Créer un modèle** : `php artisan make:model NomDuModele`
- **Créer un modèle et sa migration associée** : `php artisan make:model NomDuModele -m`
- Les modèles se trouvent dans le dossier `app/Models`.
- Un modèle étend la classe `Illuminate\Database\Eloquent\Model`.

*Configuration de base d'un modèle :*
```php
class Article extends Model
{
    // Nom de la table (optionnel si le nom du modèle est le singulier du nom de la table)
    protected $table = 'articles';

    // Désactive les colonnes created_at et updated_at si elles n'existent pas
    public $timestamps = false;

    // Définit les colonnes autorisées pour l'assignement de masse (mass assignment)
    protected $fillable = [
        'title',
        'description',
        'contenu',
        'user_id',
    ];
}
```

---

## 3. Opérations CRUD avec Eloquent

CRUD signifie **Create, Read, Update, Delete**. Eloquent simplifie ces opérations.

### ### Créer (Create)
- **Instanciation puis sauvegarde** :
  ```php
  $article = new Article;
  $article->title = 'Nouveau titre';
  $article->contenu = '...';
  $article->save();
  ```
- **Assignement de masse (Mass Assignment)** avec la méthode `create()` (requiert la propriété `$fillable` dans le modèle) :
  ```php
  Article::create([
      'title' => 'Titre avec create',
      'contenu' => '...'
  ]);
  ```

### ### Lire (Read / Retrieve)
- **Récupérer tous les enregistrements** : `$articles = Article::all();`
- **Trouver un enregistrement par son ID** : `$article = Article::find(1);`
- **Trouver ou échouer** (retourne une erreur 404 si non trouvé) : `$article = Article::findOrFail(1);`
- **Construire une requête** :
  - `$articles = Article::where('status', 'published')->get();`
  - `$article = Article::where('status', 'published')->first();`

### ### Mettre à jour (Update)
- **Récupérer, modifier, puis sauvegarder** :
  ```php
  $article = Article::find(1);
  $article->title = 'Titre mis à jour';
  $article->save();
  ```
- **Mise à jour de masse** :
  ```php
  Article::where('status', 'archived')->update(['status' => 'published']);
  ```

### ### Supprimer (Delete)
- **Supprimer un modèle récupéré** :
  ```php
  $article = Article::find(1);
  $article->delete();
  ```
- **Supprimer par ID** : `Article::destroy(1);`
- **Supprimer plusieurs modèles par ID** : `Article::destroy([1, 2, 3]);`

---

## 4. Le Query Builder

Le Query Builder offre une interface fluide pour construire des requêtes SQL, alternative à Eloquent, souvent utilisée pour des opérations complexes.

- **Principe** : Utilise la façade `DB`.
- **Sélectionner des données** :
  ```php
  $users = DB::table('users')->where('votes', '>', 100)->get();
  ```
- **Jointures** :
  ```php
  $users = DB::table('users')
      ->join('contacts', 'users.id', '=', 'contacts.user_id')
      ->select('users.name', 'contacts.phone')
      ->get();
  ```
- **Agrégats** : `count()`, `max()`, `min()`, `avg()`, `sum()`.
  ```php
  $count = DB::table('users')->count();
  ```

---

## 5. Relations entre les Modèles

Eloquent permet de définir et de manipuler facilement les relations entre les tables.

### ### Relation 1-N (One-to-Many)
*Un `User` a plusieurs `Article`, un `Article` appartient à un seul `User`.*

- Dans le modèle `User` (le "un") :
  ```php
  public function articles()
  {
      return $this->hasMany(Article::class);
  }
  ```
- Dans le modèle `Article` (le "plusieurs") :
  ```php
  public function user()
  {
      return $this->belongsTo(User::class);
  }
  ```

### ### Relation N-N (Many-to-Many)
*Un `Article` a plusieurs `Tag`, un `Tag` a plusieurs `Article`.* Nécessite une table pivot (ex: `article_tag`).

- Dans les deux modèles (`Article` et `Tag`) :
  ```php
  public function tags()
  {
      return $this->belongsToMany(Tag::class);
  }

  public function articles()
  {
      return $this->belongsToMany(Article::class);
  }
  ```
- **Attacher/Détacher des relations** :
  - `$article->tags()->attach($tagId);`
  - `$article->tags()->detach($tagId);`
  - `$article->tags()->sync([1, 2, 3]);`

### ### Accéder aux données liées
- Une fois les relations définies, on y accède comme des propriétés :
  ```php
  // Récupérer tous les articles d'un utilisateur
  $user = User::find(1);
  $articles = $user->articles;

  // Récupérer l'utilisateur d'un article
  $article = Article::find(1);
  $user = $article->user;
  ```

---

## 6. Seeding : Remplir la Base de Données

Le seeding permet de peupler la base de données avec des données de test.

- **Créer un seeder** : `php artisan make:seeder UsersTableSeeder`
- **Lancer tous les seeders** : `php artisan db:seed`
- **Lancer un seeder spécifique** : `php artisan db:seed --class=UsersTableSeeder`

### ### Utilisation des Model Factories et Faker
- Les **factories** définissent une structure par défaut pour créer des modèles avec des données fictives.
- Elles se trouvent dans `database/factories/`.
- La librairie **Faker** est utilisée pour générer des données aléatoires (noms, emails, phrases...).

*Exemple de factory pour le modèle `User` :*
```php
// database/factories/UserFactory.php
$factory->define(App\User::class, function (Faker\Generator $faker) {
    return [
        'name' => $faker->name,
        'email' => $faker->unique()->safeEmail,
        'password' => bcrypt('password'),
    ];
});
```

*Utilisation de la factory dans un seeder :*
```php
// database/seeders/UserSeeder.php
public function run()
{
    // Crée 50 utilisateurs
    factory(App\User::class, 50)->create();
}
```

---

## 7. Principes Avancés et Bonnes Pratiques

### ### Injection de Dépendances et Design Pattern Repository
- **Problème** : Écrire la logique de base de données directement dans les contrôleurs les rend difficiles à tester et à maintenir (non-respect du principe DRY - Don't Repeat Yourself).
- **Solution** : **L'injection de dépendances**. On délègue la logique métier à des classes de service ou des "Repositories".
- Laravel peut **automatiquement injecter** une instance de classe dans une méthode de contrôleur grâce au "type-hinting".
- On peut lier une **interface** à une **classe concrète** dans un `ServiceProvider` (ex: `AppServiceProvider`) pour plus de flexibilité.
  ```php
  // app/Providers/AppServiceProvider.php
  public function register()
  {
      $this->app->bind(
          'App\Repositories\EmailRepositoryInterface',
          'App\Repositories\EmailRepository'
      );
  }
  ```

### ### Gestion de Plusieurs Connexions
- Les connexions sont définies dans `config/database.php`.
- On peut spécifier la connexion à utiliser pour une requête :
  - **Query Builder** : `DB::connection('mysql2')->select(...)`
  - **Eloquent (dans le modèle)** : `protected $connection = 'mysql2';`
  - **Eloquent (à la volée)** : `$model->setConnection('mysql2')->find(1);`