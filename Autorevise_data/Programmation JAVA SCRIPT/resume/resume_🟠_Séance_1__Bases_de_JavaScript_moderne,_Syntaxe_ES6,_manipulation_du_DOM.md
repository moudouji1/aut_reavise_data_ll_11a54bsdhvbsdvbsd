# Résumé de la Séance : JavaScript, du Web Classique au Moderne

Cette séance offre un panorama très complet du développement web, commençant par les bases indispensables de HTML et CSS, puis plongeant au cœur de JavaScript. Elle couvre la syntaxe fondamentale, la manipulation du DOM, et aborde des concepts avancés cruciaux comme la gestion de l'asynchronisme avec les callbacks, les promesses et async/await. La formation explore également des outils et frameworks puissants comme jQuery pour la simplification du code, Node.js et Express pour une incursion côté serveur, et termine sur les évolutions modernes du langage avec ES6 et TypeScript.

## Fondamentaux du Web : HTML & CSS

### Structure d'une page HTML
- Un document HTML est un arbre d'éléments (DOM).
- **`<html`** : Balise racine du document.
- **`<head>`** : Contient les méta-informations (titre, encodage `UTF-8`, liens CSS).
- **`<body>`** : Contient le contenu visible de la page.

### Les balises HTML
- Une balise a une partie **ouvrante** (`<div>`) et une partie **fermante** (`</div>`).
- Les balises peuvent contenir des **attributs** (ex: `<div class="container">`) pour fournir des informations supplémentaires.
- Certaines balises sont **orphelines** (ex: `<img ... />`, `<br />`).

### Balises courantes
- **Texte** : `<h1>` à `<h6>` pour les titres, `<p>` pour les paragraphes, `<strong>` pour le gras, `<em>` pour l'italique.
- **Listes** :
    - `<ul>` : Liste non ordonnée (à puces).
    - `<ol>` : Liste ordonnée (numérotée).
    - `<li>` : Élément de liste.
- **Liens** : `<a href="URL">Texte du lien</a>` pour créer un lien hypertexte. L'attribut `target="_blank"` ouvre le lien dans un nouvel onglet.
- **Images** : `<img src="chemin/image.jpg" alt="description">`.
- **Blocs génériques** :
    - `<div>` : Conteneur de type **block**.
    - `<span>` : Conteneur de type **inline**.

### Introduction à CSS
- **CSS (Cascading Style Sheets)** sert à mettre en forme les éléments HTML.
- **Intégration** :
    1.  **Externe** : Fichier `.css` lié via `<link rel="stylesheet" href="style.css">` (méthode recommandée).
    2.  **Interne** : Dans la balise `<style>` à l'intérieur du `<head>`.
    3.  **En ligne (inline)** : Via l'attribut `style` directement sur une balise HTML.

