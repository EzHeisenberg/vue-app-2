# newsfrance

- **Dernières news** : https://ezheisenberg.github.io/vue-app-2/#/
- **Rechercher une catégorie** : https://ezheisenberg.github.io/vue-app-2/#/search




API utilisée : ```https://api.currentsapi.services/v1/```

----

### Endpoint disponible

|methode | Route | Description |
|:---: | :---: | :---:|
| GET | /search | Search query results |
| GET | /latest-news | Get the latest news by language |
| GET | /available/languages | Valid language code |
| GET | /available/regions | Valid country region code |
| GET | /available/category | Valid category code |


# Problèmatique

- **L'API** n'a pas d'`` Endpoint`` afin de récupérer un article par un **ID**

Le problème de ne pas avoir un lien pour faire une requête GET et passer en paramètre un ID 
(Exemple : https://api.currentsapi.services/v1/search?id=7YSH-8AIJJbfr7-0kstzT)
fait qu'il m'est impossible de récupérer une News spécifique


## Optimisation 

- Mettre en cache les **DATA** récupérées = moins de requêtes sur l'API.
- Mettre un bouton *refresh* pour faire une nouvelle requête.
