# Feedback #4
## Execution du projet
  
 Lancement : attention à la présence d'un fichier .htaccess à la racine du /public afin de permettre aux routes de fonctionner correctement sans devoir passer par la case configuration au niveau serveur. Ainsi la configuration de l'applicatif le suivra peux importe le serveur sur lequel il sera déployé.
Par défaut le premier lancement de l'application affiche une page blanche. En effet la route par défaut est / qui est censée mener au Controller MainController mais n'est pas présent dans l'architecture du site. 	 
  
## Structure du projet / code
Attention à la nomenclature des dossiers., en effet le dossier "App" devrait être "app". 

StudentsController : 
- la classe est censée étendre la classe "CoreController" mais est absente.
- manque un ; ligne 19
- ligne 20 : students(); est une fonction qui n'est pas déclarée
- ligne 21 : $studentsdModel est un variable qui n'est définie nulle part
- ligne 42 : Studentss est un Model qui n'existe pas
- et plusieurs autres erreurs encore de variables non déclarées mais utilisées comme si elles l'étaient.

Attention à bien relire le code. 

TeacherController : même remarque que StudentsController, beaucoup d'erreurs de variables utilisées mais non définies. Soucis d'indentation de l'ensemble du fichier.

UserController : la classe est censée étendre la classe "CoreController" mais est absente.

Models : 
- Students & Teachers : aucun typage des propriétés n'est présent. Plus la définition de l'ensemble des propriétés d'une classe est complète, plus les erreurs de paramètres ou de gestion des valeurs seront réduites. Il est de même pour les valeurs des variables pour les fonctions set() et des valeurs de retour des fonctions get()  Alors que cette partie est très bien sur le model AppUser

Views : 
- main/home.tpl.php : attention à l'url d'accès au fichier style.css, il ne sera valable que si nous sommes sur la page d'accueil à cause du "./", l'idéal étant d'utiliser une variable qui sera globale (exemple fichier de configuration) et l'indiquer avant chaque ressources appelées. Cette valeur peux être également dynamique en fonction des valeurs du $_SERVER.
- Pour les vues d'ajout et d'édition qui sont semblables en tout point sauf que dans un formulaire nous avons des valeurs vides et l'autre où des valeurs par défauts sont définies, il est possible de n'utiliser qu'une seule vue plutot que 2 et juste de renseigner au niveau du value="" la valeur si elle est renseignée (ex : value="<?=(isset(\\$$teacher))?\\$teacher->getFirstName:''")


## Routes
  
Le fichier index.php du répertoire public/ pourrait être allégé pour ne garder que de l'execution "centralisé". Rien n'empêche de mettre ce genre de configuration dans un fichier à part et de l'inclure au moment du "match()" de la route courante

## Avis global

Aucun lancement du projet est possible en l'état. En effet de nombreux élements nécessaire au bon fonctionnement de l'architecture MVC sont manquants. Attention à la nomenclature des dossiers avec des majuscules.   
Cela traduit un projet assez brouillon sur la structure principal nécessaire au bon fonctionnement de l'application. Il serait nécessaire de revoir le fonctionnement et l'utilisation du MVC afin de mieux comprendre comment il fonctionne et avec quels éléments.  
Outre la partie fonctionnement applicatif, il manque également une lecture du code (; manquant, variable utilisées mais non définies, ...).

Au niveau du fichier .gitignore, ne pas exclure le fichier config.ini de configuration d'accès à la base de données va créer des soucis de déploiement de l'application et de sécurité (Identifiants en clair inscrit en dur), il est possible de mettre un fichier config.ini.example ou config.ini.dist comme base et mettre dans le fichier config.ini les identifiants de la machine où fonctionne l'application et donc ne pas l'oublier dans le .gitignore. Ainsi pour chaque déploiement, il suffira de copier le fichier de configuration mis en example, et de ne modifier que les valeurs propre à l'environnement.





