# 🟠 Séance 5 : Application complète

Cette séance est une plongée pratique dans la supervision, le test et la création d'applications web complètes. Elle aborde la surveillance avancée d'une application NodeJS avec Keymetrics, explore les stratégies de test logiciel (notamment avec Jest), et guide l'étudiant à travers la construction de plusieurs projets concrets avec Vue.js et jQuery, de l'interface jusqu'à la base de données.

## Supervision d'application NodeJS avec Keymetrics

### ### Qu'est-ce que Keymetrics ?
- Un outil de **supervision** qui permet d'afficher des **statistiques** et des métriques remontées par **`pm2`**.
- Offre une interface web pour monitorer en temps réel la santé et les performances de vos applications.

### ### Mise en place
- **Inscription** : Se fait sur le site [keymetrics.io](https://keymetrics.io/).
- **Lien avec PM2** :
    - La liaison se fait via une commande simple dans le terminal :
    - `$ pm2 link [CLÉ_PRIVÉE] [CLÉ_PUBLIQUE] [NOM_DU_SERVEUR]`

### ### Ajout de sondes personnalisées (Probes)
- **Module `pmx`** : C'est le module qui permet d'envoyer des données métier personnalisées à Keymetrics.
    - Installation : `npm install --save pmx`.
- **Initialisation** : Il est recommandé de créer un **wrapper** (singleton) pour initialiser le module une seule fois dans l'application.
- **Quatre types de sondes** :
    - **`Simple metrics`** : Pour remonter une **valeur numérique** simple (ex: nombre d'utilisateurs connectés).
    - **`Counter`** : Pour **incrémenter** ou **décrémenter** une valeur (ex: nombre de tâches actives).
    - **`Meter`** : Pour mesurer une **fréquence** sur une période, comme un nombre de requêtes par seconde.
    - **`Histogram`** : Pour garder un **historique de valeurs** sur une période définie (ex: les temps de réponse des 5 dernières minutes).

## Le Test des Applications

### ### Types de Tests et Pyramide des Tests
- **Tests Unitaires** :
    - Valident une **petite portion de code isolée** (une fonction, un composant).
    - Ils sont **rapides**, nombreux et constituent la base de la pyramide.
- **Tests d'Intégration** :
    - Vérifient que **plusieurs unités fonctionnent correctement ensemble**.
- **Tests End-to-End (E2E)** :
    - Simulent un **parcours utilisateur complet** dans l'application, en pilotant un navigateur.
    - Ils sont **lents**, coûteux à maintenir et se situent au sommet de la pyramide.

### ### Tests d'instantanés (Snapshot) avec Jest
- **Jest** : Framework de test JavaScript populaire, notamment dans l'écosystème React.
- **Principe du Snapshot** :
    - Le test prend une "photographie" (un instantané) du rendu d'un composant.
    - Lors des exécutions suivantes, le nouveau rendu est comparé à l'instantané enregistré.
    - Si une différence est détectée, le test **échoue**. Le développeur doit alors :
        - **Accepter** le nouvel instantané si le changement était intentionnel.
        - **Corriger** le code si le changement est un bug.
- **Mise en place** :
    - Installer `react-test-renderer`.
    - Lancer les tests avec `npm test`.
- **Structure d'un fichier de test** :
    - **`describe('Suite de tests', ...)`** : Regroupe des tests liés à une même fonctionnalité.
    - **`it('cas de test', ...)`** ou **`test('cas de test', ...)`** : Définit un test unitaire.
    - **`expect(resultat).toMatchSnapshot()`** : L'assertion qui compare le composant à son instantané.

## Application Complète : Création d'une Web App avec Vue.js

### ### Étape 1 : Initialisation du Projet
- **Prérequis** : Installer **Node.js** et **NPM**.
- **Vue CLI** : Outil en ligne de commande pour créer et gérer des projets Vue.
    - Installation : `npm install -g @vue/cli`.
    - Création : `vue create mon-projet` (via la console) ou `vue ui` (via une interface graphique).

### ### Étape 2 : Structure et Concepts de Base
- **Composants `.vue`** : Fichiers contenant le **HTML** (`<template>`), le **JavaScript** (`<script>`) et le **CSS** (`<style>`) d'un élément d'interface.
- **Binding de données (`v-bind` ou `:`)** : Lie une variable du script à un attribut HTML.
- **Rendu de listes (`v-for`)** : Itère sur un tableau pour afficher une liste d'éléments.
    - *Important* : Toujours utiliser une **`:key`** unique pour chaque élément de la boucle.
- **Two-way data binding (`v-model`)** : Synchronise la valeur d'un champ de formulaire avec une variable du script.

### ### Étape 3 : Développement de l'Interface (UI) avec Vuetify
- **Vuetify** : Une bibliothèque de composants **Material Design** pour Vue.js.
- **Installation** : `vue add vuetify`.
- **Utilisation** : Permet de construire rapidement une interface professionnelle avec des composants prêts à l'emploi comme `<v-btn>`, `<v-card>`, `<v-dialog>`, `<v-text-field>`, etc.

### ### Étape 4 : Persistance des Données
- **Exemple avec Sheetsu** : Le TP utilise une feuille **Google Sheets** comme une base de données simplifiée via le service Sheetsu.
- **Opérations CRUD** (Create, Read, Update, Delete) :
    - **`Read`** : Lire les données de la feuille pour les afficher au chargement.
    - **`Create`** : Ajouter une nouvelle ligne dans la feuille.
    - **`Update`** : Modifier une ligne existante.
    - **`Delete`** : Supprimer une ligne.

## Ateliers Pratiques (TP) avec jQuery

### ### TP 1 : Mise en forme dynamique d'une page web
- **Objectif** : Créer un formulaire pour modifier dynamiquement le **style CSS** d'une page (couleur, police, gras, etc.).
- **Concepts** : Gestion d'événements (`.change()`, `.click()`), manipulation du CSS (`.css()`), et lecture des valeurs d'un formulaire (`.val()`).

### ### TP 2 : Création d'un jeu de course
- **Objectif** : Développer un jeu où le joueur doit éviter des voitures.
- **Concepts** : Animation en boucle (`.animate()`), gestion des **événements clavier** (`.keydown()`), détection de **collisions** par comparaison de coordonnées, et gestion des couches avec **`z-index`**.

### ### TP 3 : Création d'un jeu de collecte spatiale
- **Objectif** : Diriger un vaisseau pour collecter des objets et gérer un score.
- **Concepts** : Déplacement sur 8 axes, apparition **aléatoire** d'éléments, gestion du score et ajout d'une **musique de fond**.

### ### TP 4 : Création d'un Chat
- **Objectif** : Développer un chat simple en utilisant jQuery pour le front-end.
- **Concepts** : Envoi de données à un serveur (ici, un script **PHP**) et rafraîchissement périodique des messages avec `setInterval`.

## Conclusion et Rappels du Cours NodeJS

### ### Thèmes Abordés dans la Formation
- **Framework Express** :
    - Mise en place, **routes**, **fichiers statiques**, **middlewares**, et **moteurs de templates**.
- **Programmation Asynchrone** :
    - Utilisation de la librairie **`Async`** et des **promesses**.
- **Communication Temps Réel** :
    - Implémentation avec **`Socket.io`**.
- **Bases de données** :
    - Connexion et manipulation de bases **SQL** (MySQL, Postgres, etc.) et **NoSQL** (MongoDB, Redis).
- **Architecture Logicielle** :
    - Développement suivant le patron de conception **MVC** (Modèle-Vue-Contrôleur).
- **Déploiement et Supervision** :
    - Monitoring de l'application avec **`PM2`** et **`Keymetrics`**.