### Sélecteurs CSS
- Permettent de cibler les éléments HTML à styliser.
- **Par balise** : `p` (cible tous les paragraphes).
- **Par classe** : `.nom-classe` (cible tous les éléments avec `class="nom-classe"`).
- **Par identifiant** : `#mon-id` (cible l'élément unique avec `id="mon-id"`).
- **Sélecteurs hiérarchiques** :
    - `div p` : Cible les `<p>` à l'intérieur d'une `<div>`.
    - `div > p` : Cible les `<p>` qui sont des **enfants directs** d'une `<div>`.
    - `h2 + p` : Cible le `<p>` qui suit **immédiatement** un `<h2>`.
- **Pseudo-classes** :
    - `:hover` : Au survol de la souris.
    - `:focus` : Quand l'élément a le focus.
    - `:first-child` / `:last-child` : Cible le premier / dernier enfant.

### Le Modèle des Boîtes (Box Model)
- Chaque élément HTML est une boîte rectangulaire composée de :
    - **`content`** : Le contenu (texte, image).
    - **`padding`** : Marge intérieure (espace entre le contenu et la bordure).
    - **`border`** : La bordure.
    - **`margin`** : Marge extérieure (espace entre la bordure et les autres éléments).

### Introduction à Bootstrap
- **Bootstrap** est un framework CSS/JS gratuit pour créer des sites **responsives** et **mobiles** plus rapidement.
- Il fournit des composants prêts à l'emploi : système de **grille**, **boutons**, **formulaires**, **barres de navigation**, etc.
- Utilise un système de grille basé sur **12 colonnes** pour organiser la mise en page.

## Les Bases de JavaScript

### Variables et Portée
- **`let`** : Déclare une variable avec une portée de **bloc** (`{}`). C'est la méthode moderne préférée.
- **`const`** : Déclare une constante dont la valeur ne peut pas être réassignée. Portée de bloc également.
- **`var`** : Ancienne façon de déclarer des variables. A une portée de **fonction** et peut entraîner des comportements inattendus (hoisting). À éviter.

### Types de données
- **Types Primitifs** :
    - **`String`** : Chaîne de caractères (ex: `"Bonjour"`).
    - **`Number`** : Nombre (entier ou à virgule, ex: `42`, `3.14`).
    - **`Boolean`** : Vrai ou faux (`true`, `false`).
    - **`undefined`** : Variable déclarée mais non initialisée.
    - **`null`** : Absence intentionnelle de valeur.
- **Types Objets** :
    - **`Object`** : Collection de paires clé-valeur (ex: `{ nom: "Toto", age: 25 }`).
    - **`Array`** : Liste ordonnée d'éléments (ex: `[1, "deux", true]`).
    - **`Function`** : Un bloc de code exécutable.

### Opérateurs et Expressions
- **Arithmétiques** : `+`, `-`, `*`, `/`, `%` (modulo), `++` (incrément), `--` (décrément).
- **Concaténation** : L'opérateur `+` assemble des chaînes de caractères.
- **Comparaison** :
    - `==` : Égalité simple (avec conversion de type, à éviter).
    - `===` : Égalité **stricte** (sans conversion de type, à privilégier).
    - `!=`, `!==`, `<`, `>`, `<=`, `>=`.
- **Logiques** : `&&` (ET), `||` (OU), `!` (NON).

### Structures de Contrôle
- **`if / else if / else`** : Exécute des blocs de code en fonction de conditions.
- **`switch`** : Alternative au `if/else` pour tester une variable contre plusieurs valeurs.
- **Boucles** :
    - **`for`** : Répète un bloc un nombre de fois défini.
    - **`while`** : Répète un bloc tant qu'une condition est vraie.
    - **`for...of`** : Itère sur les éléments d'un objet itérable (comme un `Array`).
    - **`for...in`** : Itère sur les clés d'un `Object`.

### Fonctions
- Bloc de code réutilisable, défini avec le mot-clé `function` ou sous forme de **fonction fléchée (ES6)**.
- Peut prendre des **paramètres** et retourner une valeur avec **`return`**.
- Les fonctions sont des **citoyens de première classe** : elles peuvent être stockées dans des variables, passées en argument et retournées par d'autres fonctions.

## Manipulation du DOM (Document Object Model)

### Comprendre le DOM
- Le DOM est une représentation **arborescente** de la page HTML.
- Chaque balise est un **nœud** dans l'arbre.
- Permet à JavaScript de lire et de modifier le contenu, la structure et le style de la page de manière dynamique.

### Accéder aux éléments
- **`document.getElementById('id')`** : Sélectionne l'élément unique par son `id`.
- **`document.getElementsByClassName('classe')`** : Retourne une collection d'éléments par leur `class`.
- **`document.getElementsByTagName('div')`** : Retourne une collection d'éléments par leur nom de balise.
- **`document.querySelector('sélecteur_css')`** : Sélectionne le **premier** élément correspondant au sélecteur CSS.
- **`document.querySelectorAll('sélecteur_css')`** : Retourne **tous** les éléments correspondant au sélecteur CSS.

### Manipuler les éléments
- **Modifier le contenu** :
    - `element.innerHTML` : Modifie le contenu HTML à l'intérieur d'un élément.
    - `element.textContent` : Modifie le contenu textuel (ignore le HTML).
- **Modifier les attributs** :
    - `element.src`, `element.href` : Accès direct aux attributs communs.
    - `element.setAttribute('nom', 'valeur')` et `element.getAttribute('nom')`.
- **Modifier le style** : `element.style.proprieteCSS` (ex: `element.style.color = 'red'`).
- **Modifier les classes** : `element.classList.add('classe')`, `.remove('classe')`, `.toggle('classe')`.

### Créer et supprimer des éléments
- **`document.createElement('div')`** : Crée un nouvel élément.
- **`parent.appendChild(enfant)`** : Ajoute un élément `enfant` à la fin d'un élément `parent`.
- **`parent.removeChild(enfant)`** : Supprime un élément `enfant` de son `parent`.

### Gestion des Événements
- Permet de rendre la page interactive en réagissant aux actions de l'utilisateur.
- **`element.addEventListener('type_event', fonction_callback)`** : Attache un gestionnaire d'événement.
- **Événements courants** :
    - `click` : Clic de la souris.
    - `mouseover` / `mouseout` : Survol de la souris.
    - `keydown` / `keyup` : Appui sur une touche du clavier.
    - `submit` : Soumission d'un formulaire.
    - `change` : Changement de la valeur d'un champ de formulaire.

## La Gestion de l'Asynchrone en JavaScript

### Le "Callback Hell"
- Problème des **callbacks imbriqués** les uns dans les autres, créant une structure en "pyramide de la mort" (`pyramid of doom`).
- Rend le code **difficile à lire**, à maintenir et à déboguer.
- **Solutions** : nommer les fonctions, modulariser le code, et surtout, utiliser des Promesses.

### Les Promesses (Promises)
- Un objet **`Promise`** représente l'achèvement (ou l'échec) futur d'une opération asynchrone.
- Une promesse a trois états :
    1.  **`pending`** (en attente) : état initial.
    2.  **`fulfilled`** (tenue) : l'opération a réussi.
    3.  **`rejected`** (rejetée) : l'opération a échoué.
