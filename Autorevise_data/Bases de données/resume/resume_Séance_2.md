# Résumé de la Séance 2 : Modélisation, Diagrammes E/A, Normalisation

Cette séance aborde les concepts fondamentaux de la conception et de la gestion des bases de données. Elle couvre le parcours complet, de la modélisation conceptuelle avec les diagrammes Entité/Association (E/A) à la mise en œuvre d'un schéma relationnel normalisé, jusqu'à l'interrogation et la manipulation des données avec le langage SQL.

---

## Introduction aux bases de données

### Historique des modèles
- **Modèle Hiérarchique (années 60) :** Organisation des données en arborescence, avec des relations de type **père-fils**. Un fils ne peut avoir qu'un seul père.
- **Modèle Réseau :** Extension du modèle hiérarchique où une classe "fille" peut avoir **plusieurs mères**.
- **Modèle Relationnel (1970, Codd) :** Représentation unifiée de l'information sous forme de **tables** (relations). Il repose sur des fondements mathématiques solides (algèbre relationnelle) et offre une grande indépendance entre les données et les applications.

### Définitions Clés
- **Base de Données (BD) :** Un ensemble structuré de données, avec un minimum de redondance, pour satisfaire simultanément plusieurs utilisateurs.
- **Système de Gestion de Base de Données (SGBD) :** Un ensemble de logiciels permettant de décrire, stocker, interroger et gérer une base de données. Il assure :
    - La **description** et la **manipulation** des données.
    - La **sûreté** (sauvegarde, restauration).
    - La **sécurité** (gestion des droits d'accès).
    - L'**intégrité** (respect des règles et contraintes).
    - La **concurrence d'accès** (gestion des accès multiples).

### Avantages des SGBD (par rapport aux SGF)
- **Indépendance Données/Programmes :** La structure des données est séparée des applications. Une modification des données n'implique pas la réécriture des programmes.
- **Réduction de la redondance :** Les données sont centralisées et partagées, ce qui évite les duplications.
- **Cohérence des données :** La réduction de la redondance prévient les incohérences.
- **Partage et sécurité :** Contrôle centralisé de l'accès et du partage des données.

---

## Architecture des SGBD (ANSI/SPARC)

L'architecture de référence pour les SGBD, qui vise à séparer les vues des utilisateurs de la manière dont les données sont stockées physiquement.

### Les Trois Niveaux
- **Niveau Externe :** La **vue des utilisateurs**. Chaque utilisateur ou application a sa propre vue des données, souvent sous forme de **schémas externes** ou "vues".
- **Niveau Conceptuel :** La **vue logique globale** de la base de données. Il décrit toutes les informations contenues dans la base de manière abstraite, via un **schéma conceptuel**.
- **Niveau Interne :** La **vue physique**. Décrit comment les données sont réellement stockées sur les disques (fichiers, index, etc.) via un **schéma interne**.

### Les Indépendances
- **Indépendance Physique :** Permet de modifier le **schéma interne** (stockage physique) sans affecter le **schéma conceptuel**. *Exemple : ajouter un index pour améliorer les performances.*
- **Indépendance Logique :** Permet de modifier le **schéma conceptuel** sans avoir à modifier les **schémas externes** (les applications des utilisateurs). *Exemple : ajouter un nouvel attribut à une table.*

---

## Le Modèle Entité/Association (E/A)

Le modèle E/A est un modèle conceptuel qui permet de décrire la structure d'une base de données de manière abstraite et graphique.

### Concepts Fondamentaux
- **Entité :** Un objet du monde réel (concret ou abstrait) ayant une existence propre (ex: `CLIENT`, `PRODUIT`). Représentée par un **rectangle**.
- **Association :** Un lien sémantique entre deux ou plusieurs entités (ex: un `CLIENT` *passe* une `COMMANDE`). Représentée par une **ellipse**.
- **Attribut :** Une propriété décrivant une entité ou une association (ex: l'attribut `Nom` pour l'entité `CLIENT`).
- **Identifiant :** Un ou plusieurs attributs permettant d'identifier de manière **unique** une occurrence d'entité (ex: `NumClient`). Il est **souligné** dans le diagramme.
- **Cardinalités :** Un couple de valeurs **(min, max)** sur le lien entre une entité et une association, indiquant le nombre de fois (minimum et maximum) qu'une occurrence de l'entité peut participer à l'association.
    - `(0,n)` : facultatif, multiple
    - `(1,n)` : obligatoire, multiple
    - `(1,1)` : obligatoire, unique
    - `(0,1)` : facultatif, unique

### Concepts Spécifiques
- **Association réflexive :** Une association liant une entité à elle-même.
- **Généralisation/Spécialisation (Héritage) :** Relation "EST-UN" (`IS A`) où une entité (ex: `EMPLOYE`) est une généralisation d'entités plus spécifiques (ex: `PILOTE`).

---

## Le Modèle Relationnel

Le modèle relationnel est le modèle de données le plus répandu, utilisé par la majorité des SGBD modernes.

### Concepts de base
- **Relation :** Une **table** à deux dimensions.
- **Tuple :** Une **ligne** de la table, représentant un enregistrement.
- **Attribut :** Une **colonne** de la table.
- **Domaine :** L'ensemble des valeurs autorisées pour un attribut.
- **Clé primaire :** Un attribut (ou un groupe d'attributs) qui identifie de manière unique chaque tuple dans une relation.
- **Clé étrangère :** Un attribut dans une table qui fait référence à la clé primaire d'une autre table, établissant ainsi un lien entre elles.

### Traduction du Modèle E/A au Relationnel
- **Règle 1 (Entité) :** Chaque entité devient une **table**. L'identifiant de l'entité devient la **clé primaire** de la table.
- **Règle 2 (Association 1-N) :** La clé primaire de la table côté "1" est ajoutée comme **clé étrangère** dans la table côté "N".
- **Règle 3 (Association N-N) :** Une **nouvelle table** est créée (table de jonction). Sa clé primaire est composée des clés primaires des entités liées.
- **Règle 4 (Association 1-1) :** La clé primaire d'une des tables migre comme clé étrangère dans l'autre.

---

## La Normalisation

Processus visant à organiser les attributs dans les tables pour **minimiser la redondance** des données et éviter les anomalies de mise à jour, d'insertion et de suppression.

### Dépendance Fonctionnelle (DF)
- Une contrainte entre deux ensembles d'attributs. On dit que `Y` dépend fonctionnellement de `X` (noté `X -> Y`) si chaque valeur de `X` est associée à une et une seule valeur de `Y`.
- **Dépendance transitive :** Si `A -> B` et `B -> C`, alors `A -> C`.

### Les Formes Normales (FN)
- **1ère Forme Normale (1FN) :** Une table est en 1FN si tous ses attributs sont **atomiques** (indivisibles). Une cellule ne peut pas contenir une liste ou un ensemble de valeurs.
- **2ème Forme Normale (2FN) :** Une table est en 2FN si elle est en 1FN et si tous ses attributs non-clés dépendent **pleinement** de la clé primaire. *Cette règle s'applique surtout aux clés primaires composées.*
- **3ème Forme Normale (3FN) :** Une table est en 3FN si elle est en 2FN et s'il n'existe aucune **dépendance transitive** entre des attributs non-clés.
- **Forme Normale de Boyce-Codd (BCNF) :** Une forme plus stricte de la 3FN. Pour chaque dépendance fonctionnelle `X -> Y`, `X` doit être une super-clé.

---

## L'Algèbre Relationnelle

Un langage formel utilisé pour interroger les bases de données relationnelles. Les requêtes sont formées en appliquant des opérateurs à des relations.

### Opérateurs Principaux
- **Opérateurs ensemblistes :**
    - **Union (`∪`) :** Combine les tuples de deux relations compatibles.
    - **Différence (`-`) :** Renvoie les tuples qui sont dans la première relation mais pas dans la seconde.
    - **Intersection (`∩`) :** Renvoie les tuples communs aux deux relations.
- **Opérateurs relationnels :**
    - **Sélection (`σ`) :** Filtre les **lignes** (tuples) d'une relation en fonction d'une condition.
    - **Projection (`π`) :** Sélectionne certaines **colonnes** (attributs) d'une relation et élimine les doublons.
    - **Produit cartésien (`×`) :** Combine chaque tuple d'une relation avec chaque tuple d'une autre.
    - **Jointure (`⨝`) :** Combine des tuples de deux relations sur la base d'une condition. C'est l'opération la plus courante pour relier des tables (souvent un produit cartésien suivi d'une sélection).

---

## Le Langage SQL

**SQL (Structured Query Language)** est le langage standard pour interagir avec les SGBD relationnels.

### Sous-ensembles de SQL
- **LDD (Langage de Définition de Données) :** Pour définir et gérer la structure de la base.
    - `CREATE TABLE` : Crée une nouvelle table.
    - `ALTER TABLE` : Modifie la structure d'une table.
    - `DROP TABLE` : Supprime une table.
- **LMD (Langage de Manipulation de Données) :** Pour gérer les données dans les tables.
    - `INSERT INTO` : Ajoute de nouvelles lignes.
    - `UPDATE` : Modifie des lignes existantes.
    - `DELETE FROM` : Supprime des lignes.
- **LID (Langage d'Interrogation de Données) :** La commande `SELECT` est au cœur de ce langage.
    - `SELECT [colonnes]` : Spécifie les colonnes à retourner.
    - `FROM [tables]` : Spécifie les tables à interroger.
    - `WHERE [condition]` : Filtre les lignes.
    - `GROUP BY [colonne]` : Regroupe les lignes pour appliquer des fonctions d'agrégation (**COUNT, SUM, AVG, MIN, MAX**).
    - `HAVING [condition]` : Filtre les groupes créés par `GROUP BY`.
    - `ORDER BY [colonne]` : Trie les résultats.
- **LCD (Langage de Contrôle de Données) :** Pour gérer la sécurité et les permissions.
    - `GRANT` : Attribue des droits à un utilisateur.
    - `REVOKE` : Retire des droits.

---

## Concepts Avancés

### Transactions
- Une **transaction** est une séquence d'opérations exécutée comme une seule unité de travail logique. Elle est **atomique** : soit toutes les opérations réussissent, soit elles sont toutes annulées.
- `COMMIT` : Valide définitivement les modifications d'une transaction.
- `ROLLBACK` : Annule toutes les modifications effectuées depuis le début de la transaction.
- `SAVEPOINT` : Crée un point de retour à l'intérieur d'une transaction, permettant une annulation partielle via `ROLLBACK TO SAVEPOINT`.

### Déclencheurs (Triggers)
- Un **trigger** est une procédure stockée qui est exécutée **automatiquement** par le SGBD en réponse à un événement de manipulation de données (`INSERT`, `UPDATE` ou `DELETE`) sur une table spécifique.
- Ils sont utiles pour :
    - Maintenir l'intégrité des données complexes.
    - Automatiser des actions (ex: mettre à jour un stock après une vente).
    - Auditer les modifications.
- La syntaxe typique est `CREATE TRIGGER ... BEFORE/AFTER [événement] ON [table]`.