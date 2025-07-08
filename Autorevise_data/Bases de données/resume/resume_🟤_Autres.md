Ce cours offre une vue d'ensemble complète sur les réseaux informatiques, la programmation web avec PHP et SQL, et une introduction à la cartographie numérique. Il aborde les principes fondamentaux des réseaux, de leurs topologies et architectures (Ethernet, Token Ring) aux modèles de communication comme OSI et TCP/IP. La section sur PHP couvre les bases du langage, des structures de contrôle aux interactions avec des formulaires et des bases de données. La partie SQL détaille la gestion de bases de données avec MySQL via phpMyAdmin, incluant la création de tables, la manipulation de données et les jointures. Enfin, une introduction aux Systèmes d'Information Géographique (SIG) et au WebMapping est présentée, expliquant les concepts de base et les architectures client/serveur.

## Les Fondamentaux des Réseaux

### Avantages des Réseaux
- **Briser la chaîne numérique** : Permet le partage de fichiers efficace (fin du "Sneakernet"), la standardisation et l'automatisation.
- **Créer des synergies** : Le réseau apporte une valeur ajoutée (ex: messagerie électronique), où le tout est supérieur à la somme de ses parties.
- **Centraliser l'administration** : Facilite la gestion des configurations à distance, offrant un gain de temps et d'argent.
  - Outils notables : **SMS (Microsoft)**, **Saber LAN Manager**, **TME10 (Tivoli)**, **Norton Administrator for Networks**.

### Classification des Réseaux
- Les réseaux sont classifiés selon plusieurs critères, notamment leur **topologie**, leur **organisation** et les **protocoles** utilisés.
- **Protocoles routables** : Permettent de traverser des routeurs pour connecter plusieurs sous-réseaux.
  - *Routables* : **TCP/IP**, **IPX/SPX**, **OSI**, **AppleTalk (DDP)**.
  - *Non routables* : **NetBEUI**.

### Topologie des Réseaux
- La topologie est la représentation d'un réseau.
- **Topologie physique** : Disposition des matériels (câbles, postes).
- **Topologie logique** : Parcours de l'information entre les équipements.
- **Topologies courantes** :
  - **Bus** : Postes reliés à un seul câble. Simple et peu coûteux, mais une rupture du câble paralyse tout le segment.
  - **Étoile** : Chaque poste est relié à un point central (concentrateur ou **hub**, commutateur ou **switch**). Plus facile à administrer ; une panne de poste ou de câble n'affecte pas les autres.
  - **Anneau** : Les postes forment une boucle logique. La communication est gérée par un **jeton** (token) qui circule, évitant les collisions.
  - **Mixte** : Combinaison de plusieurs topologies (ex: bus en étoile).

### Types d'Organisation des Réseaux
- **Informatique centralisée** : Architecture historique (type IBM) avec un ordinateur central puissant et des terminaux "passifs".
- **Réseaux poste à poste (Peer-to-Peer)** : Chaque machine est à la fois client et serveur. Convient aux petits réseaux (< 10 postes). Pas d'administration centrale.
- **Réseaux Client/Serveur** : Des machines **clientes** accèdent aux ressources de machines **serveurs** dédiées (fichiers, impression, applications, etc.). Modèle le plus courant pour les réseaux d'entreprise.
  - Avantages : Centralisation de la gestion, sécurité accrue, meilleure performance pour les services partagés.
  - Serveurs dédiés : Serveur de fichiers, d'applications, de messagerie, web, proxy, etc.
  - Systèmes d'exploitation serveurs : **Windows NT Server**, **NetWare**, **UNIX**, **Linux**.

## Le Modèle OSI et les Protocoles

### Organismes de Normalisation
- Les normes assurent l'**interopérabilité** et la **compatibilité** entre équipements de différents constructeurs.
- Principaux organismes : **ISO** (International Standard Organization), **IEEE** (Institute of Electrical and Electronics Engineers), **ANSI**, **ITU** (anciennement CCITT).

