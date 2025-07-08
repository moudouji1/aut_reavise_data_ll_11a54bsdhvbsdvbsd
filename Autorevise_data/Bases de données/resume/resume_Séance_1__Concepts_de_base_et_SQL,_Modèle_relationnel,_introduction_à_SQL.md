# Séance 1 : Concepts de base et SQL, Modèle relationnel, introduction à SQL

## Résumé Général de la Séance

Cette séance d'introduction couvre les fondements des bases de données. Elle commence par identifier les problèmes des systèmes de fichiers traditionnels et présente l'approche "Base de Données" avec ses concepts de modélisation et l'architecture à trois niveaux (conceptuel, externe, interne). La séance explore ensuite l'algèbre relationnelle, le fondement théorique de SQL, en détaillant les opérations clés comme la projection et la restriction. Enfin, elle introduit le langage SQL, en couvrant son histoire, ses principaux langages (LDD, LMD, LCD), les types de données, la création de tables, la manipulation des données (`SELECT`, `INSERT`, `UPDATE`, `DELETE`), les jointures, les transactions, la gestion des vues et le contrôle des accès.

---

## 1. Introduction aux Bases de Données (BDD)

### ### Problèmes de la gestion de données traditionnelle
-   **Redondance de données** : Informations dupliquées sur plusieurs fichiers.
-   **Incohérence des données** : Mises à jour non synchronisées créant des contradictions.
-   **Difficulté d'interrogation** : Chaque nouvelle question nécessite un développement spécifique.
-   **Maintenance difficile** et coûts élevés.
-   Manque de gestion centralisée pour le **partage**, la **sécurité** et la **gestion des pannes**.

### ### L'approche "Bases de Données"
-   **Modélisation** des données pour représenter le monde réel de manière structurée.
-   **Centralisation et organisation** des données pour éliminer la redondance.
-   Utilisation d'un **Système de Gestion de Bases de Données (SGBD)** pour gérer :
    *   L'**interrogation** des données.
    *   La **cohérence** et l'**intégrité**.
    *   Le **partage** et les accès concurrents.
    *   La **sécurité** et la confidentialité.
    *   La **gestion des pannes**.

### ### Architecture à trois niveaux (ANSI-SPARC)
-   **Schéma Conceptuel** : Description logique globale des données de l'organisation, indépendante de l'implémentation physique (ex: Modèle Entité-Relation). Géré par l'**Administrateur de l'Organisation**.
-   **Schéma Interne** : Description de la représentation **physique** des données sur la machine (structures de fichiers, **index**). Géré par l'**Administrateur de la BD**.
-   **Schéma Externe** : Description d'une **vue partielle** de la base de données pour un utilisateur ou une application spécifique. Permet l'**indépendance logique**. Géré par l'**Administrateur des Applications**.

---

## 2. Le Modèle Relationnel et son Algèbre

### ### Concepts Fondamentaux
-   Le modèle relationnel, base théorique de SQL, a été proposé par **E. F. Codd** en 1970.
-   **Relation** : Représentée par une **table** à deux dimensions.
-   **Tuple** : Une **ligne** de la table, représentant un enregistrement.
-   **Attribut** : Une **colonne** de la table, caractérisée par un nom et un domaine.
-   **Domaine** : Ensemble des valeurs possibles pour un attribut.
-   **Clé primaire** : Un ou plusieurs attributs permettant d'identifier de manière **unique** chaque tuple. Une clé primaire ne peut pas contenir de valeur **NULL**.

### ### Opérations de l'Algèbre Relationnelle
-   Langage formel pour manipuler les relations. Une requête en algèbre relationnelle est traduite et optimisée par le SGBD.

#### #### Opérations ensemblistes (sur des relations de même schéma)
-   **UNION (∪)** : Fusionne deux relations en éliminant les doublons.
-   **INTERSECTION (∩)** : Conserve uniquement les tuples présents dans les deux relations.
-   **DIFFÉRENCE (-)** : Conserve les tuples de la première relation qui ne sont pas dans la seconde.

