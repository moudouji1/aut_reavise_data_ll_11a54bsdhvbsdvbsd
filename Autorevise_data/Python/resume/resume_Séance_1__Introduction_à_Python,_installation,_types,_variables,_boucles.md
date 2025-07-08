Cette séance d'introduction à Python vous a permis de découvrir les origines du langage, ses avantages, et comment mettre en place votre environnement de développement. Vous avez appris à déclarer des variables, à manipuler les types de données de base (nombres, chaînes de caractères, booléens) et à utiliser les opérateurs. Enfin, la séance a couvert les structures de contrôle fondamentales que sont les boucles `for` et `while` pour exécuter des actions de manière répétitive.

## 1. Introduction à Python

### ### Un peu d'histoire
- **Créateur** : Guido van Rossum, en 1989.
- **Origine du nom** : Inspiré de la troupe comique "Monty Python's Flying Circus".
- **Philosophie** : Langage de programmation **objet**, **interprété**, **open source** et de **haut niveau**.
- **Communauté** : Supporté par une large communauté, utilisé par des entreprises comme Google, NASA, YouTube.

### ### Pourquoi utiliser Python ?
- **Qualité** : Produit du code **évolutif** et **maintenable**.
- **Productivité** : Syntaxe **claire et concise**, qui permet de développer rapidement.
- **Portabilité** : Le même code fonctionne sur de nombreuses plateformes (Windows, macOS, Linux).
- **Intégration** : S'intègre facilement avec d'autres langages (C, C++, Java).
- **Caractéristiques clés** :
    - Langage **interprété** (pas de compilation).
    - **Typage dynamique** (pas de déclaration de type explicite).
    - Gestion **automatique de la mémoire**.

### ### Le Zen de Python
Une série de principes guidant le développement en Python, accessible via la commande `import this`.
- *Beautiful is better than ugly.* (Le beau est préférable au laid.)
- *Explicit is better than implicit.* (L'explicite est préférable à l'implicite.)
- *Simple is better than complex.* (Le simple est préférable au complexe.)

## 2. Installation et Environnement