### Le Modèle OSI (Open Systems Interconnection)
- Modèle théorique en **7 couches** qui standardise la communication réseau.
- **Couche 7 : Application** : Interface entre l'utilisateur et le réseau (ex: HTTP, FTP, SMTP).
- **Couche 6 : Présentation** : Formatage, compression et cryptage des données.
- **Couche 5 : Session** : Établissement, gestion et fin des connexions (sessions) entre applications.
- **Couche 4 : Transport** : Fiabilité des communications, segmentation des données en paquets et contrôle d'erreurs (**TCP**, **SPX**).
- **Couche 3 : Réseau** : Adressage logique (**IP**) et routage des paquets entre les réseaux.
- **Couche 2 : Liaison de données** : Adressage physique (**MAC**), création des trames et détection d'erreurs sur un support physique donné.
- **Couche 1 : Physique** : Transmission des bits bruts sur le support (câble, fibre optique). Spécifie les aspects électriques et mécaniques.

### Le Modèle IEEE 802
- Standard de l'IEEE pour les réseaux locaux (LAN).
- Raffine les couches 1 et 2 du modèle OSI.
- La couche **Liaison de données** est divisée en deux sous-couches :
  - **LLC (Logical Link Control)** : Gère la communication entre les couches supérieures et inférieures (norme **802.2**).
  - **MAC (Media Access Control)** : Gère l'accès au support physique (ex: **CSMA/CD** pour Ethernet).
- **Catégories notables** :
  - **802.3** : Ethernet (CSMA/CD)
  - **802.5** : Token Ring
  - **802.11** : Réseaux sans fil (Wi-Fi)

### Paquets et Trames
- **Segmentation** : Les données sont découpées en **paquets** pour fluidifier le réseau et faciliter la correction d'erreurs.
- **Structure d'un paquet** : Un paquet contient une **en-tête** (adresses source/destination, infos de contrôle), les **données** et une **queue** (vérification d'erreur CRC).
- **Adressage** : Les paquets sont adressés à un destinataire spécifique via son adresse MAC (couche 2) et son adresse IP (couche 3).
- **Routage** : Dans les réseaux étendus, les **routeurs** utilisent les adresses IP pour déterminer le meilleur chemin pour acheminer les paquets.

## Architectures Réseaux Spécifiques

### Réseaux ETHERNET
- Architecture la plus répandue, standardisée par la norme **IEEE 802.3**.
- **Méthode d'accès** : **CSMA/CD** (Carrier Sense Multiple Access with Collision Detection). Les stations écoutent le support avant d'émettre et détectent les collisions.
- **Topologie** : Bus ou étoile.
- **Normes courantes** :
  - **10BaseT** : 10 Mb/s sur câble à **paires torsadées (UTP/STP)**, topologie en étoile.
  - **10Base2 (Thinnet)** : 10 Mb/s sur **câble coaxial fin**, topologie en bus.
  - **10Base5 (Thicknet)** : 10 Mb/s sur **câble coaxial épais**, utilisé pour les dorsales (backbones).
  - **Fast Ethernet (100BaseX)** : 100 Mb/s, inclut **100BaseTX** (paires torsadées) et **100BaseFX** (fibre optique).
  - **Gigabit Ethernet** et plus : 1 Gb/s et au-delà.

### Réseaux TOKEN RING
- Développé par IBM, standardisé par **IEEE 802.5**.
- **Méthode d'accès** : **Passage du jeton (Token Passing)**. Une trame spéciale (le jeton) circule sur l'anneau. Seule la station qui possède le jeton peut émettre.
- **Topologie** : Anneau logique, souvent implémenté physiquement en étoile avec un concentrateur spécial appelé **MAU** (Multistation Access Unit).
- **Débits** : 4 ou 16 Mb/s.

### Autres Architectures
- **APPLETALK** : Architecture propriétaire d'Apple, simple à mettre en place (intégrée à Mac OS). Aussi appelé **LocalTalk**.
- **ARCNET** : Ancienne architecture (1977), topologie en bus ou étoile, utilise le passage de jeton.
- **ARPANET** : Ancêtre d'Internet, développé par l'ARPA. Pionnier de la **commutation de paquets**.

## Les Réseaux Étendus (WAN)