#### #### Opérations algébriques spécifiques
-   **PROJECTION (π)** : Sélectionne certaines **colonnes** (attributs) d'une relation et élimine les lignes en double.
-   **RESTRICTION (σ)** ou **SÉLECTION** : Sélectionne les **lignes** (tuples) d'une relation qui satisfont un critère donné.
-   **PRODUIT CARTÉSIEN (X)** : Combine chaque tuple d'une relation avec chaque tuple d'une autre, créant une nouvelle relation avec tous les attributs des deux.
-   **JOINTURE (⨝)** : Combine un produit cartésien avec une restriction pour lier des relations sur des attributs communs.
    -   **Équi-jointure** : Jointure basée sur l'égalité.
    -   **Jointure naturelle** : Équi-jointure sur tous les attributs de même nom, avec suppression des colonnes dupliquées.
    -   **Jointure externe (OUTER JOIN)** : Conserve tous les tuples d'une ou des deux tables, même s'il n'y a pas de correspondance dans l'autre table (en complétant avec des valeurs **NULL**). Types : `LEFT`, `RIGHT`, `FULL`.
-   **DIVISION (÷)** : Opération complexe utilisée pour des requêtes de type "tous les...".

---

## 3. Introduction au Langage SQL

### ### Origines et Évolutions
-   **SQL** (Structured Query Language) est un langage **déclaratif** : on exprime ce que l'on veut obtenir, pas comment l'obtenir.
-   Standardisé par l'ISO/ANSI :
    -   **SQL-86, SQL-89** : Versions initiales.
    -   **SQL2 (SQL-92)** : Version relationnelle complète, largement supportée.
    -   **SQL3 (SQL-99)** : Ajout de concepts objets, triggers, requêtes récursives.

### ### Composants du Langage SQL
-   **Langage de Définition de Données (LDD)** : `CREATE`, `ALTER`, `DROP` (pour tables, vues, index...).
-   **Langage de Manipulation de Données (LMD)** : `SELECT`, `INSERT`, `UPDATE`, `DELETE`.
-   **Langage de Contrôle de Données (LCD)** : `GRANT`, `REVOKE` (gestion des droits) et `COMMIT`, `ROLLBACK` (gestion des transactions).

### ### Types de Données Courants
-   **Numériques** : `INT` (ou `INTEGER`), `SMALLINT`, `DECIMAL(p, d)`, `FLOAT`, `DOUBLE`.
-   **Chaînes de caractères** :
    -   `CHAR(n)` : Longueur fixe.
    -   `VARCHAR(n)` : Longueur variable.
-   **Dates et Heures** : `DATE`, `TIME`, `TIMESTAMP`.

---

## 4. Langage de Définition de Données (LDD)

### ### Gestion des Tables
-   **`CREATE TABLE`** : Crée une nouvelle table.
    ```sql
    CREATE TABLE VINS (
        NV INT PRIMARY KEY,
        CRU VARCHAR(20) NOT NULL,
        MILLESIME INT,
        PRIX INT DEFAULT 40,
        NVT INT REFERENCES VITICULTEURS(NVT)
    );
    ```
-   **Contraintes d'intégrité** :
    -   `NOT NULL` : La colonne ne peut pas contenir de valeur nulle.
    -   `UNIQUE` : Assure que toutes les valeurs dans la colonne sont uniques.
    -   `PRIMARY KEY` : Combinaison de `NOT NULL` et `UNIQUE` pour identifier chaque ligne.
    -   `FOREIGN KEY ... REFERENCES` : Crée un lien entre deux tables (intégrité référentielle).
        -   `ON DELETE CASCADE` : Supprime les lignes dépendantes.
        -   `ON DELETE SET NULL` : Met à `NULL` les clés étrangères dépendantes.
    -   `CHECK` : Vérifie qu'une valeur respecte une condition.
    -   `DEFAULT` : Attribue une valeur par défaut si aucune n'est fournie.
-   **`ALTER TABLE`** : Modifie la structure d'une table (ajouter, supprimer, modifier une colonne ou une contrainte).
-   **`DROP TABLE`** : Supprime une table et toutes ses données.

