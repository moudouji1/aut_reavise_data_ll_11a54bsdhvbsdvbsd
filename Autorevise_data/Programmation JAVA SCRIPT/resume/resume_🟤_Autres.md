Ce document est une compilation de ressources sur diverses technologies de développement web. Il aborde les concepts fondamentaux de l'architecture web, les technologies côté serveur comme NodeJS et ASP.NET, ainsi que les principaux frameworks et librairies côté client tels que React, Angular et Vue.js. Il couvre également des sujets comme PHP, les bases de données, les outils de développement et les bonnes pratiques.

## I. Formation NodeJS (Avancé)

### ### Objectifs de la formation
- Apprendre et comprendre les différentes **méthodes asynchrones** de NodeJS.
- Concevoir un **projet d'envergure**.
- Comprendre le fonctionnement d'**Express**, un des frameworks les plus utilisés de NodeJS.
- Mettre en place une architecture **MVC** et une abstraction de base de données.
- Développer une application web de **niveau professionnel**.

### ### Public Concerné
- Étudiants, développeurs, chefs de projet.
- Passionnés de **nouvelles technologies**, d'**event-coding** et d'**asynchrone**.
- Projets nécessitant une architecture **robuste, scalable et modulaire** (Web ou back-end).

### ### Contenu de la Formation
- **Node et le Web : HTTP, Request & Express**
    - Périmètre du module **HTTP**.
    - Gestion des requêtes (`Request`).
    - Création d'un serveur web avec **Express**.
    - Routage des requêtes, gestionnaires de route, fichiers statiques et **middlewares**.
    - Utilisation de **moteurs de template**.
    - Projet pratique : `ChatWithMe`.
- **L'asynchrone en détail**
    - Gestion du **Callback Hell** & **Pyramid of Doom**.
    - Utilisation de la librairie **Async**.
    - Les **promesses** (avec la librairie Q) : fondamentaux, gestion des erreurs, flux, timers et I/O.
- **Communication temps réel**
    - Utilisation de **Socket.io**.
    - Intégration de Socket.io à **Express**.
    - Projet pratique : `ChatWithMe` (Parties 1 & 2).
- **Liaison avec la persistance des données**
    - Interaction avec des bases de données relationnelles (**MySQL**) et NoSQL (**Redis**, **MongoDB**).
    - Utilisation de l'ORM **Sequelize** pour les associations et l'intégration.
    - Intégration des bases de données au projet `ChatWithMe`.
- **Bonus**
    - Monitoring avec **PM2**.
    - Supervision avec **Keymetric**.

## II. Concepts Généraux du Développement Web

### ### Architecture Client/Serveur
- **Définition** : Modèle où des **clients** (navigateurs) demandent des services à un **serveur centralisé**.
- **Fonctionnement d'une requête web** :
    1.  L'utilisateur saisit une **URL**.
    2.  Le navigateur demande l'adresse IP au serveur **DNS**.
    3.  Le navigateur envoie une requête **HTTP/HTTPS** au serveur.
    4.  Le serveur renvoie les fichiers nécessaires (HTML, CSS, JS).
    5.  Le navigateur interprète les fichiers (DOM, CSS, JS) et affiche la page.
- **Protocole HTTP (Hypertext Transfer Protocol)** : Protocole de requête-réponse pour communiquer avec les serveurs web.
- **Méthodes HTTP courantes** :
    - `GET` : Récupérer une ressource.
    - `POST` : Créer une nouvelle ressource.
    - `PUT` : Mettre à jour une ressource existante.
    - `DELETE` : Supprimer une ressource.

### ### Langage de Script vs Langage Compilé
- **Langage compilé** : Le code est traduit en **code machine** avant l'exécution (ex: C, C++). Un **compilateur** crée un fichier exécutable.
- **Langage de script (interprété)** : Le code est traduit ligne par ligne au moment de l'exécution par un **interpréteur** (ex: JavaScript, Python, PHP).

### ### Front-end vs Back-end
- **Front-end (côté client)** :
    - Désigne l'**interface utilisateur** visible et interactive.
    - Technologies : **HTML**, **CSS**, **JavaScript** et frameworks (React, Angular, Vue.js).
- **Back-end (côté serveur)** :
    - Désigne le **serveur**, l'**application** et la **base de données**.
    - Gère la logique métier, le traitement des données et la sécurité.
    - Technologies : **Node.js**, **PHP**, **Python**, **Java**, **ASP.NET**.

## III. Frameworks et Librairies Front-End

