## Séance 3 : Navigation et fragments, Multi-écrans avec fragments et intents

Cette séance introduit les **Fragments** comme des composants d'interface utilisateur modulaires et réutilisables. L'objectif est de comprendre leur cycle de vie, comment les intégrer dans une activité, et comment les utiliser pour créer des **interfaces adaptatives (responsive)** qui fonctionnent aussi bien sur smartphone que sur tablette. La séance aborde également la communication entre fragments et la manière dont ils interagissent avec les **Intents** pour la navigation.

### 1. Introduction aux Fragments

*   **Définition** : Un **Fragment** est une "sous-activité". Il représente une portion de l'interface utilisateur (UI) qui peut être intégrée dans une `Activity`. Un fragment a son propre layout et son propre cycle de vie.
*   **Principaux avantages** :
    *   **Réutilisabilité** : Un même fragment peut être utilisé dans plusieurs activités différentes.
    *   **Modularité** : Permet de décomposer une interface complexe en composants indépendants et plus faciles à gérer.
    *   **Adaptabilité** : Facilite la création d'interfaces utilisateur **responsives** pour différentes tailles d'écran (ex: une seule vue sur smartphone, deux vues côte à côte sur tablette).

### 2. Le Cycle de Vie d'un Fragment

*   Le cycle de vie d'un fragment est étroitement lié à celui de son `Activity` hôte. Si l'activité est mise en pause, tous ses fragments le sont aussi.
*   **Étapes clés du cycle de vie** :
    *   `onAttach()`: Le fragment est attaché à son `Activity` hôte.
    *   `onCreate()`: Initialisation non graphique du fragment.
    *   `onCreateView()`: **Méthode cruciale**. C'est ici que le fragment **"gonfle" (inflate)** son layout XML pour créer sa hiérarchie de vues.
    *   `onViewCreated()`: Appelée juste après `onCreateView()`, idéale pour configurer les vues (ex: `findViewById`).
    *   `onStart()` / `onResume()`: Le fragment devient visible et/ou interactif.
    *   `onPause()` / `onStop()`: Le fragment n'est plus interactif ou visible.
    *   `onDestroyView()`: La hiérarchie de vues du fragment est détruite. C'est le moment de nettoyer les références aux vues.
    *   `onDestroy()`: Nettoyage final du fragment.
    *   `onDetach()`: Le fragment est détaché de son `Activity`.

### 3. Intégration et Gestion des Fragments

Il existe deux manières d'ajouter un fragment à une activité.

*   **1. Intégration Statique (dans le XML)**
    *   Utilisation de la balise `<fragment>` directement dans le fichier de layout de l'activité.
    *   Simple et direct, mais **rigide** et **moins flexible**.

*   **2. Intégration Dynamique (dans le code Kotlin/Java)**
    *   C'est la **méthode recommandée et la plus flexible**.
    *   Elle utilise le `FragmentManager` et les `FragmentTransaction`.
    *   **Étapes** :
        1.  Obtenir une instance du `FragmentManager` : `supportFragmentManager`.
        2.  Démarrer une transaction : `beginTransaction()`.
        3.  Effectuer des opérations : `add()`, `replace()`, `remove()`.
        4.  (Optionnel) Ajouter la transaction à la pile arrière : `addToBackStack(null)`.
        5.  Valider la transaction : `commit()`.

### 4. Communication entre Fragments et Activités

*   **Fragment vers Activity (Hôte)**
    *   La **meilleure pratique** est de définir une **interface de callback** dans le fragment.
    *   L'`Activity` hôte **implémente cette interface**.
    *   Dans `onAttach()`, le fragment récupère une référence à l'activité et vérifie qu'elle implémente bien l'interface.
    *   Le fragment peut alors appeler les méthodes de l'interface pour communiquer des événements à l'activité.

*   **Activity vers Fragment**
    *   L'activité peut trouver une instance de fragment via son ID (`findFragmentById()`) ou son tag (`findFragmentByTag()`).
    *   Elle peut ensuite appeler des **méthodes publiques** définies dans le fragment.
    *   Pour passer des données initiales à un fragment, la bonne pratique est d'utiliser une **méthode `newInstance()` statique** qui attache les arguments dans un `Bundle`.

### 5. Multi-Écrans et Navigation avec Fragments

*   **Pile Arrière (Back Stack)**
    *   En appelant `addToBackStack()` lors d'une transaction, l'état précédent du fragment est sauvegardé.
    *   L'utilisateur peut alors revenir en arrière avec le bouton "Retour" du système, ce qui annule la transaction.

*   **Conception pour Multi-Écrans (ex: Master/Detail)**
    *   **Sur smartphone** : On utilise deux activités. `ActivityA` affiche un fragment de liste (`MasterFragment`). Un clic sur un élément ouvre `ActivityB` qui affiche un fragment de détail (`DetailFragment`).
    *   **Sur tablette** : On utilise une seule activité (`ActivityA`) qui affiche les deux fragments (`MasterFragment` et `DetailFragment`) côte à côte. La communication se fait via l'interface de callback.
    *   Ceci est réalisé en utilisant des **qualificateurs de ressources** (ex: `layout/` pour les smartphones, `layout-sw600dp/` pour les tablettes).

### 6. Fragments et Intents

*   Les **Intents** sont le mécanisme principal d'Android pour la **navigation entre les `Activities`**.
*   Un fragment ne peut pas être démarré directement par un `Intent`. C'est toujours l'activité hôte qui le reçoit.
*   Cependant, un **fragment peut lancer une nouvelle `Activity`** en utilisant un `Intent` :
    *   `val intent = Intent(requireActivity(), DetailActivity::class.java)`
    *   `startActivity(intent)`
*   Ceci est courant dans un pattern Master/Detail sur smartphone, où le fragment de liste déclenche l'ouverture de l'activité de détail.