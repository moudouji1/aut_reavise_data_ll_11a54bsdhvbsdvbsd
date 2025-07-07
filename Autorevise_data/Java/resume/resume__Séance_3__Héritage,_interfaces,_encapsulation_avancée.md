```json
{
  "titre_session": "Séance 3 : Héritage, interfaces, encapsulation avancée",
  "resume_general": "Cette séance aborde les concepts fondamentaux de la programmation orientée objet en Java, notamment l'héritage, le polymorphisme, les interfaces et les classes abstraites. Elle couvre également des mécanismes avancés comme l'encapsulation, la visibilité des membres, et l'utilisation de mots-clés essentiels tels que `super`, `this`, et `final`.",
  "themes": [
    {
      "titre": "1. Encapsulation et Visibilité des Membres",
      "contenu": [
        {
          "sous_titre": "Principe",
          "points_cles": [
            "L'encapsulation est un principe de la POO qui consiste à contrôler l'accès aux membres (attributs et méthodes) d'une classe depuis l'extérieur.",
            "Java utilise des modificateurs d'accès pour définir 4 niveaux de visibilité."
          ]
        },
        {
          "sous_titre": "Niveaux de visibilité",
          "points_cles": [
            "`public`: Le membre est accessible depuis n'importe quelle autre classe.",
            "`protected`: Le membre est accessible au sein du même paquetage, ainsi que par les sous-classes (même si elles sont dans un autre paquetage).",
            "Par défaut (aucun mot-clé) ou 'friendly': Le membre est accessible uniquement par les classes du même paquetage (package-private).",
            "`private`: Le membre est accessible uniquement à l'intérieur de la classe où il est déclaré."
          ]
        }
      ]
    },
    {
      "titre": "2. Héritage",
      "contenu": [
        {
          "sous_titre": "Définition et Mise en œuvre",
          "points_cles": [
            "L'héritage permet à une classe (dite 'sous-classe' ou 'classe fille') de réutiliser les attributs et méthodes non-privés d'une autre classe (dite 'super-classe' ou 'classe mère').",
            "Il se met en œuvre avec le mot-clé `extends`. Exemple : `public class Automobile extends Vehicule {}`.",
            "Java ne supporte pas l'héritage multiple pour les classes : une classe ne peut hériter que d'une seule autre classe.",
            "Toute classe qui n'étend pas explicitement une autre classe hérite implicitement de la classe `Object`, la racine de toute la hiérarchie de classes en Java."
          ]
        },
        {
          "sous_titre": "Constructeurs et Héritage",
          "points_cles": [
            "Le constructeur d'une sous-classe appelle implicitement le constructeur sans argument (`super()`) de sa super-classe.",
            "Si la super-classe ne possède pas de constructeur sans argument, une erreur de compilation se produit.",
            "Dans ce cas, il faut appeler explicitement un autre constructeur de la super-classe en utilisant `super(...)`, qui doit être la toute première instruction du constructeur de la sous-classe."
          ]
        },
        {
          "sous_titre": "Le mot-clé `super`",
          "points_cles": [
            "Permet d'accéder aux membres (attributs ou méthodes) de la super-classe.",
            "Utile pour appeler la version d'une méthode de la classe mère qui a été redéfinie : `super.nomDeLaMethode();`.",
            "Indispensable pour appeler un constructeur spécifique de la classe mère : `super(arguments);`."
          ]
        },
        {
          "sous_titre": "Le mot-clé `this`",
          "points_cles": [
            "Désigne l'instance courante de la classe (l'objet lui-même).",
            "Sert à lever l'ambiguïté entre un attribut de classe et un paramètre de méthode ayant le même nom : `this.valeur = valeur;`.",
            "Dans une classe interne, `NomClasseExterne.this` permet d'accéder à l'instance de la classe qui l'englobe."
          ]
        },
        {
          "sous_titre": "Interdire l'héritage et la redéfinition : Le mot-clé `final`",
          "points_cles": [
            "Une classe déclarée `final` ne peut pas être étendue (aucune classe ne peut en hériter).",
            "Une méthode déclarée `final` ne peut pas être redéfinie (overridden) dans les sous-classes.",
            "Un attribut déclaré `final` est une constante : sa valeur ne peut être assignée qu'une seule fois."
          ]
        }
      ]
    },
    {
      "titre": "3. Polymorphisme et Conversion de Type (Cast)",
      "contenu": [
        {
          "sous_titre": "Définition du Polymorphisme",
          "points_cles": [
            "Le polymorphisme signifie qu'un même service (méthode) peut avoir des comportements différents selon le type réel de l'objet sur lequel il est appliqué.",
            "Il est rendu possible par le fait qu'une variable de type super-classe peut référencer un objet de n'importe laquelle de ses sous-classes."
          ]
        },
        {
          "sous_titre": "Surclassement (Upcasting) et Déclassement (Downcasting)",
          "points_cles": [
            "**Upcasting (implicite)** : Affecter un objet de sous-classe à une référence de super-classe. `Personne p = new Employe();`",
            "Lorsqu'un objet est 'upcasté', ses fonctionnalités accessibles sont limitées à celles définies dans le type de la référence (la super-classe).",
            "**Downcasting (explicite)** : Convertir une référence de super-classe vers un type de sous-classe. Nécessite une conversion explicite (cast). `Employe e = (Employe) p;`",
            "Le downcasting est risqué : il provoque une erreur `ClassCastException` à l'exécution si l'objet n'est pas réellement du type de la sous-classe.",
            "L'opérateur `instanceof` permet de vérifier le type réel d'un objet avant de faire un downcasting pour éviter cette erreur."
          ]
        }
      ]
    },
    {
      "titre": "4. Interfaces et Classes Abstraites",
      "contenu": [
        {
          "sous_titre": "Interfaces",
          "points_cles": [
            "Une interface est un contrat qui définit un ensemble de méthodes qu'une classe doit obligatoirement implémenter.",
            "Une classe utilise le mot-clé `implements` pour appliquer une ou plusieurs interfaces. C'est le moyen pour une classe de participer à plusieurs 'hiérarchies de type', simulant un héritage multiple de comportement.",
            "Une interface peut elle-même hériter de plusieurs autres interfaces avec le mot-clé `extends`."
          ]
        },
        {
          "sous_titre": "Classes Abstraites",
          "points_cles": [
            "Déclarées avec le mot-clé `abstract`, elles se situent entre une interface et une classe concrète.",
            "Elles ne peuvent pas être instanciées directement.",
            "Elles peuvent contenir à la fois des méthodes abstraites (sans corps, que les sous-classes devront définir) et des méthodes concrètes (avec une implémentation).",
            "Leur but principal est de factoriser du code commun à plusieurs sous-classes tout en forçant l'implémentation de certains comportements spécifiques."
          ]
        }
      ]
    },
    {
      "titre": "5. Concepts Associés",
      "contenu": [
        {
          "sous_titre": "Surcharge de Méthodes (Overloading)",
          "points_cles": [
            "À ne pas confondre avec la redéfinition (Overriding) de l'héritage.",
            "La surcharge consiste à définir, dans la même classe, plusieurs méthodes portant le même nom mais avec des signatures différentes (le nombre ou le type des paramètres change).",
            "Le compilateur choisit quelle version appeler en fonction des arguments fournis."
          ]
        },
        {
          "sous_titre": "Classes Internes Statiques",
          "points_cles": [
            "C'est une classe déclarée avec le mot-clé `static` à l'intérieur d'une autre classe.",
            "Elle n'est pas liée à une instance de la classe externe et ne peut donc accéder qu'aux membres `static` de celle-ci.",
            "Utile pour regrouper logiquement des classes qui ne sont utilisées que dans un contexte précis."
          ]
        }
      ]
    }
  ]
}
```