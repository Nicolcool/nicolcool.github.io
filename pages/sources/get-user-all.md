---
title: get-user-all
layout: default
nav_order: 1
parent: Sources
---

PUBLIC
{: .label .label-green }

<!-- DÉBUT DE LA ROUTE -->
# get-user-all
----

> Renvoie la liste de tous les `Units` qui existent en base de données pour l'utilisateur authentifié.

## Requête

{: .request-get }
> https://api.sharlotte.fr/users/units

## Paramètres
*Aucun paramètre n'est nécessaire*

## Body
*Aucun contenu n'est nécessaire*

## Réponse
{% capture _code %}{% highlight json linenos %}
{
    "units": [
        {
            "id": "6460eb105983b6a7ad04f495",
            "ingredient": {
                "id": "6460eb105983b6a7ad04f47a",
                "name": "Jambon blanc, cuit"
            },
            "alias": {
                "id": "6460eb105983b6a7ad04f46d",
                "name": "tranche"
            },
            "value": 45
        },
        {
            "id": "6460eb105983b6a7ad04f496",
            "ingredient": {
                "id": "6460eb105983b6a7ad04f47c",
                "name": "Vanille"
            },
            "alias": {
                "id": "6460eb105983b6a7ad04f46f",
                "name": "gousse"
            },
            "value": 3
        }
    ]
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->

# Routes

1. [get-user-all]

----

[User]: index.md
[Supplier]: ../supplier.md
[Ingredient]: ../ingredient.md
[get-user-all]: #get-user-all