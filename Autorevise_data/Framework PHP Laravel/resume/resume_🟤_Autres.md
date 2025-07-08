Cette séance couvre une large gamme de sujets avancés en développement web, principalement axés sur PHP 5 et MySQL 5. Elle commence par des rappels sur MySQL et les bases de la Programmation Orientée Objet (POO), avant de plonger dans des concepts plus complexes tels que la POO avancée (interfaces, classes abstraites, design patterns), la gestion des exceptions, les transactions de base de données avec InnoDB, et la manipulation de flux XML. Le cours aborde également l'optimisation des requêtes SQL, l'architecture des services web (REST et SOAP) et une introduction à la Standard PHP Library (SPL). En complément, des extraits de cours sur le framework Laravel, la sécurité, et d'autres technologies web sont inclus.

## Rappels MySQL (avec mysqli)
### Concepts de base
- Un **champ** est une donnée définie par un type, une longueur et des contraintes.
- Un **enregistrement** est un ensemble de champs.
- Une **table** contient des enregistrements et des champs.
- Un **schéma** (ou base de données) est un ensemble de tables.

### L'extension mysqli
- Permet de profiter des fonctionnalités de **MySQL 4.1 et supérieur**.
- Doit être activée dans la configuration de PHP.
- La connexion se fait via `mysqli_connect()` qui prend 4 arguments :
    - L'adresse du serveur.
    - Le nom d'utilisateur.
    - Le mot de passe.
    - La base de données à utiliser.
- **Bonne pratique** : Factoriser les informations de connexion dans un fichier de configuration.

### Exécuter des requêtes
- La fonction `mysqli_query()` envoie une requête SQL au serveur.
- Elle prend en paramètre l'identifiant de connexion et la requête SQL.

### Récupérer les résultats
- Trois fonctions principales pour récupérer les résultats :
    - `mysqli_fetch_assoc()` : Retourne un **tableau associatif** (nom du champ comme clé).
    - `mysqli_fetch_row()` : Retourne un **tableau indexé numériquement**.
    - `mysqli_fetch_object()` : Retourne un **objet**.
- La fonction `mysqli_close()` ferme la connexion au serveur.

## Gestion des Index MySQL
### Rôle des index
- Les index **accélèrent les lectures** (requêtes `SELECT`).
- Ils peuvent cependant **ralentir les écritures** (`INSERT`, `UPDATE`, `DELETE`).
- La création peut se faire via `CREATE TABLE`, `CREATE INDEX` ou `ALTER TABLE`.

### Types d'index
- **PRIMARY KEY** :
    - Identifiant **unique** d'un enregistrement.
    - Interdit les doublons et les valeurs `NULL`.
    - Un seul par table.
- **UNIQUE** :
    - Interdit les doublons, mais **autorise les valeurs `NULL`**.
    - Plusieurs index `UNIQUE` possibles par table.
- **KEY / INDEX** :
    - Permet d'indexer des champs pouvant avoir des **valeurs identiques**.
- **FULLTEXT** :
    - Optimise la **recherche de mots** dans des champs de type texte (`CHAR`, `VARCHAR`, `TEXT`).
    - Utilise la syntaxe `MATCH(colonne) AGAINST('mots clés')`.
    - Supporte un mode booléen pour des recherches avancées (`+`, `-`, `""`).

## Les bases de la POO en PHP
### Concepts clés
- Une **classe** est une abstraction, un "moule" qui contient des **propriétés** (variables) et des **méthodes** (fonctions).
- Un **objet** est une **instance** d'une classe, créé avec le mot-clé `new`.

### Constructeur et Destructeur
- **Constructeur (`__construct()`)** : Méthode magique appelée automatiquement lors de la création d'un objet (`new`). Utile pour initialiser les propriétés.
- **Destructeur (`__destruct()`)** : Méthode magique appelée à la fin de la vie d'un objet. Utile pour le "nettoyage" (ex: fermer une connexion).

### Visibilité
- **public** : Accessible de partout, à l'intérieur comme à l'extérieur de la classe.
- **protected** : Accessible uniquement dans la classe elle-même et dans ses classes filles (héritage).
- **private** : Accessible uniquement dans la classe où il est défini.

