---
title: get-all
layout: default
nav_order: 1
parent: IngredientCategory
---

Public
{: .label .label-green }

<!-- DÉBUT DE LA ROUTE -->
# get-all
----

> Renvoie la liste de tous les `IngredientCategory` qui existent en base de données.

## Requête

{: .request-get }
> https://api.sharlotte.fr/ingredientcats

## Paramètres
*Aucun contenu n'est nécessaire*

## Body
*Aucun contenu n'est nécessaire*

## Réponse
{% capture _code %}{% highlight json linenos %}
[{
    "id": "6460eb105983b6a7ad04f467",
    "name": "Viandes",
    "description": "Eum et et minima soluta eos molestiae earum molestias. Illo velit veniam et unde placeat et dolorem reprehenderit."
},
{
    "id": "6460eb105983b6a7ad04f468",
    "name": "Fromages",
    "description": "Doloremque quod qui neque consequatur. Nam facere sed reprehenderit exercitationem ut mollitia quo fugit. Fuga iste perferendis quod tenetur ut consequatur ut eos."
}]
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->

# Routes

1. [get-all]
1. [get-one]
1. [create-one]
1. [update-one]
1. [delete-one]

----

[get-all]: get-all.html
[get-one]: get-one.html
[create-one]: create-one.html
[update-one]: update-one.html
[delete-one]: delete-one.html