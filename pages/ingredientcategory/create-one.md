---
title: create-one
layout: default
nav_order: 3
parent: IngredientCategory
---

Admin
{: .label .label-red }

<!-- DÉBUT DE LA ROUTE -->
# create-one
----

> Créer et ajoute un document `IngredientCategory` à la base de données.

## Requête

{: .request-post }
> https://api.sharlotte.fr/admin/ingredientcats

## Paramètres
*Aucun contenu n'est nécessaire*

## Body
{% capture _code %}{% highlight json linenos %}
{
    "name":"Nouvelle catégorie",
    "description":"Lorem ipsum dolor sit amet, consectetur adipiscing elit."
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

## Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6462cc280d8c1c3efd0b43d2",
    "name": "Nouvelle catégorie",
    "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit."
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