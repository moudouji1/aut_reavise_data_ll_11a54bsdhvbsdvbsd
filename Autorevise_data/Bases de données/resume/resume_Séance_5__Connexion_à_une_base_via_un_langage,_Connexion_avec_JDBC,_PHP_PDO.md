## Résumé de la Séance 5 : Connexion aux Bases de Données

Cette séance explore les deux principales approches pour connecter une application à une base de données : l'une utilisant le langage de script côté serveur **PHP**, et l'autre utilisant l'API **JDBC** (Java Database Connectivity) pour les applications Java. Elle couvre les concepts fondamentaux, la syntaxe essentielle, et les étapes clés pour établir une connexion, exécuter des requêtes et récupérer des données dans les deux écosystèmes.

---

## Partie 1 : Connexion à une base de données avec PHP

### ### Introduction à PHP et au couple PHP/MySQL

*   **PHP (Hypertext Preprocessor)** :
    *   Langage de script **Open Source** exécuté côté **serveur**.
    *   Spécialement conçu pour le développement web et peut être intégré directement dans du code **HTML**.
    *   La syntaxe s'inspire des langages C, Perl et Java.
    *   Le code source PHP n'est jamais visible par le client, ce qui assure sa **protection**.

*   **Le couple PHP/MySQL** :
    *   Une combinaison très populaire pour le développement web dynamique.
    *   **PHP** gère la logique de l'application (le traitement).
    *   **MySQL** est le **SGBD** (Système de Gestion de Bases de Données) qui stocke et gère les données.
    *   L'environnement de développement typique inclut : un serveur web (**Apache**), un SGBDR (**MySQL**) et le langage de script (**PHP**).

### ### Syntaxe Essentielle pour la Manipulation de Données

*   **Intégration et Syntaxe de base** :
    *   Le code PHP est inséré dans des balises : `<?php ... ?>`.
    *   Chaque instruction se termine par un point-virgule (`;`).
    *   Les fonctions `echo` et `print` sont utilisées pour envoyer des données (texte, HTML) au navigateur.

*   **Variables** :
    *   Un nom de variable commence toujours par un dollar (`$`), par exemple `$nom_variable`.
    *   Les noms sont **sensibles à la casse** (`$nom` et `$Nom` sont deux variables différentes).
    *   **Types scalaires** : booléen, entier, flottant, chaîne de caractères.
    *   **Types non scalaires** : tableaux, objets.
    *   **Variables superglobales** : tableaux prédéfinis contenant des informations sur le serveur, la requête, etc. Exemples : `$_GET`, `$_POST`, `$_SERVER`.

*   **Chaînes de caractères (Strings)** :
    *   Délimitées par des apostrophes (`'`) ou des guillemets (`"`).
    *   L'opérateur de concaténation est le point (`.`). Exemple : `$phrase = "Bonjour " . $nom;`.
    *   La fonction `strlen()` permet de connaître la longueur d'une chaîne.

*   **Tableaux (Arrays)** :
    *   Collection de couples **clé/valeur**.
    *   **Tableaux indexés** : les clés sont des entiers (par défaut à partir de 0).
    *   **Tableaux associatifs** : les clés sont des chaînes de caractères.
    *   La boucle `foreach` est idéale pour parcourir les éléments d'un tableau.

### ### Interagir avec la base de données via un formulaire HTML

