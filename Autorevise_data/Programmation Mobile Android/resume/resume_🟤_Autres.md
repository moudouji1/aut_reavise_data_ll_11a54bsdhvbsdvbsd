# Résumé de la séance : Autres

Cette séance est une compilation de plusieurs cours et tutoriels couvrant divers domaines du développement logiciel. Elle aborde en profondeur le **développement natif Android**, y compris son architecture, ses composants, la création d'interfaces, et la gestion des données. Elle explore ensuite le **développement backend** avec un guide sur la création d'API REST en Python avec Flask. Des sections dédiées traitent de plateformes spécifiques comme le **système ERP Odoo** et le **framework JavaFX** pour les applications de bureau. Enfin, une introduction au **développement mobile cross-platform** avec Flutter est également incluse.

## Développement Android (Généralités et Concepts Approfondis)

### 1. Environnement et Architecture
- **Écosystème Android** : Repose sur **Java/Kotlin** et le **SDK Android**. Android Studio est l'IDE principal.
- **Architecture du système** : Basé sur un **noyau Linux**, une couche d'abstraction matérielle (HAL), la machine virtuelle **Dalvik/ART** (exécutant des fichiers `.dex` optimisés), des bibliothèques natives (SQLite, OpenGL) et des applications.
- **Structure d'un projet** :
    - `src/` : Code source Java/Kotlin.
    - `res/` : Ressources (layouts, drawables, strings, etc.).
    - `AndroidManifest.xml` : Déclare les composants, permissions et caractéristiques de l'application.
    - `build.gradle` : Scripts de compilation et de dépendances.

### 2. Composants Fondamentaux
- **Activity** : Représente un **écran unique** avec une interface utilisateur. Gère les interactions utilisateur.
- **Service** : Composant exécutant des **opérations en arrière-plan** sans interface utilisateur (ex: lecteur de musique).
- **BroadcastReceiver** : Écoute et réagit à des **messages système ou applicatifs** (Intents) à l'échelle du système (ex: batterie faible, SMS reçu).
- **ContentProvider** : Gère un **ensemble partagé de données** applicatives, permettant l'échange d'informations entre applications (ex: contacts).
- **Cycle de vie d'une Activity** :
    - `onCreate()` : Création de l'activité. Initialisation des vues et des données.
    - `onStart()` / `onStop()` : L'activité devient visible / invisible.
    - `onResume()` / `onPause()` : L'activité gagne / perd le focus (premier plan). C'est le bon endroit pour sauvegarder les données non persistantes.
    - `onDestroy()` : L'activité est détruite.
    - `onSaveInstanceState(Bundle)` : Permet de sauvegarder l'état de l'interface avant que l'activité ne soit détruite (ex: rotation de l'écran). L'état est restauré dans `onCreate()`.

### 3. Interfaces Graphiques (UI)
- **Vues (Views)** : Blocs de construction de base de l'UI (`Button`, `TextView`, `EditText`, `ImageView`).
- **Layouts (Gabarits)** : Conteneurs (`ViewGroup`) qui organisent les vues.
    - `LinearLayout` : Aligne les enfants **horizontalement** ou **verticalement**.
    - `RelativeLayout` : Positionne les enfants les uns **par rapport aux autres** ou par rapport au parent.
    - `ConstraintLayout` : Similaire à `RelativeLayout` mais plus flexible et puissant, optimisé pour l'éditeur visuel.
    - `FrameLayout` : Empile les enfants les uns sur les autres.
- **Ressources UI** : Déclarées en **XML** dans le dossier `res/`.
    - `res/layout/` : Fichiers XML définissant la structure des vues.
    - `res/drawable/` : Images, formes, icônes.
    - `res/values/` : Chaînes de caractères (`strings.xml`), couleurs (`colors.xml`), dimensions (`dimens.xml`).
