# Séance 4 : Transactions, Sécurité et Verrouillage

Cette séance explore les concepts fondamentaux de la gestion des transactions dans les bases de données. Elle commence par une transition du modèle relationnel vers l'objet-relationnel, puis détaille la notion de transaction et ses propriétés **ACID**. Les problèmes liés à l'exécution concurrente de plusieurs transactions sont présentés, ainsi que la solution principale : le **verrouillage**. Différents types de verrous, protocoles (comme le verrouillage à deux phases) et niveaux d'isolation en SQL sont expliqués. La séance se termine par une introduction à des sujets avancés tels que les transactions distribuées, les index multidimensionnels et textuels, et les règles d'association.

## Du Modèle Relationnel à l'Objet-Relationnel

### Atouts du modèle relationnel
- **Simplicité** : La base de données est vue comme un ensemble de tables.
- **Fondements formels** : Basé sur l'algèbre et le calcul relationnel, permettant l'optimisation des requêtes.
- **Conception structurée** : Méthodes de normalisation pour concevoir des schémas robustes.
- **Langage universel** : Le langage **SQL** est un standard.
- **Transactions sûres** : Le modèle garantit la sérialisabilité, notamment via le verrouillage à deux phases.

### Le compromis Objet-Relationnel (SQL:1999)
Pour dépasser les limites du relationnel, l'approche objet-relationnelle intègre des concepts objets.
- **Types définis par l'utilisateur (UDT)** : Permet de créer des types de données complexes et structurés.
- **Tables typées** : Une table peut être basée sur un type défini par l'utilisateur.
- **Héritage** : Une table peut hériter des attributs et des comportements d'une autre table.

### Étude de cas : PostgreSQL
- **Contrôle de concurrence multiversions (MVCC)** : Mécanisme où les lecteurs ne bloquent pas les écrivains et vice-versa, améliorant les performances en concurrence.
- **Types composites** : Permet de définir des attributs qui sont eux-mêmes des structures (similaires aux `struct` en programmation).
- **Héritage de tables** : Implémentation directe du concept d'héritage au niveau des tables.

## Le Concept de Transaction

### Définition
- Une transaction est une **unité de travail logique** qui fait passer la base de données d'un état **cohérent** à un autre.
- C'est une séquence d'opérations indivisible.
- **Événements principaux** : `start`, `read`, `write`, `commit` (valider), `rollback` (annuler).

### Propriétés ACID
- **A - Atomicité** : La transaction est une opération **"tout ou rien"**. Soit toutes ses modifications sont appliquées (**commit**), soit aucune ne l'est (**rollback**).
- **C - Cohérence** : La transaction garantit que la base de données respecte toutes les **contraintes d'intégrité** définies.
- **I - Isolation** : Chaque transaction s'exécute comme si elle était **seule** sur le système. Ses modifications intermédiaires sont invisibles aux autres transactions.
- **D - Durabilité** : Une fois qu'une transaction est validée (**commit**), ses modifications sont **permanentes** et survivent à toute panne ultérieure.

## Problèmes de Concurrence et Sérialisabilité

### Anomalies de concurrence
L'exécution simultanée de plusieurs transactions peut entraîner des problèmes :
- **Perte de mise à jour (Lost Update)** : La modification d'une transaction est écrasée par une autre transaction avant d'avoir pu être lue.
- **Lecture impropre (Dirty Read)** : Une transaction lit une donnée modifiée par une autre transaction qui n'a pas encore été validée (pas de `commit`). Si la seconde transaction est annulée, la première a lu une donnée qui n'a "jamais existé".
- **Lecture non reproductible (Non-Repeatable Read)** : Une transaction lit une même donnée plusieurs fois et obtient des valeurs différentes, car une autre transaction a modifié cette donnée entre-temps.
- **Objets fantômes (Phantom Reads)** : Une transaction exécute une requête plusieurs fois et obtient un ensemble de lignes différent, car une autre transaction a inséré ou supprimé des lignes qui correspondent aux critères de la requête.

### Sérialisabilité
- **Principe** : Le SGBD doit garantir que le résultat d'une exécution concurrente de transactions est **équivalent** au résultat d'une exécution en **série** (séquentielle) de ces mêmes transactions.
- **Opérations conflictuelles** : Deux opérations sont en conflit si elles appartiennent à des transactions différentes, portent sur la même donnée, et au moins l'une des deux est une opération d'**écriture** (`write`).
- Une exécution est **sérialisable** si l'ordre des opérations conflictuelles est préservé par rapport à une exécution en série.

## Le Verrouillage (Locking)

C'est la technique la plus courante pour assurer l'isolation et la sérialisabilité.

### Principe et Granularité
- **Principe** : Avant d'accéder à une donnée, une transaction doit obtenir un **verrou** sur celle-ci.
- **Granularité** : Fait référence à la taille de la donnée verrouillée (ex: une ligne, une page, une table, la base de données entière). Un compromis doit être trouvé entre la précision du verrouillage et le coût de sa gestion.

### Modes de Verrouillage
- **Verrou partagé (Shared - S)** : Demandé pour une **lecture**. Plusieurs transactions peuvent détenir un verrou S sur la même donnée simultanément.
- **Verrou exclusif (Exclusive - X)** : Demandé pour une **écriture** (modification, insertion, suppression). Si une transaction détient un verrou X, aucune autre transaction ne peut obtenir de verrou (ni S, ni X) sur cette donnée.

