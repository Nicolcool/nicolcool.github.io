---
title: get-one
layout: default
parent: Supplier
nav_order: 2
---

User
{: .label .label-yellow }

<!-- DÉBUT DE LA ROUTE -->
# get-one
----

> Renvoie les informations d'un seul document `Supplier` depuis son identifiant unique et dont l'utilisateur authentifié possède les droits d'accès.

> Pour plus d'informations à propos de l'authentification et des droits d'accès aux données : lire la section [Security].

## Requête

{: .request-get }
> https://api.sharlotte.fr/suppliers/*_id*

## Paramètres

| Paramètres | Valeurs                                             |
|:-----------|:----------------------------------------------------|
| *_id*      | identifiant unique du document `Supplier` recherché |

## Body
*Aucun contenu n'est nécessaire*

## Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6460eb105983b6a7ad04f46a",
    "name": "Fournisseur",
    "owner": {
        "email": "manager@brand.cool"
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