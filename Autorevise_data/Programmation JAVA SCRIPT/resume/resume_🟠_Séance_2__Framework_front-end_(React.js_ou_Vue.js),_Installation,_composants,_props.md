Voici un résumé structuré de la séance, prêt à être copié dans Notion ou Obsidian.

---

Cette séance couvre les fondamentaux des frameworks front-end, avec un focus sur React.js et Vue.js, ainsi qu'une introduction à Angular. Elle aborde l'installation, la structure de projet, et les concepts clés comme les composants, les props, l'état (state), le data-binding et les directives. La séance inclut également la mise en pratique de concepts backend avec un side-project de chat en temps réel (Node.js et Socket.io) et explore des patterns de conception avancés pour construire des applications robustes et maintenables.

## 🟠 Side Project : ChatWithMe (Backend)

### ### Objectif
- Intégrer **socket.io** pour une communication en temps réel dans une application de chat.

### ### Arborescence et Requêtes
- **Arborescence des objets** : La logique est gérée par des `Managers` qui contrôlent les `Users` et les `Rooms`.
- **Liste des requêtes backend** :
    - `JoinRoom` : Un utilisateur rejoint un salon de discussion.
    - `QuitRoom` : Un utilisateur quitte un salon.
    - `SetName` : Un utilisateur change de nom.
    - `NewMessage` : Un utilisateur envoie un nouveau message dans un salon.

### ### Flux de communication
- **Connexion de l'utilisateur** :
    - Le serveur transmet la liste des **salons (rooms)** disponibles à l'utilisateur.
- **L'utilisateur rejoint un salon** :
    - Le salon avertit tous les autres utilisateurs de l'arrivée du nouvel utilisateur.
    - Le salon transmet toutes ses informations (messages précédents, etc.) au nouvel utilisateur.
- **Envoi d'un message** :
    - L'information est reçue par l'objet `user`.
    - L'objet `user` transmet l'information à l'objet `room`.
    - L'objet `room` diffuse le message à **tous les utilisateurs** présents dans le salon.

## 🟠 Principes d'Architecture Front-end

### ### SOFEA (Service Oriented Front End Architecture)
- **Idée principale** : Déplacer la logique applicative du serveur vers le client. Le serveur se concentre sur les processus métier et la fourniture de données via des services (API).
- **Avantages** :
    - **Évolutivité (Scalability)** : Meilleure répartition de la charge.
    - **Processing client** : Interfaces plus riches et interactives (animations, 2D/3D).
    - **Stateless** : Le serveur n'a pas besoin de conserver l'état de la session de chaque client.
    - **Mise en cache** efficace des ressources.
    - **Interopérabilité** : Le front-end est agnostique vis-à-vis de la technologie backend.
    - Permet des applications **hors connexion (offline)**.

### ### Application Web Monopage (SPA)
- **SPA (Single Page Application)** vs **MPA (Multi-Page Application)** :
    - **MPA** : Chaque action de l'utilisateur déclenche une nouvelle requête au serveur et un rechargement complet de la page.
    - **SPA** : La page initiale est chargée une seule fois. Les interactions suivantes chargent dynamiquement les données nécessaires (souvent via **AJAX**) sans recharger la page, offrant une expérience utilisateur plus fluide, similaire à une application de bureau.
- **Fonctionnement** : Le framework JavaScript (React, Vue, Angular) prend le contrôle du DOM et le met à jour dynamiquement en fonction des actions de l'utilisateur et des données reçues.

## 🟠 Angular

### ### Environnement d'Installation
- **Node.js + npm** : Environnement d'exécution JavaScript côté serveur et gestionnaire de paquets.
- **Angular CLI** : Outil en ligne de commande pour créer, gérer et construire des projets Angular (`ng new`, `ng generate component`).
- **TypeScript** : Sur-ensemble de JavaScript qui ajoute le typage statique, les classes et les interfaces, améliorant la robustesse des grandes applications. Le code TypeScript est **transpilé** en JavaScript.

