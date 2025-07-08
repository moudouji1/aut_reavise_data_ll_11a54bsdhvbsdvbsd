# Séance 3 : Structures de données et algorithmes fondamentaux

Cette séance offre une introduction complète aux structures de données et aux algorithmes fondamentaux en utilisant le langage Python. Elle aborde les concepts de base de la programmation, les types de collections de données (listes, tuples, dictionnaires, ensembles), la distinction entre objets mutables et immuables, et présente des algorithmes essentiels de tri et de recherche. La séance introduit également des structures plus avancées comme les piles, les files, les listes chaînées et les arbres, ainsi que des concepts clés tels que la récursivité et l'analyse de complexité.

## Les bases de la programmation en Python

### Comparaisons
- Les comparaisons de **chaînes de caractères** se font selon l'**ordre lexicographique** (`'abc' < 'abd'`).
- Les comparaisons de **listes** et **tuples** se font **élément par élément** de gauche à droite.

### Boucles
Il existe deux types de boucles, `for` et `while`, qui peuvent inclure une clause `else` (exécutée en fin de boucle si elle n'est pas interrompue par un `break`).
- **`break`** : sort de la boucle.
- **`continue`** : passe à l'itération suivante.

#### Boucle `for` (énumérée)
Parcourt les éléments d'une séquence (liste, tuple, chaîne).
- **`range(stop)`** : génère une séquence d'entiers de 0 à `stop-1`.
- **`range(start, stop)`** : génère une séquence de `start` à `stop-1`.
- **`range(start, stop, step)`** : génère une séquence avec un pas `step`.
- **`enumerate(sequence)`** : permet de parcourir une séquence tout en ayant l'indice et la valeur de chaque élément.

```python
# Parcourir une liste
for elt in ['hello', 'world']:
    print(elt)

# Parcourir avec l'indice et la valeur
for idx, val in enumerate(['hello', 'world']):
    print(idx, val)
```

#### Boucle `while` (conditionnelle)
S'exécute tant qu'une condition est vraie.
```python
while condition:
    # instructions
else:
    # exécuté si la boucle se termine normalement
```

### Fonctions (`def`)
- En Python, il n'y a que des **fonctions** (pas de procédures).
- Une fonction retourne toujours une valeur. Si aucun `return` n'est spécifié, elle retourne **`None`**.
- Les paramètres peuvent avoir des **valeurs par défaut**, les rendant optionnels.
- **Fonctions anonymes (`lambda`)** : fonctions courtes et simples, souvent utilisées comme arguments d'autres fonctions.
    `lambda arguments: expression`

### Documentation (`docstrings`)
- La documentation d'une fonction, classe ou module se place juste après sa définition, entre triples guillemets `"""..."""`.
- Elle est accessible via l'attribut `__doc__` ou la fonction `help()`.

## Structures de Données Fondamentales

### Chaînes de caractères (`str`)
- **Immuables** (non modifiables).
- S'écrivent avec des apostrophes (`'...'`), des guillemets (`"..."`) ou des triples guillemets (`"""..."""` pour les chaînes multi-lignes).
- L'accès aux caractères se fait par **indexation** (`ch[0]`) et **slicing** (`ch[1:5]`).
- **Méthodes utiles** :
    - `len(ch)` : longueur.
    - `c1 + c2` : concaténation.
    - `ch.split(sep)` : découpe la chaîne en une liste.
    - `sep.join(liste)` : joint les éléments d'une liste avec `sep`.
    - `ch.find(sub)` : trouve l'indice de la première occurrence de `sub` (-1 si non trouvée).
    - `ch.replace(old, new)` : remplace les occurrences.
    - `ch.format(...)` : formate la chaîne en insérant des valeurs.

### Listes (`list`)
- **Mutables** (modifiables).
- Séquence **ordonnée** d'éléments hétérogènes.
- Création : `[1, "a", 3.0]`
- Accès par **indexation** et **slicing**.
- **Compréhensions de listes** : syntaxe concise pour créer des listes.
  `[expression for item in iterable if condition]`
  - Exemple : `[i*i for i in range(5)]` -> `[0, 1, 4, 9, 16]`

### Tuples (`tuple`)
- **Immuables** (non modifiables).
- Séquence **ordonnée** d'éléments.
- Création : `(1, "a", 3.0)` ou `1, "a", 3.0`.
- **Attention** : un tuple à un seul élément doit avoir une virgule : `(1,)` ou `1,`.
- **Sequence Unpacking** : affectation multiple à partir d'un tuple.
  `prenom, nom = ('Jean', 'Dupont')`

### Dictionnaires (`dict`)
- **Mutables** (modifiables).
- Collection **non ordonnée** (avant Python 3.7) de paires **clé-valeur**.
- Les **clés** doivent être **uniques** et de type **immuable** (nombre, chaîne, tuple).
- Création : `{'nom': 'Dupont', 'age': 42}` ou `dict(nom='Dupont', age=42)`.
- **Opérations courantes** :
    - Accès : `d['clé']` (lève une `KeyError` si la clé n'existe pas).
    - Accès sécurisé : `d.get('clé', valeur_par_defaut)`.
    - Ajout / Modification : `d['nouvelle_clé'] = valeur`.
    - Suppression : `del d['clé']`.
    - `d.keys()` : retourne une vue des clés.
    - `d.values()` : retourne une vue des valeurs.
    - `d.items()` : retourne une vue des paires (clé, valeur), utile pour itérer.
- **`defaultdict`** (du module `collections`) : un dictionnaire qui fournit une valeur par défaut pour les clés inexistantes.

### Ensembles (`set`)
- **Mutables** (modifiables).
- Collection **non ordonnée** d'éléments **uniques** et **immuables**.
- Création : `{1, 2, 3}`. Pour un set vide, utiliser `set()`.
- **Opérations ensemblistes** :
    - `s.add(elt)` : ajoute un élément.
    - `s.remove(elt)` : enlève un élément (lève une `KeyError` si absent).
    - `s.discard(elt)` : enlève un élément sans erreur s'il est absent.
    - **Union** : `s1 | s2` ou `s1.union(s2)`.
    - **Intersection** : `s1 & s2` ou `s1.intersection(s2)`.
    - **Différence** : `s1 - s2` ou `s1.difference(s2)`.
    - **Différence symétrique** : `s1 ^ s2` ou `s1.symmetric_difference(s2)`.
- **`frozenset`** : version **immuable** d'un ensemble, peut être utilisée comme clé de dictionnaire.

## Mutabilité et Copie
- **Objets immuables** : `int`, `float`, `str`, `tuple`, `frozenset`. Leur valeur ne peut pas être changée après création.
- **Objets mutables** : `list`, `dict`, `set`. Peuvent être modifiés en place.
- **Copie superficielle (`copy.copy()` ou `[:]` pour les listes)** :
  - Crée un nouvel objet conteneur, mais copie les **références** vers les objets contenus.
  - Modifier un objet mutable à l'intérieur de la copie affectera l'original.
- **Copie profonde (`copy.deepcopy()`)** :
  - Crée une copie **récursive** de tous les objets.
  - La copie et l'original sont totalement indépendants.

## Algorithmes Élémentaires
### Algorithmes de Recherche
- **Recherche Séquentielle (linéaire)** :
  - Parcours de tous les éléments du tableau jusqu'à trouver l'objet.
  - Complexité : **O(n)**.
- **Recherche Dichotomique** :
  - Applicable uniquement sur un **tableau trié**.
  - Divise l'espace de recherche par deux à chaque étape.
  - Complexité : **O(log n)**.

### Algorithmes de Tri
- **Tri à Bulles** : Compare et permute les éléments adjacents de manière répétée.
- **Tri par Sélection** : Recherche le plus petit élément et le place à sa position correcte.
- **Tri par Insertion** : Construit le tableau trié un élément à la fois, en insérant chaque nouvel élément à sa place.
- **Tri par Fusion (Merge Sort)** :
  - Approche **diviser pour régner** : divise le tableau en deux, trie récursivement chaque moitié, puis fusionne les deux moitiés triées.
  - Complexité : **O(n log n)**.

## Concepts Algorithmiques et Structures Avancées

### Récursivité
- Une fonction est **récursive** si elle s'appelle elle-même.
- Nécessite un **cas de base** pour arrêter les appels.
- Exemple : calcul de la factorielle `n! = n * (n-1)!`.

### Types de Données Abstraits (TAD)
- Un TAD définit un ensemble de données et les opérations applicables, **indépendamment de l'implémentation**.
- Exemples : Piles, Files, Listes, Arbres.

### Piles (Stack)
- Structure de données **LIFO** (Last-In, First-Out, Dernier Entré, Premier Sorti).
- **Opérations** :
  - **`PUSH`** : ajouter un élément au sommet.
  - **`POP`** : retirer l'élément du sommet.

### Files (Queue)
- Structure de données **FIFO** (First-In, First-Out, Premier Entré, Premier Sorti).
- **Opérations** :
  - **`ENQUEUE`** : ajouter un élément à la fin.
  - **`DEQUEUE`** : retirer l'élément du début.

### Listes Chaînées
- Structure où les éléments (nœuds) ne sont pas contigus en mémoire.
- Chaque **nœud** contient une **donnée** et un **pointeur** vers le nœud suivant.
- Permet une gestion dynamique de la mémoire (taille variable, insertion/suppression efficace).

### Arbres
- Structure de données **hiérarchique** et non linéaire.
- Composée de **nœuds** reliés par des arêtes.
- **Terminologie** : racine, feuille, père, fils, profondeur, hauteur.
- **Arbre Binaire** : chaque nœud a au plus deux fils (gauche et droit).
- **Arbre Binaire de Recherche (ABR)** : pour tout nœud, les valeurs du sous-arbre gauche sont inférieures, et celles du sous-arbre droit sont supérieures.

### Graphes
- Structure composée de **sommets** (nœuds) et d'**arêtes** (liens).
- Peut être **orienté** (arcs) ou **non orienté** (arêtes).
- Permet de modéliser des réseaux (sociaux, routiers, etc.).