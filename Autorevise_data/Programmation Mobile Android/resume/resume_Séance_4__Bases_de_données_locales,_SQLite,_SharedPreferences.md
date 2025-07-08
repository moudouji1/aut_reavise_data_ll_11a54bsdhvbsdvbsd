## Séance 4 : Bases de données locales, SQLite, SharedPreferences

Cette séance explore les deux principales méthodes de stockage de données localement sur un appareil Android. Elle couvre les **SharedPreferences** pour le stockage simple de paires clé-valeur (idéal pour les paramètres) et **SQLite** pour la gestion de données structurées et complexes via une base de données relationnelle.

### Introduction à la persistance des données
- **Objectif** : Sauvegarder des données pour qu'elles survivent à la fermeture de l'application.
- **Pourquoi ?** Permettre un fonctionnement hors ligne, sauvegarder les préférences de l'utilisateur, conserver l'état de l'application.
- **Options principales sur Android** : Fichiers, **SharedPreferences**, et **SQLite**.

---

### ## SharedPreferences : Stockage simple clé-valeur

Idéal pour stocker des données primitives et légères comme les préférences utilisateur, les réglages ou des indicateurs (flags).

#### ### Fonctionnement
*   **1. Obtenir une instance**
    - On récupère un fichier de préférences (créé s'il n'existe pas) avec `getSharedPreferences("NomDuFichier", MODE_PRIVATE)`.

*   **2. Écrire des données**
    - Utiliser un objet `SharedPreferences.Editor` pour modifier les données.
    - Ajouter des valeurs avec les méthodes `put...()` (ex: `putString("clé", "valeur")`, `putBoolean("tuto_vu", true)`).
    - **Crucial** : Valider les changements avec `apply()` ou `commit()`.
        - `apply()` est **asynchrone** et recommandé.
        - `commit()` est **synchrone** et bloque l'interface utilisateur.

*   **3. Lire des données**
    - Utiliser les méthodes `get...()` sur l'instance de SharedPreferences (ex: `prefs.getString("clé", "valeur_par_défaut")`).
    - Il est **essentiel de fournir une valeur par défaut** au cas où la clé n'existerait pas encore.

#### ### Avantages et Limites
*   **Avantages** : Très **simple** et **rapide** à mettre en œuvre pour des données non structurées.
*   **Limites** : Ne convient **pas aux données volumineuses ou complexes**. Aucune possibilité de faire des requêtes ou d'établir des relations entre les données.

---

### ## SQLite : Base de données relationnelle

SQLite est un moteur de base de données complet, puissant et intégré à Android, qui permet de gérer des données structurées en tables, lignes et colonnes à l'aide du langage **SQL**.

#### ### Concepts Clés
*   **Le Contrat (Contract Class)**
    - Une classe qui agit comme un **schéma** public pour votre base de données.
    - Elle définit les **noms de table** et les **noms de colonnes** sous forme de constantes.
    - C'est une **bonne pratique** pour centraliser la structure et éviter les erreurs de frappe.

*   **SQLiteOpenHelper**
    - Une classe d'aide qui gère le cycle de vie de la base de données.
    - Elle simplifie la **création** et la **mise à jour** de la BDD.
    - **Méthodes à surcharger :**
        - `onCreate(db)` : Exécutée **une seule fois** à la création de la base de données. C'est ici qu'on exécute les requêtes `CREATE TABLE ...`.
        - `onUpgrade(db, oldVersion, newVersion)` : Exécutée lorsque le numéro de version de la BDD augmente. Permet de **migrer les données** ou de mettre à jour le schéma.

#### ### Opérations CRUD (Create, Read, Update, Delete)

*   **Obtenir la base de données**
    - `getWritableDatabase()` pour les opérations d'écriture (INSERT, UPDATE, DELETE).
    - `getReadableDatabase()` pour les opérations de lecture (SELECT).

*   **1. Créer (Create / `insert`)**
    - On utilise un objet `ContentValues` pour associer des valeurs aux colonnes.
    - On appelle `db.insert(NOM_TABLE, null, values)` pour insérer une nouvelle ligne.

*   **2. Lire (Read / `query`)**
    - La méthode `db.query(...)` est utilisée pour interroger la base.
    - Elle retourne un objet `Cursor`, qui est un **pointeur sur l'ensemble des résultats**.
    - On parcourt les résultats avec une boucle `while(cursor.moveToNext()) { ... }`.
    - **TRÈS IMPORTANT** : Toujours **fermer le curseur** avec `cursor.close()` dans un bloc `finally` pour libérer la mémoire.

*   **3. Mettre à jour (Update / `update`)**
    - La méthode `db.update()` modifie les lignes existantes.
    - Elle utilise une clause **`WHERE`** pour cibler les lignes à mettre à jour.

*   **4. Supprimer (Delete / `delete`)**
    - La méthode `db.delete()` supprime des lignes.
    - Elle utilise également une clause **`WHERE`** pour cibler les lignes à supprimer.

---

### ## Résumé Comparatif

*   **SharedPreferences**
    - **Usage** : Données simples, préférences, réglages.
    - **Format** : Clé-valeur.
    - **Points forts** : **Simple** et **rapide**.

*   **SQLite**
    - **Usage** : Données d'application **structurées**, volumineuses ou relationnelles (ex: contacts, inventaire, articles).
    - **Format** : Tables, lignes, colonnes.
    - **Points forts** : **Robuste**, **structuré** et permet des **requêtes complexes** via SQL.