### ### Concepts Clés
- **Composants** : Blocs de construction fondamentaux d'une application Angular. Un composant est une classe TypeScript avec un décorateur `@Component` qui le lie à un template HTML et des styles CSS.
- **Modules (`@NgModule`)** : Conteneurs pour regrouper des composants, directives, pipes et services qui sont liés. L'application a au moins un module racine, `AppModule`.
- **Data Binding (Liaison de données)** :
    - **Interpolation** `{{ data }}` : Affiche une donnée du composant dans le template.
    - **Property Binding** `[property]="data"` : Lie une propriété d'un élément HTML à une donnée du composant.
    - **Event Binding** `(event)="handler()"` : Déclenche une méthode du composant en réponse à un événement du DOM (ex: `(click)`).
    - **Two-Way Binding** `[(ngModel)]="data"` : Liaison bidirectionnelle, souvent utilisée dans les formulaires pour synchroniser l'input et le modèle.
- **Directives** : Instructions pour modifier le DOM.
    - **Structurelles** : modifient la structure du DOM. Ex: `*ngIf`, `*ngFor`.
    - **d'Attribut** : modifient l'apparence ou le comportement d'un élément. Ex: `ngStyle`, `ngClass`.
- **Props (via `@Input`)** : Le décorateur `@Input()` permet à un composant parent de passer des données à un composant enfant.
- **Services et Injection de Dépendances (DI)** :
    - Les services sont des classes qui encapsulent une logique métier réutilisable (ex: appel API).
    - Angular utilise un **injecteur de dépendances** pour fournir des instances de services aux composants qui en ont besoin, favorisant un code modulaire et testable.

## 🟠 React.js

### ### Principes Fondamentaux
- **Bibliothèque JavaScript** (et non un framework complet) pour construire des interfaces utilisateur.
- **Approche par composants** : L'UI est décomposée en composants indépendants et réutilisables.
- **Virtual DOM** : React utilise une représentation en mémoire du DOM réel. Lors d'un changement d'état, il compare le nouveau Virtual DOM avec l'ancien et n'applique que les modifications nécessaires au DOM réel, ce qui est très performant.
- **JSX (JavaScript XML)** : Une extension de syntaxe qui permet d'écrire du code de type HTML directement dans le JavaScript. Il est transpilé en appels `React.createElement()`.

### ### Installation et Projet
- **create-react-app** : L'outil officiel pour créer des applications React avec une configuration prête à l'emploi.
    - `npx create-react-app my-app`
- **Scripts NPM** :
    - `npm start` : Démarre le serveur de développement.
    - `npm test` : Lance les tests.
    - `npm run build` : Construit l'application pour la production.
- **Structure de projet** :
    - `public/index.html` : Le point d'entrée HTML avec une `div` racine (ex: `<div id="root"></div>`).
    - `src/index.js` : Le point d'entrée JavaScript qui "monte" le composant principal de l'application dans la `div` racine.
    - `src/App.js` : Le composant racine de l'application.

### ### Composants, Props et État (State)
- **Composants** :
    - **Fonctionnels** : Fonctions JavaScript simples qui retournent du JSX. C'est l'approche moderne et recommandée avec les Hooks.
    - **de Classe** : Classes ES6 qui héritent de `React.Component` et ont une méthode `render()`.
- **Props (Propriétés)** :
    - Mécanisme pour passer des données d'un **composant parent à un composant enfant**.
    - Les props sont en **lecture seule** (immuables) dans le composant enfant.
    - `props.children` est une prop spéciale qui contient les éléments imbriqués dans le composant.
- **State (État)** :
    - Un objet qui représente les données internes d'un composant qui peuvent **changer** au fil du temps.
    - Le `state` ne doit être utilisé que dans les composants qui en ont besoin (composants "stateful").
    - La modification de l'état avec `this.setState()` (classes) ou le `setter` de `useState` (fonctions) déclenche un **nouveau rendu (re-render)** du composant et de ses enfants.