- **Méthodes clés** :
    - **`.then(onFulfilled, onRejected)`** : Exécute une fonction quand la promesse est tenue (ou rejetée).
    - **`.catch(onRejected)`** : Raccourci pour gérer uniquement les cas d'échec.
    - **`.finally(onFinally)`** : Exécute une fonction que la promesse soit tenue ou rejetée.
- **`Promise.all(iterable)`** : Attend que **toutes** les promesses de l'itérable soient tenues.
- **`Promise.race(iterable)`** : Attend que la **première** promesse de l'itérable soit tenue ou rejetée.

### Async / Await (ES2017)
- **Sucre syntaxique** au-dessus des promesses, rendant le code asynchrone plus lisible, comme s'il était synchrone.
- **`async function`** : Déclare une fonction qui retourne implicitement une promesse.
- **`await`** : Met en pause l'exécution de la fonction `async` et attend la résolution d'une promesse. Ne peut être utilisé que dans une fonction `async`.

## Introduction à jQuery

### Principes de base
- **jQuery** est une bibliothèque JavaScript qui simplifie la manipulation du DOM, la gestion des événements et les requêtes AJAX. Sa devise : **"Write less, do more"** (Écrire moins, faire plus).
- L'objet principal est `jQuery()` ou son alias `$()`.

### Sélection d'éléments
- Utilise la syntaxe des **sélecteurs CSS** pour trouver des éléments : `$('#monId')`, `$('.maClasse')`, `$('p')`.
- Le résultat est un **objet jQuery** sur lequel on peut chaîner des méthodes.

### Méthodes courantes
- **Manipulation du DOM** : `.html()`, `.text()`, `.attr()`, `.append()`, `.prepend()`, `.remove()`.
- **Manipulation CSS** : `.css()`, `.addClass()`, `.removeClass()`, `.toggleClass()`.
- **Événements** : `.on('click', ...)` ou les raccourcis `.click()`, `.hover()`, `.keydown()`.
- **Effets et Animations** : `.hide()`, `.show()`, `.fadeIn()`, `.fadeOut()`, `.slideUp()`, `.slideDown()`, `.animate()`.

### AJAX avec jQuery
- Simplifie les requêtes HTTP asynchrones.
- Méthodes principales : `$.ajax()`, `.load()`, `$.get()`, `$.post()`.

## Introduction à Node.js et Express

### Qu'est-ce qu'un Middleware ?
- **Express** est un framework de routage pour Node.js. Une application Express est une série de fonctions **middleware**.
- Un middleware est une fonction qui a accès aux objets **requête** (`req`), **réponse** (`res`), et à la fonction **middleware suivante** (`next`).
- **Rôles du middleware** :
    - Exécuter du code.
    - Modifier les objets `req` et `res`.
    - Terminer le cycle de la requête-réponse (en envoyant une réponse).
    - Appeler le middleware suivant dans la pile avec `next()`.
- **Attention** : si un middleware ne termine pas le cycle et n'appelle pas `next()`, la requête restera **bloquée**.
- **L'ordre des middlewares** est crucial, car ils sont exécutés séquentiellement.

## JavaScript Moderne : ES6 et TypeScript

### Nouveautés de ES6 (ECMAScript 2015)
- **`let` et `const`** : Pour la déclaration de variables avec portée de bloc.
- **Fonctions fléchées (Arrow Functions)** : Syntaxe plus concise pour les fonctions `(param) => { ... }`. Conserve le contexte de `this`.
- **Classes** : Sucre syntaxique pour la programmation orientée objet basées sur les prototypes. Utilise les mots-clés `class`, `constructor`, `extends`, `super`.
- **Modules (`import`/`export`)** : Système natif pour organiser et partager le code entre fichiers.
    - **`export`** : Rend une fonction, une classe ou une variable accessible depuis d'autres modules.
    - **`import`** : Utilise les fonctionnalités exportées par un autre module.

### Introduction à TypeScript
- **TypeScript (TS)** est un **sur-ensemble** de JavaScript développé par Microsoft.
- Ajoute un système de **typage statique optionnel** à JavaScript.
- Le code TS est **compilé** en code JavaScript standard, ce qui le rend compatible avec tous les navigateurs.
- **Avantages** :
    - **Détection d'erreurs** à la compilation plutôt qu'à l'exécution.
    - **Auto-complétion** et aide à la navigation dans le code améliorées dans les IDE.
    - Améliore la **maintenabilité** et la robustesse des grosses applications.
- **Fonctionnalités clés** :
    - **Types de base** : `number`, `string`, `boolean`, `any`, etc.
    - **`interface`** : Définit la "forme" d'un objet.
    - **`enum`** : Définit un ensemble de constantes nommées.