---
title: get-all
layout: default
parent: Supplier
nav_order: 1
---

User
{: .label .label-yellow }

<!-- DÉBUT DE LA ROUTE -->
# get-all
----

> Renvoie la liste de tous les `Supplier` qui existent en base de données et qui sont accessibles à l'utilisateur authentifié.

> Pour plus d'informations à propos de l'authentification et des droits d'accès aux données : lire la section [Security].

## Requête

{: .request-get }
> https://api.sharlotte.fr/suppliers

## Paramètres
*Aucun paramètre n'est nécessaire*

## Body
*Aucun contenu n'est nécessaire*

## Réponse
{% capture _code %}{% highlight json linenos %}
[{
    "id": "6460eb105983b6a7ad04f46a",
    "name": "Fournisseur 1",
    "owner": {
        "email": "manager@brand.cool"
    }
},
{
    "id": "6460eb105983b6a7ad04f46b",
    "name": "Fournisseur 2",
    "owner": {
        "email": "shop1@brand.cool"
    }
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

[Sources]: user/sources.html
[User]: user/index.html
[Security]: security.html
[get-all]: #get-all
[get-one]: #get-one
[create-one]: #create-one
[update-one]: #update-one
[delete-one]: #delete-one