## POO Avancée
### Interfaces
- Se déclarent avec le mot-clé `interface`.
- Définissent un **contrat** qu'une classe doit respecter en l'obligeant à implémenter certaines méthodes.
- Une classe utilise une interface avec le mot-clé `implements`.
- Une interface ne contient que des **déclarations de méthodes**, sans leur contenu.

### Classes abstraites
- Se déclarent avec le mot-clé `abstract`.
- Une classe abstraite **ne peut pas être instanciée** directement.
- Elle sert de **modèle de base** pour d'autres classes qui en hériteront (`extends`).
- Peut contenir des méthodes abstraites (sans corps) et des méthodes concrètes (avec corps).

### Méthodes et constantes magiques
- **Méthodes magiques** (appelées automatiquement) :
    - `__construct`, `__destruct`, `__clone`
    - `__call` : si une méthode inexistante est appelée.
    - `__get` / `__set` : pour accéder/modifier des propriétés inaccessibles.
    - `__toString` : pour définir comment un objet se comporte quand il est traité comme une chaîne.
- **Constantes magiques** (fournissent des informations sur le contexte) :
    - `__FILE__` : Chemin du fichier courant.
    - `__CLASS__` : Nom de la classe courante.
    - `__FUNCTION__` : Nom de la fonction courante.
    - `__LINE__` : Numéro de la ligne courante.

### Motifs de conception (Design Patterns)
- Solutions répertoriées à des problèmes de conception courants.
- **Singleton** : S'assure qu'une classe n'a qu'une seule instance.
- **Fabrique (Factory)** : Objet qui crée d'autres objets.
- **Façade** : Fournit une interface simple pour un système complexe.
- **Observateur (Observer)** : Associe des événements à des actions.
- **MVC (Modèle-Vue-Contrôleur)** :
    - Structure très utilisée pour les applications web.
    - **Modèle** : Gère les données et la logique métier.
    - **Vue** : Gère l'affichage et la présentation.
    - **Contrôleur** : Gère les requêtes de l'utilisateur et orchestre les interactions entre le Modèle et la Vue.

## Gestion des exceptions
### Utilité et Implémentation
- Permet de **gérer les erreurs** d'exécution de manière structurée et élégante.
- Le code susceptible de générer une erreur est placé dans un bloc **`try`**.
- Les erreurs sont "attrapées" et traitées dans un ou plusieurs blocs **`catch`**.
- On lance une exception avec l'instruction `throw new Exception("Message d'erreur");`.
- L'objet exception contient des informations utiles : message, code, fichier, ligne, trace.

### Exceptions personnalisées
- On peut créer ses propres classes d'exception en **étendant la classe `Exception`**.
- Cela permet de gérer différents types d'erreurs de manière plus fine en utilisant des blocs `catch` spécifiques pour chaque type d'exception.

## Moteur transactionnel InnoDB et Transactions SQL
### Moteur InnoDB
- Moteur de stockage **transactionnel** pour MySQL.
- Supporte la norme **ACID** (Atomicité, Cohérence, Isolation, Durabilité).
- Gère les **clés étrangères (`FOREIGN KEY`)** et l'**intégrité référentielle**.
- Ne supporte pas les index `FULLTEXT`.

### Intégrité référentielle
- Garantit la cohérence entre les tables liées par des clés étrangères.
- Les clauses `ON DELETE` et `ON UPDATE` définissent le comportement en cas de modification de la table parente :
    - **CASCADE** : Applique la modification en cascade à la table enfant.
    - **SET NULL** : Met les clés étrangères à `NULL` dans la table enfant.
    - **RESTRICT** / **NO ACTION** : Interdit la modification si des enregistrements liés existent (comportement par défaut).

### Transactions SQL
- Un groupe de requêtes SQL exécutées comme une **opération unique et atomique**.
- Soit **toutes** les requêtes réussissent, soit **aucune** n'est appliquée.
- `START TRANSACTION` ou `BEGIN` : Démarre une transaction.
- `COMMIT` : Valide et enregistre définitivement les modifications.
- `ROLLBACK` : Annule toutes les modifications de la transaction.
- `SAVEPOINT` : Crée un point de sauvegarde intermédiaire dans la transaction, vers lequel on peut revenir avec `ROLLBACK TO SAVEPOINT`.

