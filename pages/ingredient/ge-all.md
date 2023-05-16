---
title: get-all
layout: default
nav_order: 1
parent: Ingredient
---

Public
{: .label .label-green }

User
{: .label .label-yellow }

Admin
{: .label .label-red }

<!-- DÉBUT DE LA ROUTE -->
# get-all
----

> Renvoie la liste de tous les `Ingredient` qui existent en base de données et qui sont réglés en confidentialité `PUBLIC`. Renvoie également tous les autres ingrédients accessibles à l'utilisateur authentifié.


## Requête

{: .request-get }
> https://api.sharlotte.fr/ingredients

{: .request-get }
> https://api.sharlotte.fr/ingredients?page=1&limit=20
> 
> *renvoie les 20 premiers résultats*

{: .request-get }
> https://api.sharlotte.fr/ingredients?page=2&limit=20
> 
> *renvoie les résultats 21 à 40*

{: .request-get }
> https://api.sharlotte.fr/ingredients?search=jambon
> 
> *renvoie tout les résultats qui correspondent à la recherche, classés par ordre de correspondance*

## Paramètres

| Paramètres | Valeurs                                           |
|:-----------|:--------------------------------------------------|
| limit      | nombre de résultats affichés par page de réponses |
| page       | numéro de la page de réponses à afficher          |
| search     | phrase de recherche                               |

## Body
*Aucun contenu n'est nécessaire*

## Réponse
{% capture _code %}{% highlight json linenos %}
[{
    "id": "6460eb105983b6a7ad04f471",
    "name": "Jambon blanc, cuit",
    "slug": "jambonblanccuit",
    "category": {
        "id": "6460eb105983b6a7ad04f467",
        "name": "Viandes"
    },
    "calories": 301,
    "proteins": 12.16,
    "carbohydrates": 19.88,
    "sugars": 49.18,
    "fats": 29.38,
    "saturates": 26.5,
    "salt": 16.03,
    "owner": {
        "id": "6460eb0f5983b6a7ad04f464",
        "email": "shop1@brand.cool"
    },
    "privacy": "PRIVATE",
    "instructions": []
},
[...]
]
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->

# Routes

1. [get-all]
1. [get-one]
1. [create-one]
1. [update-one]
1. [delete-one]

----

[Product]: user/produit.html
[IngredientCategory]: ingredientcategory.html
[Security]: security.html
[User]: user/index.html
[get-all]: #get-all
[get-one]: #get-one
[create-one]: #create-one
[update-one]: #update-one
[delete-one]: #delete-one