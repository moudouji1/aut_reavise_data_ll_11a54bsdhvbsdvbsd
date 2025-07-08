# Séance 2 : Fonctions et manipulation des données

## Résumé général

Cette séance aborde les concepts fondamentaux de la programmation structurée et de la manipulation de données en Python. Elle couvre la définition et l'utilisation des **fonctions**, les **structures de contrôle** essentielles comme les boucles (`for`, `while`) et les conditions (`if`/`else`), ainsi que des techniques avancées pour manipuler les **chaînes de caractères**, notamment via les **expressions régulières**. La séance explore également l'interaction avec le **système de fichiers** et la lecture/écriture de données.

## Les Fonctions

Une fonction est un bloc de code réutilisable qui exécute une action spécifique.

- **Définition** : se définit avec le mot-clé `def`.
- **Paramètres** : une fonction peut accepter des entrées, appelées paramètres ou arguments.
  - Les paramètres peuvent avoir des **valeurs par défaut**, les rendant optionnels lors de l'appel.
  - Exemple : `def welcome(name, greeting='Hello'):`
- **Valeur de retour** : une fonction retourne toujours une valeur avec l'instruction `return`.
  - Si `return` n'est pas spécifié, la fonction renvoie **`None`** par défaut.
- **Fonctions anonymes (`lambda`)** : permettent de créer de petites fonctions sur une seule ligne, souvent utilisées comme arguments d'autres fonctions.
  - Syntaxe : `lambda arguments: expression`
  - Exemple : `(lambda x,y: x < y)`
- **Documentation (`docstring`)** : une chaîne de caractères placée juste après la définition de la fonction pour la documenter.
  - Accessible via l'attribut `__doc__` ou la fonction `help()`.
  - Exemple : `def ma_fonction(): """Ceci est un docstring.""" pass`

## Les Structures de Contrôle

### Conditions (`if`, `elif`, `else`)

Elles permettent d'exécuter différents blocs de code en fonction de conditions.

- La structure est **`if condition1:`**, suivie optionnellement de **`elif condition2:`** et/ou **`else:`**.
- Les conditions sont basées sur des **valeurs booléennes** (**`True`** ou **`False`**).
- **Opérateurs de comparaison** :
  - Égalité : **`==`**
  - Différence : **`!=`**
  - Inférieur/Supérieur : **`<`**, **`>`**, **`<=`**, **`>=`**

### Boucles (`for`, `while`)

Elles permettent de répéter l'exécution d'un bloc de code.

- **Boucle `for`** : pour itérer sur les éléments d'une séquence (liste, tuple, chaîne de caractères).
  - Syntaxe : `for element in sequence:`
  - **`range(n)`** est très utilisé pour effectuer une boucle un nombre de fois défini. `range(6)` génère les nombres de 0 à 5.
  - **`enumerate(sequence)`** permet de récupérer à la fois l'index et la valeur de chaque élément.
- **Boucle `while`** : s'exécute tant qu'une condition reste vraie.
  - Syntaxe : `while condition:`
- **Instructions de contrôle de boucle** :
  - **`break`** : pour sortir immédiatement d'une boucle.
  - **`continue`** : pour passer à l'itération suivante sans exécuter la fin du bloc.
- **Clause `else` dans les boucles** : le bloc `else` est exécuté à la fin de la boucle, sauf si celle-ci a été interrompue par un `break`.

## Manipulation des Données : Les Chaînes de Caractères (`str`)

### Propriétés de Base

- Les chaînes de caractères en Python sont des séquences **immuables** (non modifiables).
- La comparaison de chaînes se fait selon l'**ordre lexicographique** (ex: `'abc' < 'abd'`).

### Méthodes Utiles

- **Gestion de la casse** : `lower()`, `upper()`, `capitalize()`, `title()`.
- **Nettoyage** : `strip()` pour supprimer les espaces et sauts de ligne au début et à la fin.
- **Découpage et jonction** :
  - `split(separateur)` : découpe une chaîne en une **liste** de sous-chaînes.
  - `separateur.join(liste)` : assemble les éléments d'une liste en une **chaîne unique**.
- **Recherche** :
  - `find(motif)` : renvoie l'index de la première occurrence du motif (ou -1 si absent).
  - `count(motif)` : compte le nombre d'occurrences d'un motif.
