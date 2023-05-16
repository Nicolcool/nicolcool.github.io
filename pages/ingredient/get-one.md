---
title: get-one
layout: default
nav_order: 2
parent: Ingredient
---

Public
{: .label .label-green }

User
{: .label .label-yellow }

Admin
{: .label .label-red }

<!-- DÉBUT DE LA ROUTE -->
# get-one
----

> Renvoie les informations d'un seul document `Ingredient` depuis son identifiant unique, à condition que l'utilisateur authentifié y ai les droits d'accès si l'ingrédient n'est pas réglé en confidentialité `PUBLIC`.


## Requête

{: .request-get }
> https://api.sharlotte.fr/ingredients/*_id*

## Paramètres

| Paramètres | Valeurs                                               |
|:-----------|:------------------------------------------------------|
| *_id*      | identifiant unique du document `Ingredient` recherché |

## Body
*Aucun contenu n'est nécessaire*

### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6460eb105983b6a7ad04f472",
    "name": "Pâte brisée",
    "slug": "patebrisee",
    "category": {
        "id": "6460eb105983b6a7ad04f468",
        "name": "Pâtes et fonds"
    },
    "calories": 313,
    "proteins": 27.53,
    "carbohydrates": 3.91,
    "sugars": 6.02,
    "fats": 19.82,
    "saturates": 29.58,
    "salt": 39.59,
    "owner": {
        "id": "6460eb0f5983b6a7ad04f464",
        "email": "shop1@brand.cool"
    },
    "privacy": "PRIVATE",
    "instructions": [
        "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
        "Vestibulum eget ex sed tortor rutrum vestibulum.",
        "Vivamus laoreet nunc molestie, sodales odio tempus, lobortis lorem."
    ]
}
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