### Accès à Distance et Internet
- Un **WAN (Wide Area Network)** connecte des réseaux sur de longues distances.
- **Accès Internet** :
  - Via un **FAI (Fournisseur d'Accès à Internet)** avec des technologies comme l'ADSL.
  - Via une **ligne dédiée** (louée) pour une connexion permanente et garantie.
- **DMZ (Zone Démilitarisée)** : Un sous-réseau isolé entre le réseau interne et Internet pour héberger les serveurs publics (web, mail) et améliorer la sécurité. Le **pare-feu (firewall)** filtre le trafic entre ces zones.

### Caractéristiques et Technologies WAN
- **Protocoles d'accès à distance** : **PPP (Point-to-Point Protocol)** est le standard pour les connexions via lignes téléphoniques (analogiques ou numériques).
- **Modes de transmission** :
  - **Analogique** : via le réseau téléphonique commuté (RTC) avec des modems.
  - **Numérique** : Lignes dédiées (T1, E1), **RNIS** (ISDN).
  - **Commutation de paquets** : Les données sont envoyées en paquets qui peuvent suivre des chemins différents (ex: **X.25**, **Frame Relay**).
- **Technologies WAN notables** :
  - **Relais de trames (Frame Relay)** : Service de commutation de paquets efficace.
  - **ATM (Asynchronous Transfer Mode)** : Technologie à haute vitesse utilisant des cellules de taille fixe.
  - **RNIS (Réseau Numérique à Intégration de Services)** : Permet de transmettre voix et données sur des lignes numériques.
  - **FDDI (Fiber Distributed Data Interface)** : Réseau à 100 Mb/s sur fibre optique, utilisant une topologie en double anneau.

## Gestion et Sécurité des Réseaux

### Protocoles Réseaux
- Une **pile de protocoles** est une combinaison de protocoles qui collaborent (ex: pile TCP/IP).
- **TCP/IP** : Standard d'Internet, routable et très fonctionnel.
  - **TCP (Transmission Control Protocol)** : Fiable, orienté connexion (couche 4).
  - **IP (Internet Protocol)** : Gère l'adressage et le routage (couche 3).
- **SPX/IPX** : Pile propriétaire de Novell NetWare, routable et rapide.
- **NetBEUI** : Protocole léger et rapide de Microsoft, mais **non routable**, adapté aux petits LAN.

### Adressage IP
- **IPv4** : Adresses sur **32 bits**, notées en décimal pointé (ex: `192.168.1.1`).
  - L'adresse est divisée en une **partie réseau** et une **partie station**.
  - Le **masque de sous-réseau** (ex: `255.255.255.0`) définit cette division.
  - **Classes d'adresses** (A, B, C) définissent des tailles de réseau par défaut.
  - **CIDR (Classless Inter-Domain Routing)** : Méthode plus flexible pour allouer les adresses.
- **IPv6** : Nouvelle génération d'adresses sur **128 bits** pour pallier la pénurie d'adresses IPv4.

### Planification, Maintenance et Sécurité
- **Planification** : Essentielle pour anticiper les besoins, choisir les bonnes technologies et maîtriser les coûts (TCO).
- **Maintenance** : Inclut la surveillance des performances, le dépannage et la gestion des sauvegardes.
- **Stratégie de sécurité** :
  - **Contrôle des utilisateurs** : Authentification (login/mot de passe), gestion des droits et permissions.
  - **Contrôle des données** :
    - **Sauvegardes** régulières.
    - **Tolérance de pannes (RAID)** : Utilisation de plusieurs disques pour assurer la redondance des données (RAID 1, RAID 5).
    - **Cryptage** pour protéger la confidentialité.
  - **Contrôle du matériel** : Protection physique des serveurs, alimentation de secours (**UPS**).

### Systèmes d'Exploitation Réseaux (NOS)
- Gère les ressources du réseau, la sécurité et l'accès des utilisateurs.
- Caractéristiques clés : **multitâche** (préemptif ou coopératif), support multiprocesseur.
- Composants :
  - **Redirecteur** (côté client) : Intercepte les requêtes et les dirige vers le réseau.
  - **Service** (côté serveur) : Accepte et traite les requêtes des clients.
- **Exemples** :
  - **UNIX/Linux** : Très robuste, stable et multi-utilisateurs. Protocole natif : TCP/IP.
  - **Novell NetWare** : Très performant pour le partage de fichiers/imprimantes. Protocole historique : SPX/IPX. Introduit les services d'annuaire (NDS).
  - **Windows NT/Server** : Intégration forte avec l'écosystème Microsoft, interface graphique conviviale, gestion par **domaines**.
  - **OS/2** : Développé par IBM, moins répandu.

## Programmation PHP

### Structures de Contrôle
- **Conditions** :
  - `if...else` : Exécute du code si une condition est vraie.
  - `switch` : Compare une variable à plusieurs valeurs possibles.
- **Boucles** :
  - `for` : Répète un bloc de code un nombre de fois défini.
  - `while` : Répète tant qu'une condition est vraie (test en début de boucle).
  - `do...while` : Répète tant qu'une condition est vraie (test en fin de boucle, s'exécute au moins une fois).
  - `foreach` : Parcourt les éléments d'un tableau.
