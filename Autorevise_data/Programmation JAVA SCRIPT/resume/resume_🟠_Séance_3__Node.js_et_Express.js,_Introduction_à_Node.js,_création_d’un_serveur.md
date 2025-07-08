# 🟠 Séance 3 : Node.js et Express.js, Introduction et création d’un serveur

Cette séance introduit les concepts fondamentaux de Node.js, notamment son environnement d'exécution et ses capacités. Elle aborde la création d'un serveur HTTP natif avant de présenter Express.js, un framework web minimaliste pour structurer des applications web. Les points clés incluent la gestion des requêtes, le routage, l'utilisation des middlewares, la gestion des fichiers statiques et une introduction à la communication en temps réel avec Socket.io.

## ## Introduction à Node.js

### ### Les possibilités de Node.js
- Création de **serveurs** et de sites internet complexes.
- Développement d'**applications console** et d'outils en ligne de commandes.
- Mise en place de **services réseau** sur mesure (Proxies, etc.).
- Création d'**API** robustes.
- Support natif des **sockets** pour la communication en temps réel.
- Développement d'applications avec des **interfaces graphiques (GUI)**.

### ### Prérequis pour travailler avec Node.js
- Bonnes connaissances en **JavaScript**.
- Compréhension de la programmation **asynchrone** et de l'architecture **événementielle (event-driven)**.
- Connaissances de base en **réseau** et sur le fonctionnement d'Internet.
- Familiarité avec les **modules natifs** de Node.js (ex: `http`, `fs`).

---

## ## Le Projet fil rouge : "ChatWithMe"

Un projet pratique est développé tout au long de la formation pour construire une application de chat.
- **Objectif** : Développer une base solide pour une application de chat.
- **Développement par étapes** :
    1.  Mise en place du **serveur web**.
    2.  Intégration de la **communication en temps réel** (client-serveur).
    3.  **Sauvegarde** des données.
    4.  **Monitoring** de l'application.

---

## ## Node.js et le Web : Le module `http`

### ### Créer un client HTTP (envoyer des requêtes)
- Le module natif `http` permet d'envoyer des requêtes à des serveurs.
- Il est possible de réaliser des requêtes **GET** et **POST** pour interagir avec des API externes.
- La gestion manuelle des requêtes peut être complexe.

### ### Créer un serveur HTTP
- Le module `http` permet de créer un serveur web de bas niveau.
- Il est possible de gérer différentes routes (ex: `/users`, `/media`) et méthodes (**GET**, **POST**).
- **Difficulté** : La création d'un serveur robuste avec le module natif est **complexe** et verbeuse, ce qui justifie l'utilisation de frameworks comme Express.

---

## ## Le module `request`

- C'est une **abstraction** des modules natifs `http` et `httpsis` de Node.js.
- Conçu pour **simplifier** au maximum l'envoi de requêtes HTTP(S).
- **Fonctionnalités supportées** : redirections, gestion des événements, streams, etc.
- Facilite grandement l'envoi de requêtes **GET** et **POST** par rapport au module natif.

---

## ## Le framework Express.js

### ### Qu'est-ce qu'Express ?
- C'est une **infrastructure web minimaliste, souple et rapide** pour Node.js.
- Il fournit un ensemble de fonctionnalités robustes pour les applications web et mobiles sans masquer les fonctionnalités de Node.js.
- Il simplifie la création d'API grâce à ses **méthodes utilitaires HTTP** et son système de **middleware**.

### ### Démarrer avec Express
- **Installation** : `npm install --save express`
- **"Hello World"** : Créer un serveur simple qui écoute sur un port et répond aux requêtes est très rapide.
- **Express Generator** : Un outil (`express-generator`) pour créer rapidement un **squelette d'application** Express avec une structure de projet prédéfinie.
    - Installation : `npm install express-generator -g`
    - Génération : `express mon-application`

### ### Le routage avec Express
- Une **route** est un chemin (path) dans une URL qui définit un point de terminaison de l'application.
- **Définition d'une route** : `app.METHOD(PATH, HANDLER)`
    - `app` : l'instance d'Express.
    - `METHOD` : une méthode HTTP en minuscules (ex: `get`, `post`).
    - `PATH` : le chemin de la route sur le serveur.
    - `HANDLER` : la fonction **callback** exécutée lorsque la route est appelée.
- Il est possible d'utiliser des **expressions régulières (regex)** dans les chemins.
- On peut **chaîner les gestionnaires** pour une même route.
- **`express.Router`** : Une classe pour créer des gestionnaires de routes modulaires et montables. Idéal pour mieux **architecturer** son projet en séparant la logique des routes.

### ### Le gestionnaire de routes et la fonction `next()`
- On peut fournir **plusieurs fonctions callback** pour une seule route.
- Chaque fonction (sauf la dernière) doit appeler la fonction `next()` pour passer le contrôle à la fonction suivante.
- Ce mécanisme est très utile pour implémenter des **préconditions** sur une route (ex: authentification, validation des données).

### ### Servir des fichiers statiques
- Le middleware `express.static('nom_du_dossier')` est utilisé pour servir des fichiers statiques (CSS, JavaScript côté client, images).
- On peut définir **plusieurs répertoires statiques**.
- Il est possible de créer un **préfixe de chemin virtuel** pour les fichiers statiques (ex: `app.use('/static', express.static('public'))`).

### ### Les middlewares
- **Définition** : Un middleware est une fonction qui a accès à l'objet **requête (`req`)**, à l'objet **réponse (`res`)**, et à la fonction **middleware suivante (`next`)** dans le cycle requête-réponse.
- Une application Express est essentiellement une **succession d'appels de fonctions middleware**.
- **Tâches d'un middleware** :
    - Exécuter n'importe quel code.
    - Apporter des modifications aux objets `req` et `res`.
    - Terminer le cycle requête-réponse en envoyant une réponse.
    - Appeler le middleware suivant dans la pile avec `next()`.
- **Attention** : Si un middleware ne termine pas le cycle ou n'appelle pas `next()`, la **requête restera bloquée**.
- **L'ordre des middlewares est crucial**. Un middleware déclaré en premier sera exécuté en premier.

---

## ## La communication en temps réel avec Socket.io

### ### L'évolution de la communication temps réel
- **Polling classique** : Le client demande des données au serveur à intervalles réguliers (ex: toutes les 5 secondes). Inefficace et gourmand en ressources.
- **Long Polling** : Le client fait une requête, et le serveur garde la connexion ouverte jusqu'à ce qu'il ait une nouvelle donnée à envoyer. Réduit la latence mais peut être complexe.
- **WebSockets** : Protocole qui établit une **connexion bidirectionnelle et persistante** entre le client et le serveur, permettant une communication en temps réel très efficace.

### ### Socket.io
- **Socket.io** est une bibliothèque qui facilite la communication temps réel et basée sur les événements.
- Elle utilise les **WebSockets** lorsque c'est possible, mais peut se replier sur d'autres techniques (comme le Long Polling) pour garantir la compatibilité avec tous les navigateurs.