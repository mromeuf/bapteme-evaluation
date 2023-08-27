# Fetch

## Explication de la méthode Fetch JS

La méthode Fetch en Javascript permet de créer une requête HTTP afin de questionner une ressource, comme une API distante par exemple, une image, ...  Ainsi avec cette méthode il est facile de réaliser un site avec un affichage dynamique avec un retour en live des données.   

Par exemple dans un cas concret, on souhaite créer un bouton rafraichir la liste sur la liste des professeurs sans devoir rafraichir la page. Nous allons donc créer du code Javascript en utilisant la méthode fetch afin de récupérer la liste (qui pourrait être sous un format de retour/d'affichage dit JSON pour le plus répandu), et dès que la requête qui nous donne la liste est réalisée, nous avons donc tous les résultats souhaités et nous avons plus qu'à les récupérer et les traiter pour les afficher sur la page. 

## Cas concret

Si par exemple nous souhaitons récupérer le retour de l'url /teachers : 

```
// Nous demandons à la méthode fetch() d'aller récupérer l'url /teachers
fetch("/teachers")
    // Une fois que la requête HTTP est finalisée, le retour est dans le paramètre response
    // L'objet en paramètre peux comporter plusieurs propriétés dont la liste est ici : https://developer.mozilla.org/fr/docs/Web/API/Response
    .then(function (response) {
        if (response.ok) { // Dans notre cas on va juste regarder si la requête s'est bien déroulée par le response.ok
            console.log(response.text()); // Permet de récupérer la valeur de retour par le response.text(), ici on va juste l'afficher dans la console
        } else {
            console.log("Mauvaise réponse du réseau"); // Si la requête s'est mal déroulée, on va afficher une erreur dans la console
        }
    })
    // Nous allons récupérer toutes les erreurs provenant de notre méthode fecth() et les indiquer dans la console du navigateur afin de
    // pouvoir debugguer notre code facilement
    .catch(function (error) {
        console.log("Erreur avec fetch : " + error.message);
    });
```