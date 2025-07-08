# Résumé de la Séance 5 : Bases de données, SQLite, APIs

Cette séance couvre les outils Python essentiels pour la manipulation de données, le calcul scientifique et la visualisation. Elle introduit ensuite le concept fondamental des bases de données relationnelles et montre comment interagir avec elles en pratique en utilisant le langage SQL via la bibliothèque `sqlite3` de Python pour créer des tables, insérer des données et effectuer des requêtes.

## Python : Outils pour la science des données

### NumPy : Calcul matriciel
- **`np.array`** : Structure de base pour le calcul matriciel.
- Opérations usuelles :
    - **`A + B`** : Somme de deux matrices.
    - **`A * B`** : Produit coefficient par coefficient (produit de Schur).
    - **`np.dot(A,B)`** ou **`A.dot(B)`** : Produit matriciel.
    - **`np.linalg.inv(A)`** : Inverse de la matrice A.
    - **`np.linalg.solve(A,b)`** : Résolution du système de Cramer Ax=b.
- Génération aléatoire (`numpy.random` alias `npr`) :
    - **`npr.randint(a,b)`** : Entier aléatoire entre `a` et `b-1`.
    - **`npr.random()`** : Réel aléatoire dans `[0,1[`.
    - **`npr.sample(n)`** : Tableau de `n` réels aléatoires dans `[0,1[`.

### SciPy : Calcul scientifique
- **`scipy.integrate.quad(f,a,b)`** : Calcule l'intégrale de la fonction `f` entre `a` et `b`.
- **`scipy.optimize.newton(f,a)`** : Résolution d'équation par la méthode de la sécante.
- **`scipy.integrate.odeint(f,y0,T)`** : Résolution de l'équation différentielle `y'=f(y,t)`.

### Matplotlib : Visualisation de données
- Le sous-module principal est **`matplotlib.pyplot`**, souvent importé avec l'alias `plt`.
- Fonctions clés :
    - **`plt.plot(L1, L2)`** : Trace une ligne brisée à partir des points de coordonnées (L1, L2).
    - **`plt.title("titre")`** : Définit le titre du graphique.
    - **`plt.grid()`** : Affiche une grille.
    - **`plt.legend()`** : Affiche la légende des courbes.
    - **`plt.savefig('nom.ext')`** : Sauvegarde le graphique dans un fichier.
    - **`plt.show()`** : Affiche le graphique à l'écran.
    - **`plt.matshow(T)`** : Affiche une matrice `T` sous forme d'image (pixels colorés).

### Autres modules utiles
- **Module `random`** :
    - **`random.randint(a,b)`** : Entier aléatoire entre `a` et `b` **inclus** (différent de NumPy).
    - **`sample(l,k)`** : Liste de `k` éléments distincts choisis aléatoirement dans la liste `l`.
- **Module `time`** :
    - **`time.perf_counter()`** : Donne l'heure précise en secondes, utile pour mesurer le temps d'exécution d'un code.

## Introduction aux bases de données relationnelles

- **Objectif** : Regrouper, ordonner et mettre à disposition de grandes quantités de données de manière structurée.
- **Structure** : Une **base de données (BDD) relationnelle** organise les données dans des tables (relations) pour permettre d'extraire facilement des informations spécifiques (requêtes).
- **Exemple** : Une BDD musicale peut contenir des tables pour les compositeurs, les œuvres, les instruments, etc., permettant de rechercher des œuvres par compositeur, date ou instrument.

## SQL et la bibliothèque `sqlite3`

### Le langage SQL (Structured Query Language)
- **Définition** : Langage standard pour créer, gérer et interroger des bases de données relationnelles.
- **Instructions principales** :
    - **`CREATE`** : Pour créer une nouvelle table dans la base.
    - **`INSERT`** : Pour ajouter de nouvelles lignes (enregistrements) dans une table.
    - **`SELECT ... FROM ... WHERE ...`** : Pour interroger la base et extraire des données selon des critères.
    - **`ALTER`** : Pour modifier la structure d'une table.
    - **`UPDATE`** : Pour mettre à jour des enregistrements existants.

### Utilisation en Python avec `sqlite3`
Le processus pour manipuler une base de données SQLite en Python est le suivant :

1.  **Importer la bibliothèque** : `import sqlite3`
2.  **Créer une connexion** : `connection = sqlite3.connect('nom_base.db')`
    - Crée une connexion à un fichier de base de données (le crée s'il n'existe pas).
3.  **Créer un curseur** : `cur = connection.cursor()`
    - Le **curseur** est un objet qui permet d'exécuter des commandes SQL.
4.  **Exécuter des requêtes SQL** : `cur.execute("... instruction SQL ...")`
    - L'instruction SQL est passée sous forme de chaîne de caractères.
5.  **Valider les modifications** : `connection.commit()`
    - Enregistre toutes les modifications (comme `INSERT`, `UPDATE`, `CREATE`) dans le fichier de la base.
6.  **Fermer la connexion** : `connection.close()`
    - Termine la session avec la base de données.

#### Exemple : Créer une table
```python
import sqlite3

# 1. & 2. Connexion à la base
connection = sqlite3.connect('musique.db')
# 3. Création du curseur
cur = connection.cursor()

# 4. Exécution d'une commande SQL pour créer une table
cur.execute("""
CREATE TABLE IF NOT EXISTS compositeur (
    idcomp varchar(6) NOT NULL,
    nom varchar(30) NOT NULL,
    prenom varchar(30) NOT NULL,
    naissance int(4),
    mort int(4),
    PRIMARY KEY (idcomp)
);
""")

# 5. Validation des changements
connection.commit()
# 6. Fermeture de la connexion
connection.close()
```
- **Récupérer les résultats** : Après une requête `SELECT`, le curseur `cur` devient un objet itérable. On peut parcourir les résultats avec une boucle `for`. Chaque ligne est retournée sous forme de **tuple**.