*   **Formulaires HTML** :
    *   La balise `<form>` a deux attributs essentiels :
        *   `action` : spécifie le script PHP qui traitera les données.
        *   `method` : `GET` (données dans l'URL) ou `POST` (données dans le corps de la requête, plus sécurisé).

*   **Récupération des données en PHP** :
    *   Les données envoyées par un formulaire sont disponibles dans les tableaux superglobaux `$_GET` ou `$_POST`.
    *   Exemple : la valeur d'un champ `<input name="nom">` est accessible via `$_POST['nom']`.

*   **Validation des données** :
    *   Il est crucial de valider les données reçues avant de les utiliser.
    *   `isset($variable)` : vérifie si une variable est définie et n'est pas `NULL`.
    *   `strlen($chaine) > 0` : vérifie qu'une chaîne de caractères n'est pas vide.

*   **Note importante :** Bien que le titre de la séance mentionne **PHP PDO**, le contenu détaillé se concentre sur les bases de PHP. **PDO (PHP Data Objects)** est l'interface moderne et sécurisée pour accéder aux bases de données en PHP, et son étude est recommandée pour éviter les injections SQL.

---

## Partie 2 : Connexion à une base de données avec Java (JDBC)

### ### Introduction à JDBC

*   **JDBC (Java DataBase Connectivity)** est une **API** (Application Programming Interface) standard en Java.
*   Elle est composée d'un ensemble d'interfaces et de classes dans les packages `java.sql` et `javax.sql`.
*   Son but est de permettre aux applications Java de se connecter et d'interagir avec quasiment n'importe quelle base de données (Oracle, MySQL, PostgreSQL, etc.), garantissant la portabilité.

### ### Architecture et Composants Clés

*   #### Le Pilote (Driver)
    *   C'est le composant logiciel qui fait le pont entre l'application Java et la base de données. C'est une implémentation de l'interface `java.sql.Driver`.
    *   Il existe **4 types de pilotes** :
        1.  **Pont JDBC-ODBC** : Traduit les appels JDBC en appels ODBC.
        2.  **API native** : Utilise les bibliothèques du client de la base de données.
        3.  **Réseau pur Java** : Passe par un middleware qui traduit les requêtes.
        4.  **Protocole natif pur Java** : Communique directement avec la base de données via son protocole réseau. C'est le **type le plus courant et recommandé**.

*   #### Le Gestionnaire de Pilotes (DriverManager)
    *   Une classe qui gère la liste des pilotes disponibles et établit les connexions.
    *   La méthode principale est `DriverManager.getConnection()`.

*   #### La Connexion (Connection)
    *   Représente une session (une connexion active) avec la base de données.
    *   L'**URL JDBC** est une chaîne de caractères standardisée pour identifier une source de données : `jdbc:<sous-protocole>:<informations_spécifiques>`.
    *   Exemple pour MySQL : `jdbc:mysql://localhost:3306/ma_base`.

### ### Étapes d'une Opération JDBC

1.  **Charger le pilote** : Indique à l'application quel pilote utiliser.
    *   `Class.forName("com.mysql.cj.jdbc.Driver");`

2.  **Établir la connexion** : Obtient un objet `Connection`.
    *   `Connection con = DriverManager.getConnection(url, utilisateur, motDePasse);`

3.  **Créer une instruction (Statement)** : Crée un objet pour envoyer des requêtes SQL.
    *   `Statement stmt = con.createStatement();`
    *   Il est **fortement recommandé** d'utiliser `PreparedStatement` pour les requêtes avec des paramètres afin de **prévenir les injections SQL**.
    *   `PreparedStatement pstmt = con.prepareStatement("SELECT * FROM utilisateurs WHERE nom = ?");`

4.  **Exécuter la requête** :
    *   Pour les requêtes de sélection (SELECT) : `ResultSet rs = stmt.executeQuery("SELECT ...");`
    *   Pour les mises à jour (INSERT, UPDATE, DELETE) : `int lignesModifiees = stmt.executeUpdate("UPDATE ...");`

5.  **Traiter les résultats (ResultSet)** :
    *   Un `ResultSet` est un objet qui contient les lignes retournées par une requête.
    *   On le parcourt avec une boucle `while` et la méthode `rs.next()`.
    *   `while(rs.next()) { String nom = rs.getString("nom_colonne"); }`

6.  **Fermer les ressources** :
    *   Il est **impératif** de fermer les ressources (`ResultSet`, `Statement`, `Connection`) pour éviter les fuites de mémoire.
    *   Cette opération doit toujours être effectuée dans un bloc `finally`.

### ### Concepts Avancés

*   **Sources de Données (DataSource)** :
    *   Une interface du package `javax.sql` qui est la **méthode préférée** pour obtenir une connexion.
    *   Avantages : configuration centralisée, support pour le **pooling de connexions** (réutilisation des connexions pour de meilleures performances).

*   **Métadonnées (MetaData)** :
    *   Permet d'obtenir des informations sur la base de données elle-même.
    *   `DatabaseMetaData` : informations sur le SGBD (version, tables, procédures supportées, etc.).
    *   `ResultSetMetaData` : informations sur les résultats d'une requête (nombre de colonnes, noms, types, etc.).

*   **Gestion des Erreurs** :
    *   Les erreurs JDBC lèvent une `java.sql.SQLException`.
    *   Utiliser des blocs `try-catch-finally` pour gérer ces exceptions et garantir la fermeture des ressources.