### ### Cycle de vie et Hooks
- **Méthodes de cycle de vie (Classes)** : Des méthodes spéciales qui sont exécutées à des moments clés de la vie d'un composant (`componentDidMount`, `componentDidUpdate`, `componentWillUnmount`).
- **Hooks (Fonctions)** : Permettent d'utiliser l'état et d'autres fonctionnalités de React dans les composants fonctionnels.
    - **`useState`** : Pour déclarer une variable d'état local. Retourne la valeur actuelle et une fonction pour la mettre à jour.
    - **`useEffect`** : Pour gérer les "effets de bord" (ex: appels API, abonnements). Il remplace `componentDidMount`, `componentDidUpdate`, et `componentWillUnmount`. Son exécution est contrôlée par un tableau de dépendances.

### ### Communication avec une API et Gestion des Événements
- **Gestion des événements** : Les noms d'événements sont en `camelCase` (ex: `onClick`). On passe une fonction comme gestionnaire.
- **Appels API** : React n'inclut pas de client HTTP. On utilise l'API native `fetch()` ou des bibliothèques comme `axios`.
    - Les appels pour charger les données initiales se font typiquement dans un `useEffect` avec un tableau de dépendances vide `[]` pour ne s'exécuter qu'une seule fois.
- **Rendu conditionnel** : On utilise des conditions JavaScript (`if`, opérateur ternaire `? :`, opérateur logique `&&`) pour afficher du JSX de manière conditionnelle.

## 🟠 Vue.js

### ### Principes Fondamentaux
- **Framework progressif** : Peut être adopté progressivement, d'une simple bibliothèque à un framework complet pour des SPA complexes.
- **Virtual DOM** : Comme React, Vue utilise un DOM virtuel pour optimiser les mises à jour de l'affichage.
- **Data Binding** : La directive `v-model` permet une liaison de données bidirectionnelle très simple, particulièrement utile pour les formulaires.
- **Directives** : Attributs spéciaux préfixés par `v-` qui appliquent des comportements réactifs au DOM (`v-if`, `v-for`, `v-bind`, `v-on`).
- **Composants** : Le cœur de Vue.js est un système de composants permettant de construire des UI encapsulées et réutilisables.

### ### Composants, Props et Événements
- **Props** : Données passées d'un parent à un enfant. On peut les valider (type, requis, etc.).
- **Événements** : Un enfant communique avec son parent en émettant des événements via `this.$emit('nom-event', payload)`. Le parent écoute ces événements avec `v-on:nom-event` ou `@nom-event`.

### ### Patterns de Conception Avancés
- **Renderless Components** : Composants qui encapsulent une logique réutilisable mais ne rendent aucun balisage. Ils exposent leur état et leurs méthodes au composant parent via des **scoped slots** (`v-slot`), offrant une flexibilité maximale pour la couche de présentation.
- **Dependency Injection (`provide` / `inject`)** : Mécanisme pour passer des données à travers l'arbre des composants sans avoir à les passer manuellement via les props à chaque niveau ("props drilling"). Utile pour des données globales comme un store, un thème, etc.
- **Functional Core, Imperative Shell** : Un pattern d'architecture qui consiste à séparer :
    - Le **cœur fonctionnel** : Logique métier pure, sans état et sans effets de bord (fonctions pures, faciles à tester).
    - La **coquille impérative** : La couche Vue.js qui gère la réactivité, les effets de bord (appels API) et qui "enveloppe" le cœur fonctionnel.

## 🟠 Introduction à Redux (Gestion d'État Avancée)

### ### Pourquoi Redux ?
- Pour les applications avec un **état complexe** et partagé entre de nombreux composants, la gestion manuelle de l'état via les props et les événements peut devenir difficile.
- Redux propose une architecture pour une gestion d'état **prévisible**.

### ### Concepts Clés
- **Store unique** : L'ensemble de l'état de l'application est contenu dans un seul objet JavaScript (`store`), qui est la **source unique de vérité**.
- **Flux de données unidirectionnel** :
    1.  L'UI déclenche une **action** (un objet décrivant ce qui s'est passé).
    2.  L'action est envoyée (`dispatch`) au store.
    3.  Le store passe l'état actuel et l'action à un **reducer**.
    4.  Le **reducer** (une fonction pure) calcule le nouvel état et le retourne.
    5.  Le store sauvegarde le nouvel état et notifie l'UI du changement pour qu'elle se mette à jour.
- **Immuabilité** : L'état n'est jamais modifié directement. Les reducers retournent toujours un **nouvel objet d'état**.