# Feedback #3
## Execution du projet
  
 Lancement : attention à la présence d'un fichier .htaccess à la racine du /public afin de permettre aux routes de fonctionner correctement sans devoir passer par la case configuration au niveau serveur. Ainsi la configuration de l'applicatif le suivra peux importe le serveur sur lequel il sera déployé.
Par défaut le premier lancement de l'application affiche une 404. En effet la route par défaut est /home et non /
Seuls les liens "Profs" et "Etudiants" fonctionne dans le menu. Tous les autres liens sont en 404. Les pages "Profs" et "Etudiants" affiche une vue incomplète, en effet il semble que le layout global du site (header / footer / menu / ... ) en soit complètement absent. 	
  
## Structure du projet / code
public/index.php : attention aux "use" inutiles. Par exemple "App\Controllers\ErrorController" est inutile.

CoreController : pourquoi faire un "global \\$router" dans l'action show(), alors qu'il n'est pas utilisé ? 

StudentController : attention à l'indentation au niveau des lignes 35 à 37.
  
TeacherController : attention au copier/coller. Une fonction studentAdd() existe dans ce controller et est identique à celui présent dans le StudentController. Celà pourrait avoir des effets de bords très négatifs. 

Models : 
- il manque une propriété au CoreModel.php qui serait un protected int $id, nécessaire à chaque entrée afin de pouvoir l'identifier simplement en base de données. Vu qu'il sera commun aux entités présentes, il n'est pas nécessaire de l'indiquer sur les autres models mais de le centraliser sur cette classe. 
- Student : enlever la propriété \\$id après l'avoir rajoutée sur le CoreModel
- Student & Teacher : aucun typage des propriétés n'est présent. Plus la définition de l'ensemble des propriétés d'une classe est complète, plus les erreurs de paramètres ou de gestion des valeurs seront réduites. Il est de même pour les valeurs des variables pour les fonctions set() et des valeurs de retour des fonctions get()

Views : le découpage global des vues est à revoir. En effet plusieurs erreurs y sont présentes. Il est nécessaire de découper la partie "header", "contenu du site" et "footer". Car le header et footer vont être présent sur chacunes des pages, ainsi si le header et footer sont dans des fichiers séparés, il sera alors juste nécessaire de les appeller sur chacunes des vues, plutôt que de répéter l'ensemble du code HTML à chaque vue. Car si nous avons besoin de modifier le menu par exemple sur une seule entrée, il faudra le faire sur l'ensemble des fichiers de vues. Ce qui n'est pas optimal pour la suite du développement, et sa maintenabilité. Les assets, en l'occurence le fichier style.css est appelé avec un chemin absolu "./" donc ne sera valable que pour la page d'accueil. Alors qu'une variable \\$assetsBaseUri existe dans le MainController, c'est bête de ne pas l'utiliser partout dans les vue lorsque cela est nécessaire afin d'appeler les assets de façon plus dynamique et fonctionnelle partout peux importe le chemin sur lequel on se trouve.  
Attention aux liens de retour dans les formulaires d'ajouts, ils sont en dur dans le code, alors que la fonction $router->generate est bien présente quelques lignes plus bas, le bouton "Ajouter" sur la page TeacherList mêne à l'ajout d'un Student. 


## Routes
  
Le fichier index.php du répertoire public/ pourrait être allégé pour ne garder que de l'execution "centralisé". Rien n'empêche de mettre ce genre de configuration dans un fichier à part et de l'inclure au moment du "match()" de la route courante

## Avis global

La structure du projet sur la partie MVC PHP est très bien (gestion de variables globales aux vues pour les assets, liens & urls par exemple). Manque un typage afin d'obtenir des données plus qualitatives sur les Models.     
Petite note également pour les "var_dump" laissés en tant que message d'erreur. Il faudrait soit générer une erreur correcte à l'utilisateur, soit enlever les var_dump. 
Par contre sur la partie intégration et vues, le découpage est à revoir, car l'état actuel ne permet pas vraiment une utilisation et navigation aisée du projet , et va provoquer également des bugs très rapidement ainsi qu'une confusion pour la suite. Peux être moins à l'aise sur la partie HTML / CSS ? Ou comment réaliser le découpage ? 

Tout ce qui est "configuration" de l'application, ne pas hésiter à le mettre dans un fichier de configuration à part : config.ini, fichier.php séparé, ... Ainsi les évolutions et changements seront grandement facilités par la suite. 

Au niveau du fichier .gitignore, ne pas exclure le fichier config.ini de configuration d'accès à la base de données va créer des soucis de déploiement de l'application et de sécurité (Identifiants en clair inscrit en dur), il est possible de mettre un fichier config.ini.example ou config.ini.dist comme base et mettre dans le fichier config.ini les identifiants de la machine où fonctionne l'application et donc ne pas l'oublier dans le .gitignore. Ainsi pour chaque déploiement, il suffira de copier le fichier de configuration mis en example, et de ne modifier que les valeurs propre à l'environnement.