### Verrouillage à Deux Phases (2PL)
- Un protocole qui garantit la **sérialisabilité**.
- **Phase 1 (croissante)** : La transaction acquiert tous les verrous dont elle a besoin. Elle ne peut pas en libérer.
- **Phase 2 (décroissante)** : La transaction commence à libérer ses verrous. Elle ne peut plus en acquérir de nouveaux.
- En pratique, tous les verrous sont souvent conservés jusqu'au **`COMMIT`** ou **`ROLLBACK`** final.

### Interblocage (Deadlock)
- **Définition** : Situation où deux (ou plus) transactions s'attendent mutuellement. T1 attend un verrou détenu par T2, et T2 attend un verrou détenu par T1.
- **Résolution** :
    - **Prévention** : Imposer un ordre strict pour l'acquisition des verrous.
    - **Détection** : Le SGBD construit un **graphe d'attente** pour détecter les cycles. Si un cycle est détecté, une des transactions (la "victime") est choisie et annulée (`ROLLBACK`).

### Verrouillage à Granularité Multiple
- Combine des verrous à différents niveaux de granularité (table, page, ligne).
- Utilise des **verrous d'intention** pour signaler qu'un verrou plus fin est posé sur un descendant dans la hiérarchie.
- **Modes d'intention** :
    - **IS (Intention Shared)** : Intention de poser des verrous S sur des descendants.
    - **IX (Intention Exclusive)** : Intention de poser des verrous X sur des descendants.
    - **SIX (Shared with Intent Exclusive)** : La transaction lit toute la table (verrou S) et a l'intention de modifier certaines lignes (verrous X).

## Transactions en SQL

### Commandes de base
- Une transaction commence implicitement avec la première commande DML (`SELECT`, `INSERT`, etc.).
- **`COMMIT`** : Valide toutes les modifications de la transaction et les rend permanentes.
- **`ROLLBACK`** : Annule toutes les modifications effectuées depuis le début de la transaction.

### Niveaux d'Isolation
- Permettent de définir le degré d'isolation d'une transaction, en acceptant certaines anomalies pour de meilleures performances.
- Niveaux courants dans PostgreSQL :
    - **`READ COMMITTED`** (défaut) : Empêche les lectures impropres. Chaque commande voit une "photographie" de la base au moment où elle commence. Les lectures non reproductibles et les fantômes sont possibles.
    - **`SERIALIZABLE`** : Le niveau le plus strict. Garantit qu'aucune anomalie ne se produira. La transaction voit une "photographie" de la base au moment où la transaction entière a commencé.

### Verrouillage Explicite
- **`LOCK TABLE nom_table IN mode`** : Permet de verrouiller manuellement une table entière dans un mode spécifique.
- **`SELECT ... FOR UPDATE`** : Pose un verrou **exclusif (X)** sur les lignes sélectionnées.
- **`SELECT ... FOR SHARE`** : Pose un verrou **partagé (S)** sur les lignes sélectionnées.

### Points de Reprise (Savepoints)
- Permet de créer des marqueurs à l'intérieur d'une transaction pour y revenir sans annuler la transaction entière.
- **`SAVEPOINT nom_point;`** : Définit un point de reprise.
- **`ROLLBACK TO SAVEPOINT nom_point;`** : Annule les modifications effectuées depuis ce point de reprise.

## Introduction aux Sujets Avancés

### Transactions Distribuées
- **Contexte** : Une transaction qui s'exécute sur plusieurs bases de données (sites) distribuées.
- **Problème** : Comment garantir l'**atomicité** sur tous les sites ?
- **Solution** : Le protocole de **confirmation à deux phases (Two-Phase Commit - 2PC)**, qui implique un coordinateur et des participants pour s'assurer que tous les sites valident ou annulent la transaction de manière synchronisée.

### Index Multidimensionnels
- **Objectif** : Accélérer les requêtes portant sur plusieurs attributs (dimensions) simultanément.
- **Arbres k-d (k-dimensional trees)** : Structure d'arbre qui partitionne l'espace selon une dimension différente à chaque niveau.
- **Arbres R (R-trees)** : Structure d'arbre équilibrée (similaire aux arbres B+) optimisée pour les données spatiales. Elle indexe des "rectangles englobants" qui contiennent les objets.

### Index Textuels
- **Objectif** : Permettre une recherche rapide de mots ou de motifs dans de grands volumes de texte.
- **Tries (arbres préfixes)** : Chaque branche de l'arbre correspond à un mot, les arêtes étant étiquetées par des lettres.
- **Fichiers inversés** : Structure la plus courante. Associe à chaque mot une liste des documents où il apparaît (liste inverse). Les requêtes complexes sont résolues par des opérations sur ces listes (ex: intersection).

### Règles d'Association
- **Objectif** : Découvrir des relations intéressantes entre des ensembles d'items dans de grandes bases de données (ex: `si un client achète {pain, lait}, alors il achète aussi {beurre}`).
- **Concepts clés** :
    - **Support** : Fréquence d'apparition d'un ensemble d'items.
    - **Confiance** : Mesure de la force de la règle (probabilité conditionnelle).
- **Algorithme Apriori** : Algorithme classique pour extraire les ensembles d'items fréquents, qui servent ensuite à générer les règles.