### ### Installation de Python
- **Site officiel** : [python.org](https://www.python.org) est la source principale pour télécharger Python.
- **Anaconda** : Une distribution populaire qui inclut Python et de nombreuses bibliothèques pour la **Data Science** (Numpy, Pandas, etc.).
- **Versions** : Le cours se base sur **Python 3**. Les versions 2 et 3 sont incompatibles.

### ### Exécuter du code Python
- **Mode interactif (REPL)** : Lancez `python` ou `python3` dans un terminal pour exécuter des commandes ligne par ligne. Idéal pour tester rapidement.
- **Scripts** :
    - Écrivez votre code dans un fichier avec l'extension `.py` (ex: `mon_script.py`).
    - Exécutez le fichier depuis le terminal avec la commande : `python mon_script.py`.

## 3. Les Bases du Langage

### ### Variables et Affectation
- Une **variable** est un nom associé à une valeur en mémoire.
- L'affectation se fait avec le signe **`=`**.
- Python est sensible à la casse : `age`, `Age` et `AGE` sont trois variables différentes.
```python
# Assigner une valeur à une variable
age = 25
nom = "Alice"

# Réaffecter une nouvelle valeur
age = 26

# Affectations multiples
a, b = 10, 20
```

### ### Mots-clés réservés
- Certains mots sont réservés par le langage et ne peuvent pas être utilisés comme noms de variables (ex: `if`, `for`, `while`, `def`, `class`).

### ### L'importance de l'indentation
- Python n'utilise **pas d'accolades (`{}`)** pour délimiter les blocs de code (boucles, conditions, fonctions).
- Les blocs de code sont définis par l'**indentation** (le décalage vers la droite).
- La convention est d'utiliser **4 espaces** pour chaque niveau d'indentation. Une indentation incohérente provoquera une `IndentationError`.

```python
x = 10
if x > 5:
    print("x est supérieur à 5") # Cette ligne est indentée, elle fait partie du bloc if
print("Fin du programme") # Cette ligne n'est pas indentée
```

### ### Commentaires
- Les commentaires permettent d'expliquer le code. Ils sont ignorés par l'interpréteur.
- Un commentaire sur une seule ligne commence par le symbole **`#`**.
- Les commentaires multi-lignes sont encadrés par des triples guillemets `""" ... """` ou `''' ... '''`.

## 4. Types de Données Fondamentaux

### ### Nombres
- **Entiers (`int`)** : Nombres entiers sans partie décimale (ex: `10`, `-5`, `0`).
- **Flottants (`float`)** : Nombres à virgule (ex: `3.14`, `-0.5`). Le séparateur est le **point (`.`)**.
- **Complexes (`complex`)** : Nombres complexes avec une partie réelle et une partie imaginaire (ex: `3 + 4j`).

### ### Chaînes de caractères (`str`)
- Représentent du texte.
- Définies avec des guillemets simples (`'...'`) ou doubles (`"..."`).

### ### Booléens (`bool`)
- Ne peuvent avoir que deux valeurs : **`True`** (Vrai) ou **`False`** (Faux).
- Utilisés principalement pour les conditions.

### ### Le type `None`
- Représente l'**absence de valeur**. C'est souvent la valeur de retour par défaut d'une fonction qui ne retourne rien explicitement.

### ### Conversion de types (typage)
- Il est possible de convertir une valeur d'un type à un autre à l'aide de fonctions dédiées.
- `int(valeur)` : Convertit en entier.
- `float(valeur)` : Convertit en flottant.
- `str(valeur)` : Convertit en chaîne de caractères.

```python
x = "100"
y = int(x) # y vaut maintenant l'entier 100
```

## 5. Opérateurs

### ### Opérateurs arithmétiques
- **`+`** : Addition
- **`-`** : Soustraction
- **`*`** : Multiplication
- **`/`** : Division (résultat toujours `float`)
- **`//`** : Division entière (partie entière du résultat)
- **`%`** : Modulo (reste de la division entière)
- **`**`** : Puissance (ex: `2 ** 3` donne 8)

### ### Opérateurs de comparaison
- **`==`** : Égal à
- **`!=`** : Différent de
- **`<`** : Strictement inférieur à
- **`>`** : Strictement supérieur à
- **`<=`** : Inférieur ou égal à
- **`>=`** : Supérieur ou égal à

### ### Opérateurs logiques
- **`and`** : ET logique (vrai si les deux conditions sont vraies).
- **`or`** : OU logique (vrai si au moins une des conditions est vraie).
- **`not`** : NON logique (inverse la valeur booléenne).

## 6. Structures de Contrôle : Les Boucles

### ### La boucle `for`
- Permet d'itérer sur les éléments d'une **séquence** (liste, tuple, chaîne de caractères, etc.).
- **`range(n)`** : Génère une séquence de nombres de 0 à `n-1`. Très utile avec les boucles `for`.
- **`enumerate(sequence)`** : Permet d'obtenir à la fois l'index et la valeur de chaque élément pendant l'itération.

```python
# Itérer sur une liste
fruits = ["pomme", "banane", "cerise"]
for fruit in fruits:
    print(fruit)

# Itérer 5 fois avec range
for i in range(5):
    print(f"Répétition numéro {i}")

# Itérer avec index et valeur
for index, fruit in enumerate(fruits):
    print(f"Le fruit à l'index {index} est {fruit}")
```

### ### La boucle `while`
- Répète un bloc de code **tant qu'une condition est vraie**.
- Il faut s'assurer que la condition deviendra fausse à un moment donné pour éviter une **boucle infinie**.

```python
compteur = 0
while compteur < 5:
    print(f"Le compteur est à {compteur}")
    compteur += 1 # Incrémentation pour éviter une boucle infinie
```

### ### Instructions `break` et `continue`
- **`break`** : Permet de **sortir immédiatement** de la boucle en cours.
- **`continue`** : Permet de **passer à l'itération suivante** de la boucle sans exécuter le reste des instructions du bloc.