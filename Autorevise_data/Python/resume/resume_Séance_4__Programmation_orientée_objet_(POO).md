Cette séance introduit les concepts fondamentaux de la programmation orientée objet (POO). Elle explique comment structurer le code autour d'objets qui regroupent des données (attributs) et des comportements (méthodes). Les notions de classe, d'instance, d'héritage et d'encapsulation sont abordées à travers des exemples pratiques, principalement en Python et avec l'environnement Alice.

## I. Les Fondamentaux de la POO

### 1. Classes, Objets et Instances
- La **Classe** : C'est un **plan** ou un **moule** pour créer des objets. Elle définit un ensemble d'attributs et de méthodes communs. Par convention, le nom d'une classe commence toujours par une **majuscule**.
- L'**Instance** (ou **Objet**) : C'est un exemplaire **concret** créé à partir d'une classe. C'est l'objet que l'on manipule dans le programme.
- **Instanciation** : C'est l'action de créer un objet (une instance) à partir d'une classe.
- On peut créer **plusieurs instances** d'une même classe. Chacune est indépendante et peut avoir des valeurs d'attributs différentes.

### 2. Attributs et Méthodes
- **Attributs** (ou *Properties*) : Ce sont les **variables** associées à un objet, qui définissent ses **caractéristiques** ou son état (ex: `couleur`, `nom`, `age`).
- **Méthodes** : Ce sont les **fonctions** associées à un objet, qui définissent ses **comportements** ou les actions qu'il peut effectuer (ex: `avancer()`, `dire()`, `calculer()`).

## II. Définir des Classes en Python

### 1. Le Constructeur `__init__()`
- C'est une méthode spéciale qui est **automatiquement appelée** lors de la création d'une instance.
- Son rôle principal est d'**initialiser les attributs** de l'objet.
- Le premier paramètre est toujours `self`, qui représente l'instance elle-même.

```python
class Personne:
    def __init__(self, nom, age):
        self.nom = nom  # Attribut d'instance
        self.age = age    # Attribut d'instance
```

### 2. Méthodes d'instance
- Ce sont les fonctions définies à l'intérieur d'une classe.
- Elles prennent toujours `self` comme premier paramètre, ce qui leur permet d'accéder aux attributs (`self.nom`) et autres méthodes de l'instance.

### 3. Utiliser des Paramètres dans les Méthodes
- Les méthodes peuvent accepter des **paramètres** (en plus de `self`) pour rendre le code plus **flexible** et **réutilisable**.
- Cela permet d'éviter de dupliquer du code pour des actions similaires mais avec des valeurs différentes.

```python
class Robot:
    def avancer(self, distance):
        print(f"Le robot avance de {distance} mètres.")
```

## III. Les 4 Piliers de la POO

### 1. L'Encapsulation
- C'est le principe de **regrouper les données (attributs) et les méthodes** qui les manipulent au sein d'un même objet.
- On peut contrôler l'accès aux attributs via des méthodes spécifiques :
    - **Getters** : Méthodes pour lire la valeur d'un attribut.
    - **Setters** : Méthodes pour modifier la valeur d'un attribut, souvent en y ajoutant une logique de contrôle (ex: vérifier qu'un âge n'est pas négatif).
- En Python, on utilise souvent le décorateur **`@property`** qui permet de définir des getters et setters tout en conservant une syntaxe d'accès simple (`objet.attribut`).

### 2. L'Héritage
- L'héritage permet à une classe (**classe enfant**) de **récupérer les attributs et méthodes** d'une autre classe (**classe parente**).
- Cela favorise la **réutilisation du code** et crée une hiérarchie entre les classes.
- La syntaxe en Python est `class Enfant(Parent):`.
- On utilise la fonction `super().__init__(...)` dans le constructeur de la classe enfant pour appeler le constructeur de la classe parente.

### 3. L'Abstraction
- Consiste à **cacher les détails complexes de l'implémentation** et à n'exposer que les fonctionnalités nécessaires à l'utilisateur.
- Une **classe abstraite** sert de modèle et ne peut pas être instanciée directement. Elle peut contenir des **méthodes abstraites** que ses classes enfants sont obligées de redéfinir.

### 4. Le Polymorphisme
- "Polymorphisme" signifie "plusieurs formes".
- C'est la capacité pour des objets de classes différentes de répondre à un **même message** (un même appel de méthode) de manière **spécifique**.
- Par exemple, une méthode `seDeplacer()` agira différemment pour un objet `Voiture` (rouler) et un objet `Oiseau` (voler).

## IV. Bonnes Pratiques et Concepts Utiles

### 1. Décomposer le code en méthodes
- Plutôt que d'écrire tout le code dans une seule grande méthode, il est préférable de **segmenter le problème** en plusieurs petites méthodes claires et spécifiques.
- Avantages :
    - **Lisibilité** et maintenance facilitées.
    - Permet le **travail en équipe**.
    - **Réutilisation** d'une même méthode si une action doit être répétée.

### 2. Méthodes de Classe vs Méthodes de Monde (Concept Alice)
- **Méthode de Classe (Class-Level)** : Spécifique à une classe. Elle ne peut être utilisée que par les instances de cette classe (ex: `penguin.wing_flap()`).
- **Méthode de Monde (World-Level)** : Commune à plusieurs classes. Elle permet de coordonner les actions de différents objets (ex: `rencontre(lievre, tortue)`).

### 3. Méthodes Spéciales (Magic Methods)
- En Python, ce sont des méthodes encadrées par des doubles tirets bas (ex: `__init__`). Elles permettent de surcharger le comportement par défaut des opérateurs.
- `__str__(self)` : Retourne une chaîne de caractères lisible pour l'utilisateur (`print(objet)`).
- `__repr__(self)` : Retourne une chaîne de caractères pour le débogage, représentant l'objet de manière non ambiguë.
- `__add__(self, other)` : Surcharge l'opérateur `+`.
- `__eq__(self, other)` : Surcharge l'opérateur de comparaison `==`.

### 4. Gestion des Erreurs (Exceptions)
- Il est crucial d'anticiper les erreurs qu'un utilisateur pourrait provoquer.
- Le bloc **`try...except`** permet de "tenter" une opération et de "capturer" une erreur si elle se produit, évitant ainsi que le programme ne plante.
- On peut gérer différents types d'erreurs (`ValueError`, `ZeroDivisionError`, etc.).
- Le mot-clé **`raise`** permet de déclencher volontairement une exception.