### ### Vues (Views)
-   Une **vue** est une table virtuelle basée sur le résultat d'une requête SQL.
-   Permet de simplifier les requêtes complexes, de restreindre l'accès aux données et d'assurer l'indépendance logique.
-   **`CREATE VIEW NomVue AS SELECT ...`**
-   Les mises à jour via une vue sont soumises à des restrictions (pas de `GROUP BY`, d'agrégats, etc.).
-   La clause `WITH CHECK OPTION` garantit que les insertions/modifications via la vue respectent sa condition `WHERE`.

### ### Index
-   Un **index** est une structure de données qui améliore la vitesse des opérations de recherche sur une table.
-   Créé le plus souvent sur les colonnes utilisées dans les clauses `WHERE` et les jointures.
-   **`CREATE INDEX NomIndex ON NomTable (colonne1, ...);`**

---

## 5. Langage de Manipulation de Données (LMD)

### ### `SELECT` : Interroger les données
-   **Syntaxe de base** :
    ```sql
    SELECT [DISTINCT] colonne1, colonne2, ...
    FROM table1
    [WHERE condition]
    [GROUP BY colonne(s)]
    [HAVING condition_groupe]
    [ORDER BY colonne [ASC|DESC]];
    ```
-   **Clauses principales** :
    -   `SELECT` : Spécifie les colonnes à retourner. `DISTINCT` pour éliminer les doublons.
    -   `FROM` : Spécifie la ou les tables sources.
    -   `WHERE` : Filtre les lignes selon une condition. Opérateurs : `=`, `!=`, `>`, `<`, `LIKE`, `IN`, `BETWEEN`, `IS NULL`.
    -   `JOIN` : Combine les lignes de deux ou plusieurs tables (`INNER`, `LEFT`/`RIGHT OUTER`).
    -   `GROUP BY` : Regroupe les lignes ayant les mêmes valeurs dans des lignes de résumé.
    -   `HAVING` : Filtre les résultats des groupes (s'utilise après `GROUP BY`).
    -   `ORDER BY` : Trie les résultats.

### ### Fonctions d'Agrégation (avec `GROUP BY`)
-   `COUNT()` : Compte le nombre de lignes.
-   `SUM()` : Calcule la somme des valeurs.
-   `AVG()` : Calcule la moyenne.
-   `MIN()` / `MAX()` : Retourne la valeur minimale/maximale.

### ### Requêtes Imbriquées (Sous-requêtes)
-   Une requête `SELECT` à l'intérieur d'une autre requête.
-   Peut être utilisée dans les clauses `WHERE`, `HAVING`, `FROM`.
-   Opérateurs courants : `IN`, `NOT IN`, `EXISTS`, `ANY`, `ALL`.

### ### `INSERT`, `UPDATE`, `DELETE`
-   **`INSERT INTO table (col1, col2) VALUES (val1, val2);`** : Ajoute une nouvelle ligne.
-   **`UPDATE table SET col1 = val1 WHERE condition;`** : Modifie des lignes existantes.
-   **`DELETE FROM table WHERE condition;`** : Supprime des lignes.

---

## 6. Contrôle et Gestion Avancée

### ### Transactions
-   Une **transaction** est une séquence d'opérations exécutée comme un bloc unique et logique.
-   Propriétés **ACID** :
    -   **A**tomicité : Soit toutes les opérations réussissent, soit aucune n'est appliquée.
    -   **C**ohérence : La transaction amène la base d'un état valide à un autre.
    -   **I**solation : Les transactions concurrentes n'interfèrent pas les unes avec les autres.
    -   **D**urabilité : Une fois qu'une transaction est validée (`COMMIT`), ses effets sont permanents.
-   **Commandes de transaction** :
    -   `COMMIT` : Valide définitivement les modifications.
    -   `ROLLBACK` : Annule toutes les modifications depuis le début de la transaction.

### ### Confidentialité et Contrôle d'Accès (LCD)
-   **`GRANT`** : Accorde des privilèges (ex: `SELECT`, `INSERT`, `UPDATE`) sur des objets (tables, vues) à des utilisateurs.
    ```sql
    GRANT SELECT, UPDATE(DEGRE) ON VINS TO DUPONT;
    ```
-   **`REVOKE`** : Retire des privilèges accordés.
    ```sql
    REVOKE ALL ON VINS FROM DUPONT;
    ```
-   L'option `WITH GRANT OPTION` permet à un utilisateur de transmettre les droits qu'il a reçus.

### ### Déclencheurs (Triggers)
-   Un **trigger** est une procédure stockée qui est exécutée automatiquement en réponse à un événement (`INSERT`, `UPDATE`, `DELETE`) sur une table.
-   Modèle **ECA** (Événement - Condition - Action).
-   Permet d'implémenter une logique métier complexe, des contraintes d'intégrité avancées ou des audits.