- **Internationalisation** : Gérée via des dossiers de ressources spécifiques à la langue (ex: `values-fr/`, `values-es/`).
- **Listes et Grilles** :
    - `ListView` / `RecyclerView` : Affiche une liste déroulante d'éléments.
    - **Adapter** : Pont entre une source de données (ex: `ArrayList`, `Cursor`) et une `AdapterView` (`ListView`, `GridView`).
    - `ArrayAdapter` : Pour les listes simples basées sur un tableau.
    - **Adapters personnalisés** : Nécessaire pour des layouts de ligne complexes. On hérite de `BaseAdapter` ou `ArrayAdapter` et on surcharge `getView()`.
    - **ViewHolder Pattern** : Optimisation essentielle pour les listes, évitant les appels répétitifs à `findViewById()` en recyclant les vues.

### 4. Communication entre Composants (Intents)
- **Intent** : Objet de messagerie utilisé pour demander une action à un autre composant applicatif.
- **Intent Explicite** : Cible un composant spécifique en nommant sa classe. Utilisé pour la navigation **au sein de sa propre application**.
    - `Intent i = new Intent(this, SecondActivity.class); startActivity(i);`
- **Intent Implicite** : Ne spécifie pas de composant, mais une **action générale** (`ACTION_VIEW`, `ACTION_DIAL`). Le système Android trouve le composant approprié pour gérer l'intent.
    - `Uri number = Uri.parse("tel:12345"); Intent callIntent = new Intent(Intent.ACTION_DIAL, number);`
- **Données d'Intent (Extras)** : Permet de passer des données simples (clés-valeurs) entre les activités via `putExtra()` et `get...Extra()`.
- **Retourner un résultat** : `startActivityForResult()` permet à une activité "enfant" de retourner un résultat à son parent. Le parent gère ce résultat dans `onActivityResult()`.

