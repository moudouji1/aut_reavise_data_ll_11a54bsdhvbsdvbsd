Cette séance présente les bases de données NoSQL comme Redis et MongoDB, et explique comment les intégrer dans une application Node.js, notamment avec l'outil Mongoose pour MongoDB. Elle aborde également la gestion de processus en production avec PM2. Le tout est illustré par des intégrations pratiques dans un projet de chat en temps réel.

## 🟠 Séance 4 : Base de données avec Node.js

### ## 🚀 Side Project : "ChatWithMe" - Communication Temps Réel

- **Objectif** : Intégrer **`socket.io`** pour la communication en temps réel et connecter une base de données pour la persistance des données.

- **Architecture Backend** :
    - Organisation du code avec des **objets** et des **Managers** pour une meilleure structure.
    - Définition des requêtes principales gérées par le backend.

- **Requêtes `socket.io`** :
    - `JoinRoom` : L'utilisateur rejoint un salon de discussion.
    - `QuitRoom` : L'utilisateur quitte le salon.
    - `SetName` : L'utilisateur modifie son pseudonyme.
    - `NewMessage` : L'utilisateur envoie un nouveau message dans un salon.

- **Logique des Événements** :
    - *À la connexion* : Le serveur envoie la **liste des salons** disponibles à l'utilisateur.
    - *Lorsqu'un utilisateur rejoint un salon* : Le salon notifie les autres utilisateurs de l'arrivée d'un nouveau membre et transmet les informations du salon au nouvel arrivant.
    - *Lorsqu'un utilisateur envoie un message* : Le message est transmis à l'objet `room` qui le relaie à **tous les utilisateurs** du salon.

---

### ## 📦 Introduction aux Bases de Données NoSQL

#### ### Redis (REmote DIctionary Server)
- **Définition** : Système de gestion de base de données **clé-valeur** NoSQL, très performant et écrit en C.
- **Caractéristiques** : Idéal pour le **caching**, la gestion de sessions ou les données volatiles grâce à sa rapidité.
- **Commandes de base** :
    - Démarrer le serveur : `sudo service redis-server start`
    - Se connecter via le client : `redis-cli`

#### ### MongoDB
- **Définition** : Système de gestion de base de données **orienté documents** (format BSON, similaire à JSON), scalable et ne nécessitant pas de schéma de données prédéfini.
- **Caractéristiques** : Fait partie du mouvement **NoSQL** et est écrit en C++.
- **Commandes de base** :
    - Démarrer le serveur : `mongod --nojournal`
    - Se connecter via le client : `mongo`

---

### ## 🔗 Interagir avec MongoDB via Mongoose

- **Mongoose** : C'est un **ODM** (Object Data Modeling) qui facilite l'interaction entre **Node.js** et **MongoDB**. Il permet de définir des **schémas** pour les modèles de données, d'effectuer des validations et de gérer la logique métier.

- **Opérations CRUD avec Mongoose** :
    - **`Create`** : Créer de nouveaux documents.
    - **`Read`** : Lire des documents existants.
    - **`Update`** : Mettre à jour des documents.
    - **`Delete`** : Supprimer des documents.

- **Associations de documents** :
    - Mongoose permet de créer des **liens** entre différents documents (par exemple, lier un `user` à ses `posts`), simulant ainsi les relations des bases de données SQL.

---

### ## ⚙️ Gestion de Processus en Production avec PM2

- **Définition** : **PM2** est un gestionnaire de processus de production pour les applications **Node.js**. Il inclut un **load balancer** intégré.

- **Avantages clés** :
    - **Maintien en vie** des applications (redémarrage automatique en cas de crash).
    - **Rechargement à chaud** (`hot reload`) sans interruption de service.
    - **Mode Cluster** pour exploiter tous les cœurs du processeur et améliorer les performances.

- **Commandes essentielles** :
    - **Installation** : `npm install -g pm2`
    - **Démarrage d'une app** : `pm2 start app.js --name ChatWithMe`
    - **Démarrage en mode cluster** : `pm2 start app.js -i 0` (autant de processus que de cœurs CPU).
    - **Gestion des processus** : `pm2 list`, `pm2 monit`, `pm2 stop/restart/reload all`, `pm2 delete 0`.

- **Gestion des Logs** :
    - **Afficher les logs** : `pm2 logs`
    - **Vider les logs** : `pm2 flush`

- **Limite à connaître** :
    - Le mode cluster de PM2, qui utilise le module natif `cluster` de Node.js, **n'est pas nativement compatible avec `socket.io`**. Des solutions alternatives comme `node-cluster-socket.io` sont nécessaires pour faire fonctionner les deux ensemble.