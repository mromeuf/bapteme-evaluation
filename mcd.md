## Retour MCD

"Un utilisateur peut créer sur son compte une ou plusieurs adresses de livraison" : 

OK :  un utilisateur peux avoir en effet 0 ou N adresse, et une adresse aura forcément qu'un seul utilisateur en face. 

"Un utilisateur peux liker un produit ou plusieurs"

Non respecté : dans le cas actuel 1 seul utilisateur ne pourra liker qu'un seul produit, et un seul produit ne pourra avoir qu'un seul like d'un seul utilisateur. Il faudra revoir cette relation en   
USER - 0,N - LIKE - 0,N - PRODUCT

Ainsi un utilisateur peux liker 0 produit comme plusieurs, et un produit pourra également avoir 0 utilisateurs qui ont liké comme N. 

"Un utilisateur peut aussi passer une commande sur un produit"

OK : l'entité ORDER doit bien comporter au moins un produit et un produit peux avoir 0 ou N entité ORDER associée. 


Par contre, si l'utilisateur a plusieurs adresses de livraison, il faudra peux être créer une nouvelle association à une des adresses à l'entité ORDER afin de savoir où envoyer la commande. 



Voici quelques outils qui te permettront de créer facilement d'autres MCD au besoin  : 
https://app.diagrams.net/
ou encore https://www.mysql.com/products/workbench/ 