- **Remplacement** : `replace(ancien_motif, nouveau_motif)`.

### Formatage

- **f-strings** (méthode moderne et recommandée) : `f"La valeur de pi est {math.pi:.2f}"`.
- **Méthode `.format()`** : `'La valeur est {}'.format(valeur)`.
- **Opérateur `%`** (plus ancien) : `"%s vaut %d" % ('age', 25)`.

### Slicing (Découpage en tranches)

- Permet d'extraire une partie d'une chaîne : `chaine[debut:fin:pas]`.
- Les indices peuvent être **négatifs** pour compter à partir de la fin (`chaine[-1]` est le dernier caractère).

## Expressions Régulières (Module `re`)

Le module `re` offre des outils puissants pour la recherche de motifs (patterns) dans du texte.

### Fonctions Clés

- Il est conseillé d'utiliser des **raw strings** (`r"..."`) pour définir les motifs.
- `re.search(pattern, chaine)` : trouve la **première occurrence** du motif n'importe où dans la chaîne.
- `re.match(pattern, chaine)` : ne cherche une correspondance qu'**au début** de la chaîne.
- `re.split(pattern, chaine)` : découpe la chaîne en utilisant le motif comme **séparateur**.
- `re.sub(pattern, remplacement, chaine)` : **remplace** toutes les occurrences du motif.
- `re.findall(pattern, chaine)` : trouve **toutes les occurrences** non chevauchantes et les retourne dans une liste.

### Optimisation et Groupes

- **`re.compile(pattern)`** : compile une expression régulière pour des utilisations répétées plus efficaces.
- Les parenthèses `()` dans un motif créent un **groupe**, ce qui permet de capturer des parties spécifiques du texte. On peut y accéder avec `.group(index)` ou `.groups()`.

## Manipulation du Système de Fichiers (Modules `os` et `glob`)

### Module `os` et `os.path`

- Permet d'interagir avec le système d'exploitation.
- **`os.path.join(partie1, partie2)`** : construit un chemin de fichier de manière portable (gère les `/` et `\`).
- **`os.path.basename(chemin)`** : extrait le nom du fichier.
- **`os.path.dirname(chemin)`** : extrait le chemin du répertoire.
- **`os.path.exists(chemin)`** : vérifie si un fichier ou répertoire existe.
- **`os.path.isfile(chemin)`** et **`os.path.isdir(chemin)`** : testent si le chemin correspond à un fichier ou à un répertoire.

### Module `glob`

- **`glob.glob('*.txt')`** : trouve tous les fichiers correspondant à un motif simple en utilisant des jokers (`*`, `?`).

## Lecture et Écriture de Fichiers

### Ouverture et Fermeture

- La syntaxe **`with open('fichier.txt', 'mode') as f:`** est la pratique recommandée, car elle garantit que le fichier est automatiquement fermé, même en cas d'erreur.
- **Modes d'ouverture courants** :
  - **`'r'`** : **lecture** (read) – mode par défaut.
  - **`'w'`** : **écriture** (write) – écrase le contenu du fichier s'il existe.
  - **`'a'`** : **ajout** (append) – écrit à la fin du fichier sans effacer le contenu.
- Il est essentiel de spécifier l'encodage pour éviter les erreurs : **`encoding='utf-8'`**.

### Méthodes de Lecture et Écriture

- **`f.read()`** : lit l'intégralité du contenu du fichier.
- **`f.readline()`** : lit une seule ligne du fichier.
- **`f.readlines()`** : lit toutes les lignes et les retourne dans une liste.
- On peut aussi **itérer directement sur l'objet fichier** : `for ligne in f: ...`.
- **`f.write(texte)`** : écrit une chaîne de caractères dans le fichier.

## Autres Modules Utiles

### Module `math`

- Fournit des fonctions et constantes mathématiques de base.
- **Constantes** : `math.pi`, `math.e`.
- **Fonctions** : `math.sqrt()`, `math.cos()`, `math.sin()`, `math.log()`, `math.exp()`, `math.factorial()`.

### Module `json`

- Permet de travailler avec le format de données JSON.
- **`json.dump(data, file)`** : écrit un objet Python dans un fichier au format JSON.
- **`json.load(file)`** : lit un fichier JSON et le convertit en objet Python.