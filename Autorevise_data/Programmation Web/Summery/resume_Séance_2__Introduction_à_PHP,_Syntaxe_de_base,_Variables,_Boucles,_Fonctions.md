```json
{
  "titre_session": "Séance 2 : Introduction à PHP, Syntaxe de base, Variables, Boucles, Fonctions",
  "resume_points_cles": [
    {
      "titre": "Introduction à PHP",
      "contenu": "PHP (Hypertext Preprocessor) est un langage de script open source exécuté côté serveur. Il est spécialisé dans le développement d'applications web et s'intègre facilement dans le code HTML.\n- **Côté Serveur** : Le code PHP est interprété par le serveur, qui envoie ensuite le résultat (généralement du HTML) au navigateur du client. Cela protège le code source et rend l'application indépendante de la configuration du client.\n- **Syntaxe** : Inspirée des langages C, Java et Perl."
    },
    {
      "titre": "Syntaxe de Base et Intégration HTML",
      "contenu": "Le code PHP s'insère dans un fichier HTML à l'aide de balises spécifiques.\n- **Balises PHP** : Le code est encadré par `<?php ... ?>`. Une balise de fermeture `?>` à la fin d'un fichier est optionnelle.\n- **Séparateur d'instructions** : Chaque instruction PHP doit se terminer par un point-virgule (`;`).\n- **Commentaires** : `//` pour un commentaire sur une ligne, ou `/* ... */` pour un commentaire sur plusieurs lignes.\n- **Affichage** : Les fonctions `echo` et `print` sont utilisées pour envoyer du texte (et du HTML) au navigateur. `echo` est légèrement plus rapide et peut prendre plusieurs arguments séparés par des virgules.\n- **Sensibilité à la casse** : Les noms de variables sont sensibles à la casse (`$variable` est différent de `$Variable`), mais les noms de fonctions ne le sont pas (`echo()` est identique à `ECHO()`)."
    },
    {
      "titre": "Variables et Types de Données",
      "contenu": "Les variables servent à stocker des informations.\n- **Déclaration** : Un nom de variable commence toujours par un `$` (dollar), suivi d'une lettre ou d'un underscore. Exemple : `$nom_utilisateur = \"Alice\";`.\n- **Types de données principaux** :\n  - **Scalaires** : `string` (chaîne de caractères), `integer` (entier), `float` (nombre à virgule flottante), `boolean` (vrai/faux).\n  - **Composés** : `array` (tableau), `object` (objet).\n  - **Spéciaux** : `NULL` (valeur nulle), `resource` (référence à une ressource externe).\n- **Chaînes de caractères** :\n  - **Guillemets simples (`'`)** : Le contenu est traité littéralement. `$nom = 'Bob'; echo 'Bonjour $nom';` affichera `Bonjour $nom`.\n  - **Guillemets doubles (`\"`)** : Les variables sont interprétées. `$nom = 'Bob'; echo \"Bonjour $nom\";` affichera `Bonjour Bob`.\n- **Concaténation** : L'opérateur `.` permet de joindre des chaînes. Exemple : `echo 'Bonjour ' . $nom;`."
    },
    {
      "titre": "Opérateurs",
      "contenu": "PHP dispose de plusieurs types d'opérateurs pour effectuer des opérations.\n- **Arithmétiques** : `+` (addition), `-` (soustraction), `*` (multiplication), `/` (division), `%` (modulo).\n- **d'Affectation** : `=` (affectation simple), `+=`, `-=`, `.` (concaténation).\n- **de Comparaison** : `==` (égal), `!=` (différent), `>` (supérieur), `<` (inférieur), `>=` (supérieur ou égal), `<=` (inférieur ou égal).\n- **d'Incrémentation/Décrémentation** : `++` (augmente de 1), `--` (diminue de 1).\n- **Logiques** : `&&` ou `and` (ET), `||` ou `or` (OU), `!` (NON)."
    },
    {
      "titre": "Structures de Contrôle (Conditions et Boucles)",
      "contenu": "Les structures de contrôle permettent de diriger le flux d'exécution du programme.\n- **Conditions** :\n  - `if`, `elseif`, `else` : Exécute des blocs de code si certaines conditions sont remplies.\n    `if ($age >= 18) { echo 'Majeur'; } else { echo 'Mineur'; }`\n  - `switch` : Compare une variable à plusieurs valeurs possibles.\n    `switch ($jour) { case 'Lundi': ... break; default: ... }`\n- **Boucles** :\n  - `while` : Répète un bloc de code tant qu'une condition est vraie.\n    `while ($i < 10) { ... $i++; }`\n  - `for` : Répète un bloc de code un nombre de fois défini.\n    `for ($i = 0; $i < 10; $i++) { ... }`\n  - `foreach` : Spécialement conçue pour parcourir les tableaux.\n    `foreach ($tableau as $element) { ... }`"
    },
    {
      "titre": "Tableaux (Arrays)",
      "contenu": "Un tableau est une variable spéciale qui peut contenir plusieurs valeurs.\n- **Types de tableaux** :\n  - **Tableau indexé** : Les clés sont des entiers (par défaut, à partir de 0). `$fruits = array('Pomme', 'Banane', 'Fraise');` ou `$fruits = ['Pomme', 'Banane'];`\n  - **Tableau associatif** : Les clés sont des chaînes de caractères. `$personne = array('nom' => 'Dupont', 'age' => 30);`\n- **Accès aux éléments** : On utilise les crochets `[]`. `echo $fruits[0];` (affiche 'Pomme'). `echo $personne['nom'];` (affiche 'Dupont').\n- **Parcourir un tableau** : La boucle `foreach` est la méthode la plus courante.\n  `foreach ($fruits as $fruit) { echo $fruit; }`\n  `foreach ($personne as $cle => $valeur) { echo \"$cle : $valeur\"; }`\n- **Fonctions utiles** : \n  - `count($tableau)` : Compte le nombre d'éléments.\n  - `sort($tableau)` : Trie les valeurs (perd les clés associatives).\n  - `asort($tableau)` : Trie les valeurs en conservant les clés.\n  - `ksort($tableau)` : Trie par clés.\n  - `implode(', ', $tableau)` : Joint les éléments d'un tableau en une chaîne.\n  - `explode(',', $chaine)` : Scinde une chaîne en un tableau."
    },
    {
      "titre": "Fonctions",
      "contenu": "Les fonctions sont des blocs de code réutilisables qui effectuent une tâche spécifique.\n- **Définition** : `function nomDeLaFonction($parametre1, $parametre2) { ... }`\n- **Appel** : `nomDeLaFonction('valeur1', 123);`\n- **Retour de valeur** : L'instruction `return` permet à une fonction de renvoyer un résultat. `function addition($a, $b) { return $a + $b; }`\n- **Portée des variables (Scope)** : Par défaut, les variables définies à l'extérieur d'une fonction ne sont pas accessibles à l'intérieur, et vice-versa. Le mot-clé `global` permet d'accéder à une variable globale depuis une fonction."
    },
    {
      "titre": "Gestion des Formulaires HTML",
      "contenu": "PHP est particulièrement efficace pour traiter les données envoyées par des formulaires HTML.\n- **Méthodes d'envoi** :\n  - `GET` : Les données sont envoyées dans l'URL. Accessibles en PHP via le tableau superglobal `$_GET`.\n  - `POST` : Les données sont envoyées dans le corps de la requête HTTP. Accessibles via `$_POST`.\n- **Récupération des données** : Le nom de chaque champ (`<input name=\"nom_du_champ\">`) devient une clé dans les tableaux `$_GET` ou `$_POST`. Exemple : `$_POST['nom_du_champ']`.\n- **Validation** : Il est crucial de toujours valider et nettoyer les données reçues d'un utilisateur pour des raisons de sécurité. Utiliser des fonctions comme `isset()`, `empty()`, `htmlspecialchars()`, etc."
    },
    {
      "titre": "Gestion des Fichiers",
      "contenu": "PHP peut lire, écrire, créer et manipuler des fichiers sur le serveur.\n- **Permissions** : Le serveur web doit avoir les droits nécessaires pour lire ou écrire dans les fichiers/dossiers.\n- **Fonctions principales** :\n  - `fopen('fichier.txt', 'r')` : Ouvre un fichier avec un mode spécifique ('r' pour lecture, 'w' pour écriture, 'a' pour ajout) et retourne une ressource.\n  - `fwrite($handle, 'texte')` : Écrit dans un fichier ouvert.\n  - `fgets($handle)` : Lit une ligne d'un fichier ouvert.\n  - `fclose($handle)` : Ferme un fichier ouvert.\n  - `file_get_contents('fichier.txt')` : Lit tout le contenu d'un fichier dans une chaîne.\n  - `file_put_contents('fichier.txt', 'contenu')` : Écrit une chaîne dans un fichier.\n- **Téléchargement de fichiers (Upload)** : Les fichiers envoyés via un formulaire sont disponibles dans le tableau superglobal `$_FILES`. Il faut utiliser `is_uploaded_file()` pour vérifier et `move_uploaded_file()` pour déplacer le fichier du répertoire temporaire vers sa destination finale."
    },
    {
      "titre": "(Avancé) Programmation Orientée Objet (POO)",
      "contenu": "PHP supporte pleinement la programmation orientée objet.\n- **Classe** : Un modèle pour créer des objets. Défini avec le mot-clé `class`. Elle contient des propriétés (variables) et des méthodes (fonctions).\n  `class Voiture { public $couleur; function demarrer() { ... } }`\n- **Objet** : Une instance d'une classe. Créé avec `new`.\n  `$maVoiture = new Voiture();`\n- **Accès** : On accède aux propriétés et méthodes avec `->`.\n  `$maVoiture->couleur = 'rouge';`\n  `$maVoiture->demarrer();`\n- **Visibilité** : `public` (accessible partout), `protected` (accessible dans la classe et ses descendantes), `private` (accessible uniquement dans la classe).\n- **Héritage** : Une classe peut hériter des propriétés et méthodes d'une autre avec `extends`."
    }
  ]
}
```