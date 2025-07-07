```json
{
  "titre": "Séance 4 : Sessions et Cookies, Gestion des utilisateurs",
  "themes": [
    {
      "nom": "Introduction : Cookies vs. Sessions",
      "sections": [
        {
          "titre": "Contexte",
          "contenu": "Le protocole HTTP est \"sans état\" (stateless), ce qui signifie que chaque requête est indépendante. Pour suivre un utilisateur à travers plusieurs pages (panier d'achat, connexion), on utilise les cookies et les sessions afin de maintenir un état."
        },
        {
          "titre": "Comparaison des Cookies et des Sessions",
          "contenu": [
            {
              "type": "Cookies",
              "avantages": [
                "Peuvent persister pendant longtemps (des années) sur le poste client.",
                "Fonctionnent bien dans des architectures distribuées (load balancing) car les données sont côté client."
              ],
              "inconvenients": [
                "Stockés sur la machine du client, donc non sécurisés pour des données sensibles.",
                "Taille limitée (généralement < 4 Ko).",
                "L'utilisateur peut les refuser, les modifier ou les supprimer.",
                "Viennent du client, donc ne jamais leur faire confiance (valider comme une donnée de formulaire)."
              ]
            },
            {
              "type": "Sessions",
              "avantages": [
                "Données stockées sur le serveur, donc plus sécurisées.",
                "Pas de limite de taille de stockage (ou limite serveur très élevée).",
                "L'utilisateur ne peut pas manipuler directement les données.",
                "Fonctionne même si les cookies sont désactivés (l'ID de session peut passer par l'URL)."
              ],
              "inconvenients": [
                "Consomme des ressources sur le serveur.",
                "Par défaut, liées à un seul serveur, ce qui peut compliquer les architectures distribuées.",
                "Le vol de l'identifiant de session (Session ID) peut permettre une usurpation d'identité."
              ]
            }
          ]
        }
      ]
    },
    {
      "nom": "Les Cookies en PHP",
      "sections": [
        {
          "titre": "Définition et Principe",
          "contenu": "Un cookie est un petit fichier texte stocké par le navigateur sur l'ordinateur de l'utilisateur. Il est envoyé automatiquement par le navigateur à chaque requête vers le même domaine."
        },
        {
          "titre": "Création d'un cookie",
          "contenu": "On utilise la fonction `setcookie()`. Elle doit être appelée AVANT toute sortie HTML (avant `<html>`, `echo`, etc.).",
          "code": {
            "langage": "php",
            "lignes": [
              "// setcookie(nom, valeur, expiration, chemin, domaine, securise, httpOnly);",
              "// Cookie qui expire dans 1 heure (3600 secondes)",
              "setcookie('nom_utilisateur', 'JohnDoe', time() + 3600, '/');"
            ]
          }
        },
        {
          "titre": "Lecture d'un cookie",
          "contenu": "Les cookies envoyés par le client sont disponibles dans la variable superglobale `$_COOKIE`. Il est crucial de vérifier leur existence avec `isset()` avant de les utiliser.",
          "code": {
            "langage": "php",
            "lignes": [
              "if (isset($_COOKIE['nom_utilisateur'])) {",
              "  echo 'Bonjour ' . htmlspecialchars($_COOKIE['nom_utilisateur']);",
              "} else {",
              "  echo 'Pas de cookie trouvé.';",
              "}"
            ]
          }
        },
        {
          "titre": "Suppression d'un cookie",
          "contenu": "Pour supprimer un cookie, on le redéfinit avec une date d'expiration passée.",
          "code": {
            "langage": "php",
            "lignes": [
              "// Met une date d'expiration dans le passé (il y a 1 heure)",
              "setcookie('nom_utilisateur', '', time() - 3600);"
            ]
          }
        }
      ]
    },
    {
      "nom": "Les Sessions en PHP",
      "sections": [
        {
          "titre": "Définition et Principe",
          "contenu": "Une session permet de stocker des informations sur le serveur pour un utilisateur spécifique. Le client ne conserve qu'un identifiant unique (Session ID), généralement via un cookie, qui permet de retrouver les données sur le serveur."
        },
        {
          "titre": "Utilisation des sessions",
          "contenu": "Le cycle de vie d'une session est simple : démarrer, manipuler les données, puis détruire.",
          "etapes": [
            {
              "etape": 1,
              "titre": "Démarrer ou reprendre une session",
              "description": "Utiliser `session_start()` au tout début de chaque page qui a besoin des sessions. Cette fonction doit être appelée avant toute sortie HTML.",
              "code": {
                "langage": "php",
                "lignes": ["session_start();"]
              }
            },
            {
              "etape": 2,
              "titre": "Stocker et accéder aux données",
              "description": "Les données de session sont stockées et lues via la variable superglobale `$_SESSION`, qui est un tableau associatif.",
              "code": {
                "langage": "php",
                "lignes": [
                  "// Stocker une information",
                  "$_SESSION['user_id'] = 123;",
                  "$_SESSION['username'] = 'JohnDoe';",
                  "",
                  "// Lire une information",
                  "if (isset($_SESSION['username'])) {",
                  "  echo 'Utilisateur connecté : ' . $_SESSION['username'];",
                  "}"
                ]
              }
            },
            {
              "etape": 3,
              "titre": "Détruire une session",
              "description": "Pour déconnecter un utilisateur, il faut détruire toutes les données de la session.",
              "code": {
                "langage": "php",
                "lignes": [
                  "// 1. Vider toutes les variables de session",
                  "$_SESSION = array();",
                  "// ou session_unset();",
                  "",
                  "// 2. Détruire le cookie de session si utilisé",
                  "if (ini_get('session.use_cookies')) {",
                  "    $params = session_get_cookie_params();",
                  "    setcookie(session_name(), '', time() - 42000, $params['path'], $params['domain'], $params['secure'], $params['httponly']);",
                  "}",
                  "",
                  "// 3. Finalement, détruire la session sur le serveur",
                  "session_destroy();"
                ]
              }
            }
          ]
        },
        {
          "titre": "Configuration",
          "contenu": "La configuration des sessions se fait principalement dans le fichier `php.ini` via des directives comme `session.save_path` (où stocker les fichiers de session) ou `session.gc_maxlifetime` (durée de vie d'une session inactive)."
        }
      ]
    },
    {
      "nom": "Alternative : JSON Web Tokens (JWT)",
      "sections": [
        {
          "titre": "Principe",
          "contenu": "JWT est un standard pour créer des jetons d'accès autonomes et compacts. Contrairement aux sessions, les données de l'utilisateur (non sensibles) sont contenues dans le jeton lui-même, évitant un appel à la base de données à chaque requête. C'est une approche \"stateless\" (sans état côté serveur)."
        },
        {
          "titre": "Structure d'un JWT",
          "contenu": "Un JWT est composé de 3 parties encodées en Base64Url et séparées par des points : `xxxxx.yyyyy.zzzzz`.",
          "parties": [
            {
              "nom": "Header (En-tête)",
              "description": "Contient le type de jeton (`typ`: 'JWT') et l'algorithme de signature (`alg`: 'HS256' ou 'RS256')."
            },
            {
              "nom": "Payload (Données utiles)",
              "description": "Contient les \"claims\" (revendications) sur l'utilisateur, comme son ID, son rôle, et une date d'expiration (`exp`)."
            },
            {
              "nom": "Signature",
              "description": "Sert à vérifier l'intégrité du jeton. Elle est calculée à partir du header, du payload et d'une clé secrète (pour HS256) ou d'une clé privée (pour RS256). Seul le serveur connaît ce secret."
            }
          ]
        },
        {
          "titre": "Stockage et Sécurité",
          "contenu": "Le JWT est généralement stocké côté client dans le `localStorage` ou dans un `cookie`. Chaque méthode a des implications de sécurité : `localStorage` est vulnérable aux attaques XSS, tandis que les cookies sont vulnérables aux attaques CSRF. Utiliser un cookie avec les flags `HttpOnly` et `Secure` est une pratique recommandée."
        }
      ]
    },
    {
      "nom": "Failles de Sécurité Courantes (OWASP Top 10)",
      "sections": [
        {
          "titre": "A2 - Violation d'Authentification et Gestion des Sessions",
          "contenu": "Un attaquant vole l'identifiant de session (cookie) d'une victime pour usurper son identité. Cela peut se produire si l'ID transite sur un réseau non sécurisé (HTTP).",
          "contreMesures": [
            "Utiliser HTTPS (SSL/TLS) pour chiffrer toute la communication.",
            "Régénérer l'ID de session après la connexion.",
            "Utiliser les flags de cookie `Secure` et `HttpOnly`."
          ]
        },
        {
          "titre": "XSS (Cross-Site Scripting)",
          "contenu": "L'attaquant injecte un script malveillant (ex: JavaScript) dans une page web vue par d'autres utilisateurs. Le script s'exécute dans le navigateur de la victime et peut voler des cookies, des sessions, ou modifier le contenu de la page.",
          "contreMesures": [
            "NE JAMAIS FAIRE CONFIANCE AUX DONNÉES UTILISATEUR.",
            "Valider et nettoyer toutes les entrées.",
            "Encoder systématiquement les données avant de les afficher dans du HTML (ex: `htmlspecialchars()` en PHP)."
          ]
        },
        {
          "titre": "A4 - Référence Directe non Sécurisée à un Objet",
          "contenu": "L'application expose une référence directe à un objet (ex: `.../facture.php?id=101`). Un attaquant modifie l'ID (`id=102`) pour accéder à des données qui ne lui sont pas destinées.",
          "contreMesures": [
            "Implémenter un contrôle d'accès sur le serveur pour chaque requête. Vérifier non seulement que l'utilisateur est connecté, mais aussi qu'il a le droit d'accéder à l'objet demandé."
          ]
        },
        {
          "titre": "A8 - CSRF (Cross-Site Request Forgery)",
          "contenu": "L'attaquant force le navigateur d'un utilisateur connecté à effectuer une requête non désirée vers une application web (ex: transférer de l'argent, changer un mot de passe). L'attaque fonctionne car le navigateur envoie automatiquement les cookies d'authentification avec la requête.",
          "contreMesures": [
            "Utiliser un jeton anti-CSRF (token) : un jeton unique et secret est ajouté à chaque formulaire. Le serveur vérifie sa présence et sa validité avant d'exécuter l'action."
          ]
        },
        {
          "titre": "A10 - Redirections et Renvois non Validés",
          "contenu": "L'application redirige vers une URL spécifiée dans un paramètre, sans la valider. Un attaquant peut créer un lien qui redirige vers un site malveillant (`.../login?redirect=http://site-pirate.com`) pour une attaque de phishing.",
          "contreMesures": [
            "Éviter les redirections basées sur des paramètres. Si nécessaire, utiliser une liste blanche (whitelist) d'URL de redirection autorisées."
          ]
        }
      ]
    }
  ]
}
```