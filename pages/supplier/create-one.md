---
title: create-one
layout: default
parent: Supplier
nav_order: 3
---

User
{: .label .label-yellow }

<!-- DÉBUT DE LA ROUTE -->
# create-one
----

> Créer et ajoute un document `Supplier` à la base de données.

## Requête

{: .request-post }
> https://api.sharlotte.fr/suppliers

## Paramètres
*Aucun contenu n'est nécessaire*

## Body
{% capture _code %}{% highlight json linenos %}
{
    "name": "fournisseur"
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

{: .note }
> Le champ `owner` est traité automatiquement par le serveur à partir de l'utilisateur authentifié.

## Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "64621c61dbf19f8fae0dae43",
    "name": "fournisseur",
    "owner": {
        "email": "shop1@brand.cool"
    }
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