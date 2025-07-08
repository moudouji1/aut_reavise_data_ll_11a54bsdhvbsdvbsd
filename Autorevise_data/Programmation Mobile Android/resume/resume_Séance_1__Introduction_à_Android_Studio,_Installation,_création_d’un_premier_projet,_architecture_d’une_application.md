Cette séance introduit les bases du développement Android. Elle se concentre sur l'installation de l'environnement de développement officiel, **Android Studio**, et aborde deux concepts architecturaux fondamentaux : l'**Intent** pour la navigation entre les écrans et le rôle central du fichier **AndroidManifest.xml** pour la configuration de l'application.

## Séance 1 : Introduction à Android Studio et Architecture d'une Application

### Environnement de Développement et Installation

*   L'environnement de développement (IDE) officiel et recommandé pour créer des applications Android est **Android Studio**.
*   Android Studio inclut le **SDK Android** (Software Development Kit), qui est un ensemble d'outils nécessaires au développement.
*   L'installation se fait en téléchargeant le pack depuis le site officiel de développeur Android.
    *   *Note : Les anciennes méthodes basées sur Eclipse et le plugin ADT sont obsolètes.*
*   Le SDK Manager, inclus dans Android Studio, permet de télécharger et gérer les différentes **versions de l'API Android** nécessaires pour vos projets.

### Architecture et Concepts Fondamentaux

#### L'Intent : Le Messager de l'Application

*   Un **`Intent`** est un objet de messagerie utilisé pour demander une action à un autre composant de l'application.
*   Son rôle principal est de **naviguer entre les écrans** (les `Activity`).
*   Il existe deux manières principales de démarrer une nouvelle activité avec un `Intent` :
    *   Démarrer une activité **sans attendre de résultat** en retour.
    *   Démarrer une activité et **recevoir un résultat** une fois qu'elle est terminée.

#### Le Fichier Manifeste : La Carte d'Identité de l'Application

*   Chaque application Android doit posséder un fichier de configuration nommé **`AndroidManifest.xml`**.
*   Ce fichier est essentiel car il décrit les informations fondamentales de l'application pour le système Android.
*   Toute **`Activity`** (chaque écran) de votre application doit obligatoirement y être déclarée à l'intérieur de la balise `<application>`.