### ### React.js
- **Présentation** : Une **librairie JavaScript** (gérée par Facebook) pour construire des interfaces utilisateur basées sur une hiérarchie de **composants composables**.
- **Concepts clés** :
    - **JSX** : Extension de syntaxe pour écrire du HTML dans JavaScript.
    - **Composants** : Morceaux de code réutilisables avec leur propre logique et état.
    - **State & Props** : Le `state` est l'état interne d'un composant, les `props` sont les données passées d'un parent à un enfant.
    - **Cycle de vie** : Méthodes exécutées à des moments spécifiques (ex: `componentDidMount` pour les appels AJAX).
    - **Hooks** : Fonctions (`useState`, `useEffect`) pour utiliser l'état et d'autres fonctionnalités React dans les composants fonctionnels.
    - **React Router** : Librairie pour gérer le routage dans une application monopage (SPA).
- **Bonnes pratiques** :
    - Utiliser `className` au lieu de `class` en JSX car `class` est un mot-clé réservé.
    - Les appels **AJAX** se font généralement dans la méthode de cycle de vie `componentDidMount()` ou avec le hook `useEffect`.
    - Les **Render Props** sont une technique pour partager du code entre composants via une fonction passée en prop.

### ### Angular
- **Présentation** : Un **framework open source** (géré par Google) pour construire des applications client en **HTML**, **CSS** et **TypeScript**.
- **Caractéristiques** :
    - **TypeScript** : Sur-ensemble de JavaScript qui ajoute un typage statique.
    - **Architecture MVC** : Modèle-Vue-Contrôleur pour une séparation claire des préoccupations.
    - **Écosystème complet** : Inclut des solutions pour le routage, la gestion des formulaires, les requêtes HTTP, etc.
    - **Évolution** : Angular (v2+) est une réécriture complète d'**AngularJS** (v1.x) pour de meilleures performances et une meilleure adéquation avec le web moderne (mobile, Web Components).

### ### Vue.js
- **Présentation** : Un **framework JavaScript progressif** et open-source créé par Evan You.
- **Caractéristiques** :
    - **Facile à prendre en main** : Très léger et simple à intégrer dans des projets existants.
    - **Data-binding réactif** : Lie les données de l'application au DOM de manière réactive.
    - **Composants réutilisables** : Permet de diviser l'application en petits composants autonomes.
    - **API de Composition (Composition API)** : Alternative à l'API d'Options (Options API) pour organiser la logique par fonctionnalité, inspirée par les hooks de React.
- **Approches de conception** :
    - **Test-Driven Development (TDD)** : Approche encouragée pour créer des applications maintenables.
    - **Renderless Components** : Composants qui gèrent la logique sans rendre de HTML, pour une réutilisabilité maximale.

### ### jQuery
- **Présentation** : Librairie JavaScript qui simplifie la manipulation du **DOM**, la gestion des **événements** et les requêtes **AJAX**. Bien que moins dominant aujourd'hui avec l'essor des frameworks modernes, il reste présent dans de nombreux projets.

## IV. Développement Back-End et Côté Serveur

### ### PHP
- **Présentation** : Langage de script côté serveur créé par **Rasmus Lerdorf**.
- **Caractéristiques** :
    - **Faiblement typé** et orienté objet.
    - **Interprété** avec un cache de bytecode (Zend Engine).
    - Très utilisé pour le développement web, notamment par des CMS comme **Wordpress** et **Drupal**.

### ### ASP.NET
- **Présentation** : Framework de développement **côté serveur** de Microsoft.
- **Évolution** :
    - **ASP (Active Server Pages)** : Première version, avec VBScript.
    - **ASP.NET Framework** : Intégration avec le Framework .NET, introduction des **Web Forms** (approche événementielle) puis **ASP.NET MVC**.
    - **ASP.NET Core** : Réécriture **open-source** et **multiplateforme** (Windows, Linux, macOS), fusionnant MVC et Web API.
- **Modèles de programmation** :
    - **Razor Pages** : Approche centrée sur les pages pour des scénarios simples, utilisant la syntaxe Razor.
    - **Blazor** : Framework pour créer des interfaces utilisateur interactives côté client avec C# au lieu de JavaScript, via **WebAssembly**.
    - **SignalR** : Pour la communication en temps réel.

## V. Outils et Bonnes Pratiques

### ### Outils de Débogage
- **Débogueurs de navigateur** (Chrome DevTools, Firebug) :
    - **Inspection du DOM** et modification des styles CSS.
    - **Traçage des requêtes réseau**.
    - **Exécution pas à pas** de code JavaScript, inspection des variables.
    - Visualisation et modification des **cookies** et du **localStorage**.

### ### Éditeurs de code en ligne
- Plateformes pour tester rapidement des extraits de code HTML/CSS/JS.
- Exemples : **JSFiddle**, **JSBin**, **CodePen**.

### ### Tests
- **Tests unitaires et d'intégration** : Essentiels pour assurer la qualité du code.
- **Librairies de test** :
    - **Jest** & **Enzyme** (pour React).
    - **Vue Testing Library** & **Vue Test Utils** (pour Vue.js).