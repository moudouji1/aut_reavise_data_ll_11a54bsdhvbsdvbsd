## Séance 5 : Fonctionnalités Natives, Déploiement et Génération d’APK

Cette séance couvre l'intégration des fonctionnalités natives du téléphone, comme la **localisation (GPS)** et la **caméra**, dans une application Expo. Elle détaille le processus de demande de permissions à l'utilisateur, l'utilisation des API spécifiques, et se conclut par les étapes de déploiement d'une application, de la configuration à la génération d'un fichier **APK** pour Android via les services **EAS (Expo Application Services)**.

---

### 1. Accès à la Localisation (GPS)

*   **Principe** : Utiliser le module `expo-location` pour interagir avec le capteur GPS du téléphone.

#### Installation et Configuration
- **Installer le package** nécessaire via la commande :
  ```bash
  npx expo install expo-location
  ```
- **Configurer les permissions** dans le fichier `app.json` pour autoriser l'accès à la localisation sur Android.
  ```json
  "plugins": [
    [
      "expo-location",
      {
        "locationAlwaysAndWhenInUsePermission": "Permettre à $(PRODUCT_NAME) d'utiliser votre localisation."
      }
    ]
  ]
  ```

#### Implémentation dans le code
- **Demander la permission** : Il est obligatoire de demander l'accord de l'utilisateur avant d'accéder à sa position.
  - On utilise la fonction `Location.requestForegroundPermissionsAsync()`.
  - Cette fonction retourne un objet `status` qui peut être `'granted'` (accordé) or `'denied'` (refusé).
- **Récupérer la position** : Si la permission est accordée, on peut obtenir les coordonnées.
  - On utilise la fonction `Location.getCurrentPositionAsync({})`.
  - Cette fonction retourne un objet `location` contenant les `coords` (**latitude** et **longitude**).

---

### 2. Utilisation de la Caméra

*   **Principe** : Utiliser le module `expo-camera` pour afficher la vue de la caméra et prendre des photos.

#### Installation et Configuration
- **Installer le package** via la commande :
  ```bash
  npx expo install expo-camera
  ```
- **Configurer les permissions** dans le fichier `app.json` pour autoriser l'accès à la caméra.
  ```json
  "plugins": [
    [
      "expo-camera",
      {
        "cameraPermission": "Permettre à $(PRODUCT_NAME) d'accéder à votre caméra."
      }
    ]
  ]
  ```

#### Implémentation dans le code
- **Demander la permission** : Comme pour la localisation, l'accord de l'utilisateur est requis.
  - On utilise la fonction `Camera.requestCameraPermissionsAsync()`.
- **Afficher la caméra** :
  - On utilise le composant `<Camera>` importé depuis `expo-camera`.
  - Il est crucial de gérer l'état des permissions pour n'afficher le composant que si l'accès est autorisé.
- **Prendre une photo** :
  - On utilise un `useRef` pour créer une référence au composant `<Camera>`.
  - On appelle la méthode `takePictureAsync()` sur cette référence.
  - La méthode retourne un objet contenant l'**URI** (l'adresse locale) de l'image capturée.

---

### 3. Déploiement et Génération d'un APK

*   **Principe** : Utiliser **EAS (Expo Application Services)**, l'outil cloud d'Expo, pour "builder" (construire) l'application et générer un fichier d'installation pour Android (`.apk`).

#### Prérequis et Installation
- **Installer EAS CLI** (Command Line Interface) globalement sur votre machine :
  ```bash
  npm install -g eas-cli
  ```
- **Se connecter** à son compte Expo via le terminal :
  ```bash
  eas login
  ```

#### Configuration du Build
- **Initialiser la configuration** pour le build dans votre projet :
  ```bash
  eas build:configure
  ```
  - Cette commande crée un fichier `eas.json` qui définit les profils de build (ex: `production`, `preview`).
- **Modifier `app.json`** pour inclure les informations nécessaires au build, notamment :
  - `android.package` : Un identifiant unique pour votre application (ex: `com.votreNom.votreApp`).
  - `android.versionCode` : Un numéro de version pour votre build.

#### Lancement du Build
- **Lancer la construction** pour la plateforme Android en utilisant le profil `production` :
  ```bash
  eas build -p android --profile production
  ```
- **Processus** : EAS va compresser votre projet, l'envoyer sur ses serveurs, installer les dépendances et construire l'application dans un environnement Android natif.
- **Suivi** : Vous recevrez un lien pour suivre l'avancement du build en temps réel.

#### Récupération de l'APK
- Une fois le build terminé avec succès, vous obtiendrez un **lien de téléchargement** pour votre fichier **APK**.
- Ce fichier peut être installé directement sur un appareil Android pour tester ou distribuer l'application.