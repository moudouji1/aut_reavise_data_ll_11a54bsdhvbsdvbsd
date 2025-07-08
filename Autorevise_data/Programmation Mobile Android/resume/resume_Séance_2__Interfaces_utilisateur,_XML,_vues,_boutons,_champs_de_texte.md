Cette séance couvre les fondamentaux d'Android, de son histoire et son architecture aux éléments pratiques de la création d'interfaces utilisateur. Vous apprendrez ce que sont les composants d'une application (Activities, Services, etc.), comment structurer un projet dans Android Studio et, surtout, comment définir des interfaces avec XML. Les concepts clés incluent les `Layouts`, les vues comme `Button`, l'utilisation d'attributs XML comme `layout_width` et `layout_height`, et la manière de lier ces éléments visuels au code Java avec `findViewById`.

## Séance 2 : Interfaces utilisateur, XML, vues, boutons, champs de texte

### Introduction à Android

*   **Définition** : Une plateforme logicielle et un système d'exploitation pour appareils mobiles.
*   **Base** : Fondé sur le **noyau Linux**.
*   **Développement** : Géré par **Google** et l'Open Handset Alliance (OHA).
*   **Historique** : La première version commerciale a été lancée le **23 septembre 2008** avec le HTC Dream.

### Architecture d'une application Android

#### Composants principaux d'une application

Les composants sont les blocs de construction essentiels d'une application. Il en existe quatre types principaux :

*   **Activities** : Représente un **écran unique avec une interface utilisateur**. C'est le point d'entrée visuel pour l'utilisateur.
*   **Services** : Un composant qui s'exécute en **arrière-plan** pour des opérations de longue durée (ex: jouer de la musique, télécharger un fichier). Il n'a **pas d'interface utilisateur**.
*   **Content Providers** : Gère un ensemble de **données partagées** de l'application (ex: contacts). Il permet à d'autres applications d'accéder ou de modifier ces données de manière sécurisée.
*   **Broadcast Receivers** : Répond aux **annonces système globales** (ex: batterie faible, réception d'un SMS, démarrage de l'appareil).

#### Structure technique

*   **Noyau Linux** : Android utilise Linux pour la gestion des pilotes, de la mémoire, des processus et du réseau.
*   **Bibliothèques natives** : Écrites en C/C++, elles sont appelées via des interfaces Java.
*   **Dalvik Virtual Machine (DVM)** : La machine virtuelle optimisée pour mobile qui exécute les fichiers `.dex` (code Java compilé).

### Environnement de développement

*   **Prérequis logiciels** :
    *   **JDK** (Java Development Kit).
    *   **Android Studio** (l'IDE recommandé).
*   **Structure d'un projet Android Studio** :
    *   `src/` : Contient les fichiers source **.java** de votre application, y compris vos `Activities`.
    *   `res/` : Contient toutes les **ressources** de l'application.
        *   `res/layout/` : Fichiers **XML** qui définissent les interfaces utilisateur.
        *   `res/drawable/` : Fichiers d'images (png, jpg) ou de formes XML.
        *   `res/values/` : Fichiers XML pour les chaînes de caractères (`strings.xml`), les couleurs (`colors.xml`), etc.
        *   `res/raw/` : Fichiers bruts, comme des fichiers audio (MP3) ou vidéo.
    *   `AndroidManifest.xml` : Le **fichier de configuration central** de l'application. Il décrit la nature de l'application, déclare ses composants, ses permissions, etc.

### Création d'Interfaces Utilisateur (UI) avec XML

#### Le concept de Layout

*   Un **Layout** (ou "mise en page") définit l'**architecture visuelle** d'une interface utilisateur dans une `Activity`.
*   Il agit comme un conteneur pour les éléments d'interface (widgets).

#### Méthodes de déclaration de l'UI

1.  **Déclarer en XML** (méthode la plus courante et recommandée) :
    *   Android fournit un vocabulaire XML simple qui correspond aux classes `View` (comme `Button`, `TextView`).
    *   Sépare la présentation (XML) de la logique (Java), ce qui rend le code plus facile à maintenir.
2.  **Instancier en code Java** :
    *   L'application peut créer et manipuler des objets `View` et `ViewGroup` directement dans le code Java. Moins flexible et plus verbeux.

#### Lier le XML au code Java

Pour interagir avec un élément de l'interface (comme un bouton) dans votre code Java, vous devez :

1.  **Donner un ID unique** à l'élément dans le fichier XML :
    ```xml
    <Button
        android:id="@+id/mon_bouton"
        ... />
    ```
2.  **Récupérer une référence** à cet objet dans votre `Activity` en utilisant son ID :
    ```java
    Button monBouton = (Button) findViewById(R.id.mon_bouton);
    ```

#### Attributs de vue essentiels : `layout_width` et `layout_height`

Ces attributs définissent la taille d'une vue.

*   `wrap_content` : La vue prend juste la **taille nécessaire pour son contenu**.
*   `match_parent` (ou `fill_parent` dans les anciennes versions) : La vue s'étend pour **remplir tout l'espace disponible dans son conteneur parent**.

Exemple :
```xml
<Button
    android:id="@+id/my_button"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:text="Ceci est un bouton" />
```

#### Types de Layouts courants

*   **LinearLayout** : Aligne les vues enfants sur une seule ligne, soit **verticalement**, soit **horizontalement**.
*   **RelativeLayout** : Positionne les vues enfants les unes **par rapport aux autres** ou par rapport au layout parent.
*   **TableLayout** : Organise les vues en **lignes et colonnes**, comme un tableau HTML.