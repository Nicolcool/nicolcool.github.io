---
title: update-one
layout: default
nav_order: 4
parent: IngredientCategory
---

Admin
{: .label .label-red }

<!-- DÉBUT DE LA ROUTE -->
# update-one
----

> Modifie un document `IngredientCategory` existant avec de nouvelles valeurs.

## Requête

{: .request-put }
> https://api.sharlotte.fr/admin/ingredientcats/*_id*

## Paramètres

| Paramètres | Valeurs                                                       |
|:-----------|:--------------------------------------------------------------|
| *_id*      | identifiant unique du document `IngredientCategory` recherché |

## Body
{% capture _code %}{% highlight json linenos %}
{
    "name": "Nouveau nom",
    "description":"Nouvelle description"
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

## Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6462cc280d8c1c3efd0b43d2",
    "name": "Nouveau nom",
    "description":"Nouvelle description"
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