- **Instructions de rupture** :
  - `break` : Sort d'une boucle ou d'un `switch`.
  - `continue` : Passe à l'itération suivante d'une boucle.

```php
// Exemple : Tester si un nombre est multiple de 3 et de 5
$x = 15;
if ($x % 3 == 0 && $x % 5 == 0) {
    echo "$x est multiple de 3 et de 5";
} else {
    echo "$x n'est pas multiple de 3 et de 5";
}

// Exemple : Boucle foreach pour un tableau
$tab = array("un" => 1, "deux" => 2);
foreach ($tab as $cle => $valeur) {
    echo "Clé : $cle, Valeur : $valeur\n";
}
```

### Chaînes de Caractères
- **Déclaration** : Entre guillemets simples (`' '`) ou doubles (`" "`). Les guillemets doubles interprètent les variables et les caractères spéciaux (`\n`).
- **Concaténation** : Avec l'opérateur `.` (point).
- **Fonctions utiles** :
  - `strlen()` : Longueur de la chaîne.
  - `strtolower()`, `strtoupper()` : Convertir en minuscules/majuscules.
  - `trim()` : Supprimer les espaces en début et fin.
  - `substr()` : Extraire une sous-chaîne.
  - `htmlspecialchars()` : Convertir les caractères spéciaux en entités HTML.

### Tableaux (Arrays)
- **Déclaration** : `array()` ou `[]` (depuis PHP 5.4).
- **Types** :
  - **Scalaires (indexés)** : Les clés sont des entiers (`0, 1, 2, ...`).
  - **Associatifs** : Les clés sont des chaînes de caractères.
- **Fonctions utiles** :
  - `count()` : Nombre d'éléments.
  - `sort()` : Trie les valeurs.
  - `asort()` : Trie les valeurs en conservant les clés.
  - `ksort()` : Trie par clés.
  - `in_array()` : Vérifie si une valeur existe dans le tableau.

### Formulaires HTML
- **Récupération des données** :
  - Les données envoyées via un formulaire sont accessibles dans les tableaux superglobaux `$_GET` (méthode GET) ou `$_POST` (méthode POST).
- **Transfert de fichiers** :
  - Utilise `<input type="file">` et `enctype="multipart/form-data"`.
  - Les informations sur le fichier sont dans le tableau superglobal `$_FILES`.
  - La fonction `move_uploaded_file()` déplace le fichier du répertoire temporaire vers sa destination finale.

### Gestion des Fichiers, Cookies et Sessions
- **Inclusion de fichiers** :
  - `include()` : Inclut et évalue un fichier. Génère une alerte en cas d'erreur.
  - `require()` : Identique à `include()`, mais génère une erreur fatale si le fichier est introuvable.
  - `include_once()`, `require_once()` : S'assurent que le fichier n'est inclus qu'une seule fois.
- **Cookies** :
  - Petits fichiers stockés sur le **client**.
  - Créés avec `setcookie()`. Doit être appelée avant toute sortie HTML.
  - Données accessibles via le tableau superglobal `$_COOKIE`.
- **Sessions** :
  - Données stockées sur le **serveur**, associées à un identifiant unique (ID de session) transmis au client (souvent via un cookie).
  - Permet de conserver des informations entre les pages.
  - Démarrées avec `session_start()`.
  - Données accessibles via le tableau superglobal `$_SESSION`.

## Langage SQL et phpMyAdmin

### Introduction aux SGBDR et à MySQL
- **SGBDR** : Système de Gestion de Bases de Données Relationnelles. Organise les données dans des tables liées par des relations.
- **SQL (Structured Query Language)** : Langage standard pour interagir avec les SGBDR.
- **MySQL** : Un des SGBDR les plus populaires, souvent utilisé avec PHP.
- **phpMyAdmin** : Interface web pour administrer des bases de données MySQL.