## Manipulation des Flux XML
### Qu'est-ce que XML ?
- Standard pour **organiser et stocker des données** de manière structurée avec des balises.

### Extensions PHP pour XML
- **SimpleXML** :
    - **Simple** à utiliser, idéale pour la plupart des cas.
    - Permet de lire, modifier, et créer des documents XML en manipulant des objets.
    - Requiert de charger le document en entier en mémoire.
- **DOMXML** :
    - Plus **verbeuse** mais plus puissante.
    - Offre un contrôle total sur la structure du document.
    - Basée sur le standard DOM du W3C.
- **SAX (Simple API for XML)** :
    - Parseur **basé sur les événements**, très **efficace en lecture** et consomme peu de mémoire.
    - Ne charge pas tout le document, mais le lit de manière linéaire.
    - Idéal pour les très gros fichiers, mais ne permet pas l'écriture.

## Optimisation SQL & Architecture de Base de Données
### Optimisation des requêtes
- **`EXPLAIN`** : Commande essentielle pour analyser comment MySQL exécute une requête `SELECT` et voir si les index sont utilisés.
- **Indexation** :
    - Éviter les `LIKE` commençant par un joker (`%`).
    - Créer des index sur les préfixes de colonnes (`nom(10)`) pour économiser de l'espace.
    - Utiliser des index composés pour les requêtes filtrant sur plusieurs colonnes.
- **Requêtes préparées** (`PREPARE`, `EXECUTE`) : Optimisent les requêtes exécutées plusieurs fois en changeant seulement les paramètres.

### Optimisation du schéma
- **Choisir les bons types de données** : Utiliser `INT` au lieu de `BIGINT` si possible, `UNSIGNED` pour les ID, `ENUM` pour des valeurs fixes. `PROCEDURE ANALYSE()` peut aider à suggérer des types optimaux.
- **Normalisation** : Organiser les données pour limiter la redondance et éviter les anomalies.
- **Choisir le bon moteur de stockage** en fonction des besoins :
    - **MyISAM** : Très rapide en lecture, idéal pour les sites à fort trafic de lecture.
    - **InnoDB** : Transactionnel, garantit l'intégrité des données, idéal pour les applications nécessitant des écritures fiables.
    - **MEMORY** : Tables en mémoire, extrêmement rapide mais données non persistantes.
    - **ARCHIVE** : Pour stocker de grandes quantités de données compressées (logs, archives).

## Services Web (REST, SOAP)
### Principe
- Permettent à des systèmes hétérogènes d'**échanger des informations** et d'interagir via le réseau, en utilisant des protocoles standards.

### REST (Representational State Transfer)
- Style d'architecture **léger et simple**.
- Les opérations sont basées sur les **verbes HTTP** (`GET`, `POST`, `PUT`, `DELETE`).
- Les ressources sont identifiées par des **URL**.
- Le format des données n'est pas imposé (souvent **XML** ou **JSON**).

### SOAP (Simple Object Access Protocol) & WSDL
- **Protocole standardisé** pour l'échange de messages structurés en XML.
- Plus **complexe** et strict que REST.
- **WSDL (Web Services Description Language)** : Fichier XML qui décrit le service web (opérations, paramètres, etc.), agissant comme un "mode d'emploi".
- PHP 5 fournit une extension native `SoapServer` et `SoapClient` pour créer et consommer des services SOAP.

## Introduction à la SPL (Standard PHP Library)
### Qu'est-ce que la SPL ?
- Une **collection de classes et d'interfaces** natives de PHP.
- Fournit des structures de données et des itérateurs pour résoudre des problèmes courants.

### Itérateurs
- Un **itérateur** est un objet qui permet de parcourir une collection d'éléments (comme un tableau) avec une boucle `foreach`.
- La SPL fournit de nombreux itérateurs prêts à l'emploi (`ArrayIterator`, `DirectoryIterator`, `FilterIterator`, etc.).
- On peut créer ses propres itérateurs en implémentant l'interface `Iterator`, qui oblige à définir les méthodes : `rewind()`, `current()`, `key()`, `next()`, `valid()`.

