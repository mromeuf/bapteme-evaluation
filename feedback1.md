# Feedback #1
## Execution du projet
  
 Lancement : OK attention à la présence d'un fichier .htaccess à la racine du /public afin de permettre aux routes de fonctionner correctement sans devoir passer par la case configuration au niveau serveur. Ainsi la configuration de l'applicatif le suivra peux importe le serveur sur lequel il sera déployé.
  
## Structure du projet
La structure globale est correcte, les assets par contre ne se chargeront pas. En effet dans le header.tpl.php le fichier css/style.css est chargé mais ne correspond à aucun fichier et dossier dans le dossier public/. copier/coller trop rapide ?
Sur les Models, seules les propriétés de CoreModel sont typées, les autres Models n'ont aucune propriétés typées, est-ce un oubli ? Plus la définition de l'ensemble des propriétés d'une classe est complète, plus les erreurs de paramètres ou de gestion des valeurs seront réduites. 

## Fonctionnement Global 
  
- Login : OK 
- Logout : OK
- Section Prof
	- Liste : OK 
    - Ajout : OK 
    - Edition : OK
    - Suppression : OK (Attention au "Oups" il y a une erreur Javascript)
- Section Etudiants
    - Liste : OK
    - Edition : OK
    - Ajout : OK
    - Suppression : KO Attention la route de suppression ne correspond pas à la route qui gère la suppression et donc est en 404
- Section Utilisateur
    - Liste : OK 
    - Ajout : KO (Aucune action lorsqu'on clique sur le bouton)
    - Edition : KO (Aucune action lorsqu'on clique sur le bouton)
    - Suppresion : KO  (404)

## Gestion de l'authentification
Lors de l'authentification de la personne, seulement son Id Utilisateur et son rôle sont mis en session. Pourquoi ne pas sauvegarder l'utilisateur complet en session en y mettant directement $_SESSION['user] = $user ? Ainsi nous pourront accèder à l'ensemble des informations de l'utilisateur partout sans devoir effectuer des requêtes supplémentaires plusieur fois ? Ainsi l'application pourrait gagner en performance.   
Pour les rôles pourquoi avoir centralisé les accès dans une classe CoreController ? Dès lors qu'une modification sera nécessaire pour de nouveaux paramètres, il faudra modifier ce dernier. Cela est en effet centralisé, mais étant une "configuration" de l'application, l'idéal serait de le mettre dans une fichier de configuration à part. 

## Routes
Toutes les routes d'atterrissage sont sous la forme "Controller/" sauf pour la liste des utilisateurs dont la page d'accueil est "students/list". Le mieux est d'avoir une cohérence entre l'ensemble des routes et de leurs actions.
Le fichier index.php du répertoire public/ pourrait être allégé pour ne garder que de l'execution "centralisé". Rien n'empêche de mettre ce genre de configuration dans un fichier à part et de l'inclure au moment du "match()" de la route courante. 

## Avis global
L'ensemble de l'execution semble cohérent, attention à la petite incohérence au niveau des routes pour le controller Students par rapport aux autres routes définies. 

Tout ce qui est "configuration" de l'application, ne pas hésitez à le mettre dans un fichier de configuration à part : config.ini, fichier.php séparé, ... Ainsi les évolutions et changements seront grandement facilités par la suite. 

Lors de la mise en place des vues, bien vérifier que les assets sont bien mis dans le dossier public/ ainsi que bien modifier les chemins d'accès, sinon ils ne pourront se charger.  

Au niveau du fichier .gitignore, ne pas exclure le fichier config.ini de configuration d'accès à la base de données va créer des soucis de déploiement de l'application et de sécurité (Identifiants en clair inscrit en dur), il est possible de mettre un fichier config.ini.example ou config.ini.dist comme base et mettre dans le fichier config.ini les identifiants de la machine où fonctionne l'application et donc ne pas l'oublier dans le .gitignore. Ainsi pour chaque déploiement, il suffira de copier le fichier de configuration mis en example, et de ne modifier que les valeurs propre à l'environnement.





