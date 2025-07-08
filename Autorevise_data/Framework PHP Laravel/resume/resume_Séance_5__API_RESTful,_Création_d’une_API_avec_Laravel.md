# Séance 5 : API RESTful, Création d’une API avec Laravel

Cette séance introduit la création d'une API RESTful. Elle aborde les opérations CRUD, les outils de débogage essentiels comme le profiler et l'inspection des routes, ainsi que les formats d'échange de données comme JSON et XML. **Note importante** : bien que le cours porte sur Laravel, les exemples de commandes fournis (`php bin/console`) sont spécifiques au framework Symfony. Les principes restent cependant similaires.

## Principes d'une API et Opérations CRUD

L'objectif est de créer une interface pour manipuler des données (par exemple, une entité `Personne`) via des requêtes HTTP.

### Génération d'un CRUD (Create, Read, Update, Delete)

-   Un **CRUD** est un ensemble d'opérations de base pour la gestion de données.
-   Des outils peuvent générer automatiquement le code nécessaire pour ces opérations.
-   La commande `php bin/console make:crud` (dans l'écosystème **Symfony**) crée :
    -   Un **contrôleur** pour gérer la logique des requêtes.
    -   Les **templates** (vues) pour afficher les formulaires et les listes.
-   Cela permet de gérer une entité, comme `App\Entity\Personne`, via une interface web.

## Outils de Développement et Débogage

### Profiler (Barre de débogage)

-   Le **profiler** est un outil essentiel pour analyser et déboguer une application.
-   Il s'installe via Composer : `composer req profiler`.
-   Il affiche des informations clés sur chaque requête :
    -   **Requêtes à la base de données** et leur durée.
    -   Performance (temps de chargement, mémoire utilisée).
    -   Informations sur les routes, la sécurité, etc.

### Gestion des Routes

-   Une **route** associe une URL et une méthode HTTP (GET, POST, etc.) à une action dans un contrôleur.
-   Pour lister toutes les routes de l'application (avec Symfony) : `php bin/console debug:router`.
-   Un CRUD pour une entité `personne` génère typiquement les routes suivantes :
    -   `GET /personne/` : Lister toutes les personnes (**index**).
    -   `GET, POST /personne/new` : Afficher le formulaire et créer une personne (**new**).
    -   `GET /personne/{id}` : Afficher une personne spécifique (**show**).
    -   `GET, POST /personne/{id}/edit` : Afficher le formulaire et mettre à jour une personne (**edit**).
    -   `DELETE /personne/{id}` : Supprimer une personne (**delete**).

### Sécurité

-   Il est crucial de vérifier la sécurité des dépendances (bundles, packages) de votre projet.
-   L'outil **security-checker** permet d'analyser les vulnérabilités connues.
-   Installation : `composer require sec-checker --dev`.

## Formats d'Échange de Données

-   Les API utilisent des formats standardisés pour envoyer et recevoir des données.
-   **JSON** (**JavaScript Object Notation**) : Format léger et lisible, c'est le standard le plus utilisé pour les API RESTful.
-   **XML** (**eXtensible Markup Language**) : Un autre format structuré, plus verbeux que JSON, mais toujours utilisé dans certains contextes.
-   PHP dispose de fonctions natives robustes pour manipuler (encoder et décoder) ces deux formats.