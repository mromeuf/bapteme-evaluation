# Feedback #2
## Execution du projet
  
Lancement : OK    
Présence du fichier .htaccess permettant d'avoir la configuration pour la lecture des routes.   
Il semblerait qu'il n'y ai pas de gestion de l'utilisateur connecté, le menu en haut affiche un état "connecté" sans aucune action de connexion. 
  
## Structure du projet / code
  
CoreController : pourquoi faire un "global \\$router" dans l'action show(), alors qu'il n'est pas utilisé ? 
TeachersController : attention à l'indentation du code, la fonction add() devrait être au même niveau que la fonction list()

Il est mieux de mettre les catégories que vont gérer les Controller au singulier, car ils peuvent en gérer plusieurs en effet mais aussi un seul (un get() par exemple). TeachersController serait donc TeacherController et StudentsController serait StudentController

Models : seules les propriétés de CoreModel sont typées, les autres Models n'ont aucune propriétés typées. Plus la définition de l'ensemble des propriétés d'une classe est complète, plus les erreurs de paramètres ou de gestion des valeurs seront réduites. Il est de même pour les valeurs des variables pour les fonctions set() et des valeurs de retour des fonctions get()

Views : 
- layout/header.tpl.php : attention à l'url d'accès au fichier style.css, il ne sera valable que si nous sommes sur la page d'accueil à cause du "./", l'idéal étant d'utiliser une variable qui sera globale (exemple fichier de configuration) et l'indiquer avant chaque ressources appelées. Cette valeur peux être également dynamique en fonction des valeurs du $_SERVER.
  
## Fonctionnement Global 
  
Il est dommage de ne pas avoir un Controller complet, pourquoi avoir créer Students et Teachers mais non finalisé ? Il est préférable de se focaliser sur un élément à la fois, plutôt que gérer plusieurs catégories en même temps. Ainsi il est plus aisé d'y travailler et d'avancer, la concentration restant sur le même élément.
  
## Routes
  
Le fichier index.php du répertoire public/ pourrait être allégé pour ne garder que de l'execution "centralisé". Rien n'empêche de mettre ce genre de configuration dans un fichier à part et de l'inclure au moment du "match()" de la route courante
  
## Avis global
  
C'est dommage de ne pas s'être focalisé que sur une seule catégorie Student ou Teacher et donc de pas en avoir une plus complète. Par exemple se focaliser sur Teacher permettait de définir la structure complète d'un Controller type qu'il aurait été aisé de dupliquer pour Student après en modifiant ce qui était nécessaire. Peux être réussir à se focaliser sur une partie à la fois, ou un autre blocage n'a pas permis de réaliser plus de développements ? 
  




