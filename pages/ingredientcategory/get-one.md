---
title: get-one
layout: default
nav_order: 2
parent: IngredientCategory
---

Public
{: .label .label-green }

<!-- DÉBUT DE LA ROUTE -->
# get-one
----

> Renvoie les informations d'un seul document `IngredientCategory` depuis son identifiant unique.

## Requête

{: .request-get }
> https://api.sharlotte.fr/ingredientcats/*_id*

## Paramètres

| Paramètres | Valeurs                                                       |
|:-----------|:--------------------------------------------------------------|
| *_id*      | identifiant unique du document `IngredientCategory` recherché |

## Body
*Aucun contenu n'est nécessaire*

## Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6460eb105983b6a7ad04f467",
    "name": "Viandes",
    "description": "Eum et et minima soluta eos molestiae earum molestias. Illo velit veniam et unde placeat et dolorem reprehenderit."
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

[Ingredient]: ingredient.html
[get-all]: #get-all
[get-one]: #get-one
[create-one]: #create-one
[update-one]: #update-one
[delete-one]: #delete-one