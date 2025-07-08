# Séance 3 : Requêtes SQL avancées, JOIN, GROUP BY, sous-requêtes

Cette séance aborde des concepts SQL avancés essentiels pour interroger des bases de données complexes. Les points clés sont les **jointures** pour combiner plusieurs tables, le regroupement de données avec **`GROUP BY`** et les fonctions d'agrégation, le filtrage de ces groupes avec **`HAVING`**, et l'utilisation de **sous-requêtes** pour construire des requêtes imbriquées et puissantes.

## Schéma de la base de données d'exemple

Pour illustrer les concepts, les exemples s'appuient sur une base de données de gestion éditoriale composée de plusieurs tables liées :
- **`auteurs`**: Informations sur les auteurs.
- **`éditeurs`**: Informations sur les maisons d'édition.
- **`titres`**: Informations sur les livres (prix, avance, etc.).
- **`titreauteur`**: Table de liaison qui associe les auteurs à leurs livres.
- **`ventes`**: Enregistre les commandes de livres par les magasins.
- **`magasins`**: Informations sur les points de vente.
- **`employés`**: Informations sur les employés des éditeurs.
- ... et d'autres tables de support (`droits_prévus`, `remises`, etc.).

## Fonctions et Opérateurs avancés

### Filtrage et Tri

- **`LIKE`**: Permet la recherche de **motifs** dans les chaînes de caractères (ex: `WHERE nom LIKE 'L%'`).
- **`BETWEEN`**: Sélectionne les valeurs comprises dans un **intervalle** (ex: `WHERE position BETWEEN 10 AND 100`).
- **`IN`**: Vérifie si une valeur correspond à l'une des valeurs d'une **liste** (ex: `WHERE pays IN ('FR', 'CH', 'BE')`).
- **`ORDER BY`**: Trie les résultats selon un ou plusieurs critères, de manière ascendante (`ASC`) ou descendante (`DESC`).

### Expressions et Fonctions

- Il est possible d'utiliser des **opérateurs arithmétiques** (`+`, `-`, `*`, `/`) dans les clauses `SELECT` et `WHERE` pour effectuer des calculs.
- Des **fonctions spécifiques** au SGBD peuvent être utilisées, comme `DATEDIFF()` pour calculer la différence entre deux dates.

## Regroupement de Données (`GROUP BY`)

### Principe du `GROUP BY`

- La clause **`GROUP BY`** est utilisée pour **regrouper des lignes** qui ont les mêmes valeurs dans une ou plusieurs colonnes, afin d'effectuer des calculs sur chaque groupe.
- Exemple : `SELECT type, ... FROM titres GROUP BY type;` regroupe tous les livres par leur type.

### Fonctions d'Agrégation

- Appliquées sur les groupes pour calculer une valeur unique.
- **`COUNT(*)`** ou **`COUNT(colonne)`**: Compte le nombre de lignes dans le groupe.
- **`SUM(colonne)`**: Calcule la **somme** des valeurs d'une colonne numérique.
- **`AVG(colonne)`**: Calcule la **moyenne** des valeurs.
- **`MAX(colonne)`** / **`MIN(colonne)`**: Trouve la valeur **maximale** ou **minimale**.

### Filtrage des Groupes (`HAVING`)

- La clause **`HAVING`** est utilisée pour **filtrer les groupes** après leur création, contrairement à `WHERE` qui filtre les lignes avant le regroupement.
- Elle s'utilise souvent avec une fonction d'agrégation.
- Exemple : `... GROUP BY type HAVING COUNT(*) > 1;` n'affiche que les types de livres ayant plus d'un titre.

## Travail sur plusieurs tables : Les Jointures (`JOIN`)

### Concept de Jointure

- L'opération de **jointure** permet de **combiner des lignes** de deux ou plusieurs tables en se basant sur une colonne commune (généralement une clé primaire et une clé étrangère).
- Elle est fondamentale pour extraire des informations réparties sur plusieurs tables.

### Syntaxes de Jointure

- **Syntaxe implicite (ancienne)** : `SELECT pnauteur, noméditeur FROM auteurs, éditeurs WHERE auteurs.ville = éditeurs.ville;`
- **Syntaxe explicite `JOIN` (recommandée)** : `SELECT pnauteur, noméditeur FROM auteurs JOIN éditeurs ON auteurs.ville = éditeurs.ville;`

## Les Sous-requêtes (Requêtes Imbriquées)

### Définition

- Une **sous-requête** est une instruction `SELECT` imbriquée à l'intérieur d'une autre instruction (`SELECT`, `WHERE`, `HAVING`, `INSERT`, `UPDATE`...).
- Elle est toujours placée **entre parenthèses `()`**.

### Types de Sous-requêtes

- **Sous-requête scalaire** : Renvoie **une seule valeur** (une ligne, une colonne). Peut être utilisée avec des opérateurs de comparaison simples (`=`, `>`, `<`).
    - *Exemple* : `WHERE prix = (SELECT MAX(prix) FROM titres)`
- **Sous-requête ensembliste** : Renvoie une **liste de valeurs**. Doit être utilisée avec des opérateurs ensemblistes.
    - **`IN`**: Vérifie si une valeur est présente dans la liste retournée.
    - **`EXISTS`**: Vérifie si la sous-requête retourne au moins une ligne.
    - **`ANY` / `ALL`**: Modifient un opérateur de comparaison (`=`, `>`) pour l'appliquer à la liste retournée par la sous-requête.

### Sous-requêtes dans la clause `SELECT`

- Une sous-requête peut être utilisée comme une **colonne calculée** pour afficher une information agrégée en lien avec la ligne principale.
- *Exemple* : `SELECT titre, (SELECT SUM(qt) FROM ventes WHERE ventes.idtitre = titres.idtitre) AS total_ventes FROM titres;`

## Mise à jour des données

### `INSERT`

- Permet d'**ajouter** une ou plusieurs lignes dans une table.
- **`INSERT INTO table VALUES (...)`**: Ajoute une ligne complète.
- **`INSERT INTO table (col1, col2) SELECT ...`**: Insère des données provenant d'une autre requête.

### `UPDATE`

- Permet de **modifier** des lignes existantes.
- **`UPDATE table SET colonne = nouvelle_valeur WHERE condition;`**.
- La condition `WHERE` est cruciale pour ne pas modifier toute la table.

## Autres Clauses utiles

### `UNION`

- L'opérateur **`UNION`** combine les résultats de deux ou plusieurs requêtes `SELECT` en un seul jeu de résultats, en éliminant les doublons.

### `COMPUTE`

- Clause (spécifique à certains SGBD comme SQL Server) qui ajoute des **lignes de résumé** (agrégats) directement dans le jeu de résultats, en plus des lignes de détail, souvent en conjonction avec `ORDER BY`.