### 5. Persistance des Données
- **SharedPreferences** : Stockage de paires **clé-valeur** simples et privées (préférences, petits états).
- **Fichiers** : Stockage sur la **mémoire interne** (privée à l'application) ou **externe** (partagée).
- **Base de données SQLite** : Base de données relationnelle complète intégrée.
    - `SQLiteOpenHelper` : Classe d'aide pour gérer la **création** et la **mise à jour** de la base de données.
    - `Cursor` : Objet représentant le résultat d'une requête, permettant d'itérer sur les lignes.

### 6. Programmation Concurrente
- **Thread Principal (UI Thread)** : Seul thread autorisé à **modifier l'interface graphique**. Les opérations longues (réseau, BDD) sur ce thread provoquent des erreurs **ANR (Application Not Responding)**.
- **AsyncTask** (déprécié mais conceptuellement important) : Classe d'aide pour effectuer des opérations en arrière-plan et publier les résultats sur le thread UI sans manipulation manuelle des threads.
- **Services** : Pour des tâches de **longue durée** qui doivent s'exécuter même si l'application n'est pas au premier plan.
- **IntentService** : Sous-classe de `Service` qui gère les requêtes asynchrones dans un **thread de travail**.

### 7. Assemblage et Déploiement
- **Dalvik & Smali** : Le code Java est compilé en bytecode Dalvik (`.dex`). **Smali** est le langage d'assemblage correspondant, utile pour le reverse engineering.
- **Génération de l'APK** : `apktool` est utilisé pour compiler les ressources et le code `smali` en un fichier `.apk`.
- **Signature de l'APK** : Une application doit être **signée numériquement** pour être installée sur un appareil.
    - `keytool` : Crée un dépôt de clés (`.keystore`).
    - `jarsigner` : Signe l'APK avec la clé.
- **Décompilation** :
    - `dex2jar` : Convertit un fichier `.dex` en un fichier `.jar`.
    - `jd-gui` : Permet de visualiser le code source Java à partir du `.jar`.

## Développement d'API REST avec Python et Flask

### 1. Mise en Place et Premier Endpoint
- **Flask** : Micro-framework web pour Python, idéal pour créer des API REST.
- **Connexion** : Framework construit sur Flask qui gère automatiquement les requêtes HTTP en se basant sur une spécification **OpenAPI (Swagger)**.
- **Swagger/OpenAPI** : Fichier de configuration (YAML ou JSON) qui décrit les **endpoints** de l'API, les paramètres attendus, les réponses, etc. Permet de générer une **documentation interactive** (Swagger UI).

### 2. Intégration d'une Base de Données
- **SQLAlchemy** : ORM (Object-Relational Mapper) pour Python qui permet de mapper des objets Python à des tables de base de données.
- **Modèles** : Classes Python qui définissent la structure des tables de la base de données.
- **Marshmallow** : Bibliothèque pour la **sérialisation/désérialisation** d'objets. Elle convertit les objets complexes (comme les modèles SQLAlchemy) en types de données simples (dictionnaires, listes) compatibles avec JSON, et vice-versa.

### 3. Gestion des Relations
- **Clé étrangère (Foreign Key)** : Mécanisme de base pour lier deux tables dans une base de données relationnelle.
- **Relations One-to-Many** : Gérées dans SQLAlchemy avec `db.relationship`, permettant de lier un enregistrement parent à plusieurs enregistrements enfants (ex: une personne et ses notes).
- **Schémas imbriqués** : Marshmallow permet de définir des schémas qui incluent d'autres schémas, pour sérialiser et désérialiser des objets liés.

## Développement sur la plateforme Odoo

### 1. Architecture et Structure d'un Module
- **Architecture à trois niveaux** : **Présentation** (HTML5, JS, CSS, OWL Framework), **Logique** (Python) et **Données** (PostgreSQL).
- **Module** : Unité de base d'une fonctionnalité dans Odoo. Peut ajouter ou modifier une logique métier.
- **Structure d'un module** :
    - `__manifest__.py` : Fichier de manifeste décrivant le module, ses dépendances (`depends`), et ses fichiers de données (`data`).
    - `__init__.py` : Initialise le paquet Python du module.
    - `models/` : Contient les définitions des objets métier (classes Python).
    - `views/` : Contient les fichiers XML définissant les interfaces utilisateur (vues).
    - `security/` : Contient les règles de sécurité, notamment `ir.model.access.csv`.
    - `data/` et `demo/` : Fichiers de données de base et de démonstration.

### 2. Modèles et Champs
- **ORM (Object-Relational Mapping)** : Odoo utilise un ORM puissant qui mappe les classes Python à des tables de base de données.
- **Modèle** : Défini par une classe Python héritant de `models.Model`. L'attribut `_name` définit le nom technique du modèle (ex: `estate.property`).
- **Champs de base** : `Char`, `Text`, `Integer`, `Float`, `Boolean`, `Date`, `Datetime`.
- **Champs relationnels** :
    - `Many2one` : Relation "plusieurs-à-un" (clé étrangère).
    - `One2many` : Relation inverse d'un `Many2one`.
    - `Many2many` : Relation "plusieurs-à-plusieurs".
- **Champs calculés** : Leur valeur est calculée via une méthode Python décorée avec `@api.depends(...)`.
- **Onchanges** : Méthodes décorées avec `@api.onchange(...)` qui se déclenchent dans l'UI lorsque la valeur d'un champ change pour mettre à jour d'autres champs du formulaire.

### 3. Vues, Actions et Menus
- **Vues** : Définissent comment les enregistrements sont affichés. Déclarées en XML.
    - **Vue Liste (Tree)** : Affiche les enregistrements sous forme de tableau.
    - **Vue Formulaire (Form)** : Affiche un enregistrement unique pour l'édition.
    - **Vue Recherche (Search)** : Définit les filtres et les options de regroupement.
    - **Vue Kanban** : Affiche les enregistrements sous forme de cartes.
- **Actions (Window Actions)** : Déclenchent l'affichage des vues pour un modèle. Elles lient les menus aux vues.
- **Menus** : Créent des entrées dans l'interface utilisateur pour déclencher des actions.

### 4. Sécurité
- **Groupes d'utilisateurs** : Associent des permissions à des rôles (`res.groups`).
- **Droits d'accès (ACL)** : Définis dans `security/ir.model.access.csv`. Spécifient les permissions de **lecture (read), écriture (write), création (create) et suppression (unlink)** pour un groupe sur un modèle.
- **Règles d'enregistrement (Record Rules)** : Filtrent les enregistrements auxquels un utilisateur peut accéder en fonction de conditions spécifiques (domaines).

### 5. Héritage
- **Héritage de modèle** : Permet de modifier un modèle existant en utilisant l'attribut `_inherit`. On peut ajouter des champs ou surcharger des méthodes existantes.
- **Héritage de vue** : Permet de modifier une vue existante en utilisant une balise `<xpath>`.

## Développement d'applications Cross-Platform avec Flutter

### 1. Introduction à Flutter et Dart
- **Flutter** : Framework open source de Google pour créer des applications **compilées nativement** pour mobile, web et bureau à partir d'une **base de code unique**.
- **Langage Dart** : Langage de programmation orienté objet, développé par Google, qui est la base de Flutter. Syntaxe similaire à Java/C++.
- **Principe "Tout est un Widget"** : L'interface utilisateur est construite en combinant et en imbriquant des **widgets**.

### 2. Widgets et Mise en Page
- **Widgets de base** : `Text`, `Icon`, `Image`, `ElevatedButton`, `TextFormField`.
- **Widgets de mise en page (Layout)** :
    - `Container` : Widget de base pour le style, le padding, les marges.
    - `Row` / `Column` : Pour aligner des enfants horizontalement ou verticalement.
    - `ListView` / `GridView` : Pour afficher des listes ou des grilles d'éléments déroulants.
    - `Scaffold` : Implémente la structure visuelle de base d'une page (AppBar, Body, FloatingActionButton).
    - `Card` : Affiche une carte avec une ombre et des coins arrondis.

### 3. Persistance et Réseaux
- **SharedPreferences** : Stockage simple de paires clé-valeur, idéal pour les préférences.
- **SQLite** : Intégration de bases de données locales via le package `sqflite`.
- **Requêtes HTTP** : Le package `http` permet de communiquer avec des serveurs web et des API REST.

## Développement d'applications Desktop avec JavaFX

### 1. Principes de Base
- **Métaphore du théâtre** :
    - `Stage` : La fenêtre principale de l'application.
    - `Scene` : Le contenu de la fenêtre, contenant le graphe de scène.
    - `Node` : Élément de base du graphe de scène (un bouton, une forme, un layout).
- **Cycle de vie** : Une application JavaFX étend `javafx.application.Application` et surcharge la méthode `start(Stage primaryStage)`.

### 2. Composants et Layouts
- **Composants (Controls)** : `Button`, `Label`, `TextField`, `CheckBox`, `RadioButton`, `TableView`.
- **Layouts (Panes)** : Conteneurs pour organiser les composants.
    - `HBox` / `VBox` : Disposition horizontale ou verticale.
    - `BorderPane` : Divise la scène en 5 régions (Top, Bottom, Left, Right, Center).
    - `GridPane` : Disposition en grille flexible.
    - `StackPane` : Empile les enfants les uns sur les autres.
    - `FlowPane` : Dispose les enfants en flux, avec retour à la ligne automatique.

### 3. FXML et CSS
- **FXML** : Langage de balisage basé sur XML pour définir l'interface utilisateur, séparant la vue du contrôleur (logique).
- **Scene Builder** : Outil visuel pour concevoir des interfaces et générer des fichiers FXML.
- **Contrôleur** : Classe Java liée à un FXML (via `fx:controller`) qui gère les événements et la logique de l'interface. L'annotation `@FXML` est utilisée pour injecter les éléments de l'UI dans le code.
- **CSS** : JavaFX peut être stylisé en utilisant des feuilles de style CSS, permettant une personnalisation complète de l'apparence.

### 4. Gestion des Événements et Liaisons (Bindings)
- **Gestionnaires d'événements** : Logique exécutée en réponse à une action utilisateur (ex: `button.setOnAction(...)`).
- **Propriétés JavaFX** : Objets observables (`StringProperty`, `IntegerProperty`) qui permettent des liaisons.
- **Liaisons (Bindings)** : Permettent de synchroniser automatiquement la valeur de deux propriétés. Si l'une change, l'autre est mise à jour.