### Création et Modification
- **Créer une base de données** : `CREATE DATABASE nom_base;`
- **Créer une table** : `CREATE TABLE nom_table (colonne1 type, colonne2 type, ...);`
- **Modifier une table** : `ALTER TABLE nom_table ADD colonne type;` (ajouter), `DROP colonne` (supprimer), `CHANGE ...` (modifier).
- **Types de données courants** :
  - **Numériques** : `TINYINT`, `INT`, `BIGINT`, `FLOAT`, `DOUBLE`.
  - **Chaînes** : `CHAR(M)`, `VARCHAR(M)`, `TEXT`, `BLOB`.
  - **Dates/Heures** : `DATE`, `DATETIME`, `TIMESTAMP`, `TIME`.

### Manipulation de Données (DML)
- **Insertion** : `INSERT INTO nom_table (col1, col2) VALUES (val1, val2);`
- **Modification** : `UPDATE nom_table SET col1 = val1 WHERE condition;`
- **Suppression** : `DELETE FROM nom_table WHERE condition;`
- **Sélection** : `SELECT colonnes FROM nom_table WHERE condition ORDER BY colonne ASC/DESC;`
  - `*` sélectionne toutes les colonnes.
  - `DISTINCT` supprime les doublons.
  - **Clause `WHERE`** : Filtre les résultats.
    - Opérateurs : `=`, `!=`, `>`, `<`, `BETWEEN`, `LIKE '%motif%'`, `IN (val1, val2)`.
    - Opérateurs logiques : `AND`, `OR`, `NOT`.
  - **Fonctions d'agrégation** : `COUNT()`, `SUM()`, `AVG()`, `MAX()`, `MIN()`.
  - **Clause `GROUP BY`** : Regroupe les lignes pour appliquer des fonctions d'agrégation.
  - **Jointures (`JOIN`)** : Combine les lignes de deux ou plusieurs tables basées sur une colonne commune.
    - `SELECT * FROM table1 JOIN table2 ON table1.id = table2.fk_id;`

### Connexion à MySQL avec PHP
- **Connexion** : `mysql_connect("host", "user", "pass");` (obsolète, utiliser **PDO** ou **MySQLi**).
- **Sélection de la base** : `mysql_select_db("nom_base");`
- **Exécution d'une requête** : `$result = mysql_query("VOTRE REQUETE SQL");`
- **Lecture des résultats** :
  - `mysql_fetch_array($result)` : Récupère une ligne sous forme de tableau (associatif et numérique).
  - `mysql_fetch_assoc($result)` : Récupère une ligne sous forme de tableau associatif.
  - `mysql_num_rows($result)` : Nombre de lignes dans le résultat.

## Introduction à la Cartographie et au WebMapping (SIG)

### Définitions Clés
- **Cartographie** : L'art et la science de l'élaboration de cartes.
- **Carte** : Représentation graphique du monde réel permettant de localiser des objets et phénomènes.
- **SIG (Système d'Information Géographique)** : Système informatique conçu pour collecter, gérer, analyser et afficher des données à référence spatiale.

### WebMapping
- **Définition** : Processus de diffusion de cartes sur un réseau (Internet, Intranet).
- **Architecture Client/Serveur** :
  - **Côté Serveur** : Un serveur cartographique génère les cartes (souvent des images) à la demande et les envoie au client. Le client n'a besoin que d'un navigateur web.
  - **Côté Client** : Le navigateur télécharge une application (Applet Java, ActiveX) pour gérer l'interactivité (zoom, déplacement) et afficher des données complexes (vecteur).
  - **Hybride** : Combine les deux approches pour un meilleur équilibre entre performance et fonctionnalités.

### Information Géographique
- **Composantes** :
  - **Attributaires** : Données descriptives (nom, population, etc.).
  - **Graphiques (Spatiales)** : Données de localisation.
- **Modes de représentation** :
  - **Mode Raster (Matriciel)** : L'espace est divisé en une grille de pixels (ex: photos aériennes, images satellite - JPEG, PNG). La qualité se dégrade avec le zoom.
  - **Mode Vecteur** : Les objets sont représentés par des primitives géométriques (points, lignes, polygones) définies par des coordonnées. Qualité conservée au zoom (ex: SVG, Shapefile).
- **Bases de données géographiques** : SGBD étendus pour stocker et interroger des données spatiales (ex: **PostGIS** pour PostgreSQL).
- **Normes** : L'**OGC (Open Geospatial Consortium)** développe des standards pour assurer l'interopérabilité des données et services géospatiaux.