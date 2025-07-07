```json
{
  "titre_seance": "Séance 3 : Interaction avec les bases de données, Connexion à une base, Exécution de requêtes SQL",
  "chapitres": [
    {
      "titre": "1. Principes de l'interaction avec les bases de données",
      "resume": "Cette section introduit les concepts fondamentaux de l'utilisation des bases de données avec PHP.\n- **Pourquoi une base de données ?** : Comparées aux fichiers texte, les bases de données offrent une gestion des données supérieure en termes de structure, vitesse d'accès, sécurité et gestion des accès simultanés.\n- **Support par PHP** : PHP supporte nativement une grande variété de Systèmes de Gestion de Bases de Données (SGBD) comme MySQL, PostgreSQL, Oracle, etc.\n- **Connexion Native vs ODBC** : La connexion via un driver natif (spécifique au SGBD) est la plus performante. Alternativement, PHP peut utiliser un driver ODBC (Open Database Connectivity) pour se connecter à des bases de données non supportées nativement, offrant une meilleure portabilité au détriment de la performance.\n- **L'environnement de développement** : Une application web typique utilisant une base de données repose sur une pile logicielle composée d'un serveur web (ex: Apache), d'un SGBD (ex: MySQL) et d'un langage de script (PHP)."
    },
    {
      "titre": "2. Gérer une base de données MySQL avec phpMyAdmin",
      "resume": "phpMyAdmin est une interface web graphique essentielle pour administrer les bases de données MySQL sans avoir à écrire de requêtes SQL manuellement.\n- **Fonctionnalités principales** :\n  - **Gestion des bases de données** : Créer et supprimer des bases de données.\n  - **Gestion des tables** : Créer, modifier la structure (colonnes, types de données, index), et supprimer des tables.\n  - **Gestion des données** : Insérer, afficher, modifier et supprimer des enregistrements.\n  - **Import/Export** : Importer des données depuis des fichiers (ex: .txt, .csv, .sql) et exporter la base.\n- **Avantage pédagogique** : Pour chaque opération effectuée via l'interface, phpMyAdmin affiche la requête SQL correspondante, ce qui est un excellent moyen d'apprendre le langage SQL."
    },
    {
      "titre": "3. Communiquer avec MySQL en PHP (extension mysql_*)",
      "resume": {
        "introduction": "L'interaction avec une base de données MySQL en PHP suit un processus en 5 étapes clés. Ce cours utilise l'ancienne extension `mysql_*`.",
        "etapes": [
          {
            "nom": "Étape 1 : Connexion au serveur",
            "description": "Établir la connexion avec le serveur MySQL. Il est recommandé de stocker les identifiants (hôte, utilisateur, mot de passe) dans un fichier de configuration séparé et de l'inclure avec `include()`.",
            "fonctions_cles": [
              "`mysql_connect(host, user, password)` : Retourne un identifiant de connexion ou `false` en cas d'échec."
            ]
          },
          {
            "nom": "Étape 2 : Sélection de la base de données",
            "description": "Choisir la base de données sur laquelle les requêtes seront exécutées.",
            "fonctions_cles": [
              "`mysql_select_db(db_name, conn_id)` : Sélectionne la base de données active."
            ]
          },
          {
            "nom": "Étape 3 : Exécution de requêtes SQL",
            "description": "Envoyer une requête SQL (sous forme de chaîne de caractères) au SGBD.",
            "fonctions_cles": [
              "`mysql_query(sql_string, conn_id)` : Exécute la requête. Retourne `true`/`false` pour les requêtes de modification (`INSERT`, `UPDATE`, `DELETE`) et un identifiant de résultat pour les requêtes `SELECT`."
            ]
          },
          {
            "nom": "Étape 4 : Traitement des résultats",
            "description": "Pour une requête `SELECT`, il faut parcourir les résultats pour les exploiter.",
            "fonctions_cles": [
              "`mysql_num_rows(result_id)` : Renvoie le nombre de lignes dans le résultat.",
              "`mysql_fetch_row(result_id)` : Récupère une ligne du résultat sous forme de tableau indexé numériquement. S'utilise typiquement dans une boucle `while` pour parcourir tous les enregistrements.",
              "`mysql_result(result_id, row, field)` : Permet d'accéder à la valeur d'un champ spécifique.",
              "`mysql_free_result(result_id)` : Libère la mémoire allouée pour un résultat."
            ]
          },
          {
            "nom": "Étape 5 : Déconnexion",
            "description": "Fermer la connexion au serveur MySQL pour libérer les ressources.",
            "fonctions_cles": [
              "`mysql_close(conn_id)` : Ferme la connexion."
            ]
          }
        ],
        "gestion_erreurs": "Il est crucial de tester le retour de chaque fonction MySQL. L'opérateur `@` peut être utilisé pour supprimer les messages d'erreur PHP par défaut. La fonction `die()` permet d'arrêter le script en affichant un message personnalisé. `mysql_error()` et `mysql_errno()` retournent respectivement le message et le numéro de la dernière erreur survenue.",
        "note_importante": "L'extension `mysql_*` est **obsolète** depuis PHP 5.5 et a été **supprimée** en PHP 7. Les développements modernes doivent utiliser les extensions `MySQLi` ou `PDO`, qui offrent plus de fonctionnalités, de performance et de sécurité (notamment avec les requêtes préparées)."
      }
    },
    {
      "titre": "4. Le langage SQL pour MySQL",
      "resume": {
        "types_donnees": "MySQL propose trois grandes familles de types de données :\n- **Numériques** : `TINYINT`, `INT`, `BIGINT` (entiers), `FLOAT`, `DOUBLE` (nombres à virgule flottante), `DECIMAL` (pour les calculs exacts).\n- **Date et Heure** : `DATE`, `TIME`, `DATETIME`, `TIMESTAMP`, `YEAR`.\n- **Chaînes de caractères** : `CHAR` (taille fixe), `VARCHAR` (taille variable), `TEXT` (texte long), `ENUM` (liste de valeurs prédéfinies), `SET` (ensemble de valeurs possibles).",
        "commandes_structure_ddl": "Commandes pour gérer la structure de la base (Data Definition Language) :\n- `CREATE DATABASE nom_base;`\n- `DROP DATABASE nom_base;`\n- `USE nom_base;`\n- `CREATE TABLE nom_table (def_colonne1, ...);` : Attributs de colonne importants : `NOT NULL`, `DEFAULT`, `AUTO_INCREMENT`, `PRIMARY KEY`.\n- `ALTER TABLE nom_table ...;` : Pour modifier une table (ajouter/supprimer une colonne, etc.).\n- `DROP TABLE nom_table;`",
        "commandes_donnees_dml": "Commandes pour manipuler les données (Data Manipulation Language) :\n- `INSERT INTO nom_table (col1, col2) VALUES (val1, val2);`\n- `UPDATE nom_table SET col1 = val1 WHERE condition;`\n- `DELETE FROM nom_table WHERE condition;`",
        "commande_selection_dql": "Commande pour interroger les données (Data Query Language) :\n- `SELECT col1, col2 FROM nom_table WHERE condition ORDER BY col_tri ASC|DESC LIMIT offset, nombre;`\n- La clause `WHERE` utilise des opérateurs comme `=`, `!=`, `>`, `<`, `AND`, `OR`, `LIKE` (recherche de motifs avec `%`), `BETWEEN` (intervalles), `IN` (liste de valeurs)."
      }
    },
    {
      "titre": "5. Principes de sécurité",
      "resume": "La sécurité des applications web manipulant des bases de données est primordiale.\n- **Principe fondamental** : Ne jamais faire confiance aux données provenant de l'utilisateur.\n- **Injection SQL (A1 du Top 10 OWASP)** : C'est une attaque majeure où un utilisateur malveillant insère du code SQL dans les champs d'un formulaire pour manipuler les requêtes de la base de données. L'impact peut être très grave : vol, modification ou suppression de données, voire prise de contrôle du serveur.\n- **Mesures de protection (code)** :\n  - **Échappement des données** : Utiliser des fonctions comme `mysql_real_escape_string()` pour neutraliser les caractères spéciaux dans les entrées utilisateur.\n  - **Validation des données** : Toujours vérifier le format des données reçues (par exemple, s'assurer qu'un nombre est bien un nombre).\n  - **Note** : La meilleure pratique moderne est d'utiliser des **requêtes préparées** (disponibles avec MySQLi ou PDO), qui séparent la requête de ses paramètres et préviennent les injections par conception.\n- **Autres bonnes pratiques** :\n  - **Principe du moindre privilège** : Le compte utilisateur de la base de données utilisé par PHP ne doit avoir que les permissions strictement nécessaires.\n  - **Mises à jour** : Maintenir le serveur web, PHP et le SGBD à jour.\n  - **Contrôles côté serveur** : La validation JavaScript côté client est utile pour l'expérience utilisateur, mais la seule validation fiable est celle effectuée côté serveur."
    },
    {
      "titre": "6. Configuration avancée (Exemple avec un Framework)",
      "resume": "Cette section, basée sur des exemples qui semblent provenir du framework CodeIgniter, aborde des configurations avancées pour les applications PHP.\n- **Réécriture d'URL (URL Rewriting)** : Utilisation d'un fichier `.htaccess` avec le module `mod_rewrite` d'Apache pour créer des URL \"propres\" et conviviales (sans `index.php`). Les directives clés sont `RewriteEngine On`, `RewriteCond` (conditions) et `RewriteRule` (règles de réécriture).\n- **Configuration du Framework** : Les fichiers de configuration (`config.php`, `database.php`, `autoload.php`) permettent de paramétrer le comportement de l'application :\n  - **URL** : Définir l'URL de base, supprimer `index.php` de l'URL, ajouter un suffixe (`.html`).\n  - **Langue** : Choisir la langue par défaut pour les messages du framework.\n  - **Sessions** : Configurer le nom du cookie de session, sa durée de vie, et choisir de stocker les données de session dans la base de données pour plus de sécurité et de flexibilité.\n  - **Base de données** : Centraliser les identifiants de connexion.\n  - **Chargement automatique (Autoload)** : Charger automatiquement les bibliothèques (`database`, `session`) et les assistants (`helpers` comme `url`) les plus utilisés pour qu'ils soient disponibles dans toute l'application."
    }
  ]
}
```