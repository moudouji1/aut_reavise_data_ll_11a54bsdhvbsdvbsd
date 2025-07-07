```json
{
  "titre_seance": "Séance 4 : Collections et gestion des exceptions",
  "resume_general": "Cette séance aborde deux concepts fondamentaux en Java : les collections, qui sont des structures de données pour stocker et manipuler des groupes d'objets, et la gestion des exceptions, un mécanisme robuste pour traiter les erreurs qui surviennent durant l'exécution d'un programme.",
  "sections": [
    {
      "titre": "Les Collections en Java",
      "contenu": [
        {
          "sous_titre": "Introduction aux Collections",
          "points_cles": [
            "Les collections sont des objets conçus pour regrouper et gérer d'autres objets.",
            "Elles fournissent des implémentations de structures de données classiques comme les listes, piles, et tableaux associatifs.",
            "Le framework est basé sur un ensemble d'interfaces (ex: `Collection`, `List`, `Map`) qui définissent les comportements, et des classes concrètes (ex: `ArrayList`, `HashMap`) qui les implémentent.",
            "Toutes les classes et interfaces du framework des collections se trouvent dans le package `java.util`."
          ]
        },
        {
          "sous_titre": "Principaux Types de Collections",
          "types": [
            {
              "nom": "Les Listes (Interface List)",
              "description": "Collection ordonnée d'éléments où les doublons sont autorisés. Les éléments sont accessibles via un index numérique (position).",
              "implementations_communes": "ArrayList (tableau dynamique, rapide pour l'accès par index), LinkedList (liste chaînée, rapide pour les ajouts/suppressions en début/fin de liste).",
              "methodes_courantes": [
                "add(element): Ajoute un élément à la fin de la liste.",
                "get(index): Récupère l'élément à l'index spécifié.",
                "remove(index): Supprime l'élément à l'index spécifié.",
                "size(): Retourne le nombre d'éléments dans la liste."
              ]
            },
            {
              "nom": "Les Tableaux Associatifs (Interface Map)",
              "description": "Collection de paires clé-valeur. Chaque clé doit être unique et est utilisée pour retrouver la valeur associée.",
              "implementations_communes": "HashMap (non synchronisé, plus performant, autorise une clé et des valeurs `null`), Hashtable (plus ancien, synchronisé, n'autorise pas de `null`).",
              "methodes_courantes": [
                "put(cle, valeur): Associe une valeur à une clé.",
                "get(cle): Récupère la valeur associée à une clé.",
                "remove(cle): Supprime l'entrée pour une clé donnée.",
                "containsKey(cle): Vérifie si la map contient la clé spécifiée.",
                "keySet(): Retourne un `Set` (ensemble) de toutes les clés."
              ]
            },
            {
              "nom": "Les Piles (Classe Stack)",
              "description": "Structure de données LIFO (Last-In, First-Out), signifiant que le dernier élément ajouté est le premier à être retiré.",
              "methodes_specifiques": [
                "push(element): Ajoute (empile) un élément au sommet de la pile.",
                "pop(): Retire (dépile) et retourne l'élément au sommet de la pile.",
                "peek(): Retourne l'élément au sommet sans le retirer.",
                "empty(): Vérifie si la pile est vide."
              ]
            }
          ]
        },
        {
          "sous_titre": "Parcourir une Collection",
          "points_cles": [
            "**Boucle 'for-each'**: La méthode la plus simple et lisible pour parcourir tous les éléments. Syntaxe : `for (Type element : collection) { ... }`.",
            "**Itérateur (Iterator)**: Objet qui permet de parcourir une collection élément par élément. Méthodes principales : `hasNext()` (vérifie s'il reste des éléments) et `next()` (retourne l'élément suivant). C'est le seul moyen sûr de supprimer des éléments pendant un parcours.",
            "**Parcours optimisé des Maps**: Pour parcourir à la fois les clés et les valeurs, il est plus performant d'itérer sur l'ensemble des entrées (`map.entrySet()`) que d'itérer sur les clés (`map.keySet()`) et d'appeler `map.get(key)` à chaque itération."
          ]
        }
      ]
    },
    {
      "titre": "La Gestion des Exceptions",
      "contenu": [
        {
          "sous_titre": "Principes Généraux",
          "points_cles": [
            "Une exception est un signal indiquant qu'un problème ou une situation anormale est survenu pendant l'exécution du programme.",
            "Le but est de gérer ces erreurs proprement pour éviter que l'application ne plante et pour maintenir un état stable.",
            "En Java, les exceptions sont des objets héritant de la classe `Throwable`.",
            "La hiérarchie principale de `Throwable` se divise en `Error` (erreurs fatales de la JVM, généralement non gérables) et `Exception` (erreurs applicatives qu'un programmeur peut et doit souvent anticiper et gérer)."
          ]
        },
        {
          "sous_titre": "Le Mécanisme try-catch-finally",
          "mots_cles": [
            {
              "mot": "try",
              "usage": "Encadre un bloc de code susceptible de lever une exception. C'est la zone 'surveillée'."
            },
            {
              "mot": "catch",
              "usage": "Suit un bloc `try` et 'attrape' un type spécifique d'exception pour la traiter. Un `try` peut être suivi de plusieurs `catch` pour gérer différents types d'erreurs."
            },
            {
              "mot": "finally",
              "usage": "Définit un bloc de code qui s'exécute toujours, qu'une exception ait été levée ou non. Il est principalement utilisé pour libérer des ressources (ex: fermer un fichier ou une connexion réseau)."
            }
          ]
        },
        {
          "sous_titre": "Lancer et Propager des Exceptions",
          "mots_cles": [
            {
              "mot": "throw",
              "usage": "Instruction pour lancer manuellement une exception. Exemple : `throw new IllegalArgumentException(\"L'âge doit être positif\");`"
            },
            {
              "mot": "throws",
              "usage": "Mot-clé utilisé dans la signature d'une méthode pour déclarer qu'elle peut propager une exception à la méthode qui l'appelle. La méthode appelante devient alors responsable de la gestion de cette exception."
            }
          ]
        },
        {
          "sous_titre": "Types d'Exceptions et Exemples",
          "points_cles": [
            "**Checked Exceptions (vérifiées)**: Doivent obligatoirement être gérées (`try-catch`) ou déclarées (`throws`). Exemples : `IOException`, `FileNotFoundException`. Le compilateur vérifie leur gestion.",
            "**Unchecked Exceptions (non vérifiées)**: Héritent de `RuntimeException`. Ne nécessitent pas de gestion obligatoire, car elles signalent souvent des erreurs de logique du programmeur. Exemples : `NullPointerException` (accès à un objet `null`), `ArrayIndexOutOfBoundsException` (accès à un index de tableau invalide), `ArithmeticException` (division par zéro), `ClassCastException` (tentative de conversion de type invalide)."
          ]
        }
      ]
    }
  ]
}
```