---
title: create-one
layout: default
nav_order: 3
parent: Ingredient
---

User
{: .label .label-yellow }

<!-- DÉBUT DE LA ROUTE -->
## create-one
----

> Créer et ajoute un document `Ingredient` à la base de données.


### Requête

{: .request-post }
> https://api.sharlotte.fr/ingredients

### Paramètres
*Aucun contenu n'est nécessaire*

### Body
{% capture _code %}{% highlight json linenos %}
{
    "name":"Nouvel ingrédient",
    "category":"644fbb9215f67a77ac0515d7",
    "privacy":"PUBLIC"
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

{: .note }
> Les champs optionels peuvent être omis de la requête.
> Le champs `slug` est traité automatiquement par le serveur à partir du champs `name`.
> Le champ `owner` est traité automatiquement par le serveur à partir de l'utilisateur authentifié.

### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6460eb105983b6a7ad04f472",
    "name": "Nouvel ingrédient",
    "slug": "nouvelingredient",
    "category": {
        "id": "644fbb9215f67a77ac0515d7",
        "name": "Catégorie d'ingrédients"
    },
    "owner": {
        "id": "6460eb0f5983b6a7ad04f464",
        "email": "shop1@brand.cool"
    },
    "privacy": "PUBLIC"
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

[get-all]: get-all.html
[get-one]: get-one.html
[create-one]: create-one.html
[update-one]: update-one.html
[delete-one]: delete-one.html