## Introduction au Framework Laravel
### Créer un service
- Un **service** est une classe PHP qui fournit une fonctionnalité spécifique (par exemple, `OurService` avec une méthode `getNumber()`).

### Conteneur de services et Fournisseur de services (Service Provider)
- Pour éviter d'instancier manuellement un service à chaque fois (`new OurService()`), on l'enregistre dans le **conteneur de services** de Laravel.
- Cela se fait via un **Fournisseur de services** (Service Provider), une classe qui étend `Illuminate\Support\ServiceProvider`.
- Dans la méthode **`register()`** du provider, on lie le service au conteneur, souvent en tant que **singleton** pour qu'il ne soit créé qu'une seule fois :
  `$this->app->singleton('OurService', function() { return new OurService(); });`
- Le fournisseur doit être enregistré dans le tableau `providers` du fichier **`config/app.php`**.

### Accéder au service
- Une fois enregistré, le service peut être obtenu de plusieurs manières :
    - **Injection de dépendances** : En typant le service dans le constructeur ou une méthode d'un contrôleur, Laravel l'injecte automatiquement.
    - **Via le helper `app()`** : `app('OurService')->getNumber();`.

### Les façades (Facades)
- Une **façade** offre une interface **statique** et simple à un service enregistré dans le conteneur.
- Pour créer une façade, on crée une classe qui étend `Illuminate\Support\Facades\Facade`.
- On doit implémenter la méthode `getFacadeAccessor()` qui retourne le nom du service enregistré (ex: `'OurService'`).
- La façade doit être enregistrée comme un alias dans le tableau `aliases` de **`config/app.php`** (ex: `'Randomisator' => App\Services\OurService\OurServiceFacade::class`).
- On peut alors appeler le service de manière statique : `Randomisator::getNumber();`.

### Fonctions d'assistance (Helpers)
- Pour un accès encore plus simple, notamment dans les vues, on peut créer une **fonction d'assistance** globale.
- On crée un fichier (ex: `helpers.php`) contenant la fonction, qui utilise le helper `app()` pour retourner l'instance du service.
- Ce fichier doit être inclus dans la section `files` de la clé `autoload` du fichier **`composer.json`**.
- Après un `composer dump-autoload`, la fonction est disponible partout (ex: `{{ randomisator()->getNumber() }}`).

## Autres Ressources Pédagogiques (Extraits)
### Frameworks PHP
- Un **framework** fournit une structure et des composants réutilisables pour accélérer le développement.
- Il impose des **règles d'architecture** (comme le **MVC**) et de codage.
- **Inversion de Contrôle (IoC)** : Le framework appelle votre code, et non l'inverse.
- **MVC (Modèle-Vue-Contrôleur)** :
    - **M**odèle : Gère les données et la logique métier.
    - **V**ue : Gère la présentation (templates HTML).
    - **C**ontrôleur : Orchestre les interactions, reçoit les requêtes et renvoie les réponses.

### Sécurité Web (OWASP Top 10)
- **Injections (SQL, XSS)** : Valider et neutraliser toutes les entrées utilisateur. Utiliser les requêtes préparées et les entités HTML.
- **Contrôle d'accès défaillant** : S'assurer que les utilisateurs ne peuvent accéder qu'aux ressources autorisées.
- **Mots de passe** : Utiliser des fonctions de hachage robustes (`password_hash()`, `bcrypt`). Ne jamais stocker de mots de passe en clair.
- **CSRF (Cross-Site Request Forgery)** : Utiliser des tokens CSRF pour s'assurer que les requêtes proviennent bien de votre application.
- **Utiliser un framework** est une bonne pratique, car ils intègrent des protections contre de nombreuses failles courantes.

### Bonnes Pratiques
- **DRY (Don't Repeat Yourself)** : Ne pas dupliquer le code.
- **KISS (Keep It Simple and Stupid)** : Privilégier la simplicité.
- **Convention Over Configuration** : Suivre les conventions du framework pour éviter la configuration manuelle.
- **Principes SOLID** : Ensemble de 5 principes pour une conception orientée objet propre et maintenable.
- **Tests unitaires** : Écrire des tests pour vérifier le bon fonctionnement des parties isolées du code, ce qui facilite la maintenance et le refactoring.