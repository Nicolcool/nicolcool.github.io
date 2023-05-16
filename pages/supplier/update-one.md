---
title: update-one
layout: default
parent: Supplier
nav_order: 4
---

User
{: .label .label-yellow }

<!-- DÉBUT DE LA ROUTE -->
# update-one
----

> Modifie un document `Supplier` existant avec de nouvelles valeurs, à condition que l'utilisateur authentifié en possède les droits d'accès.

> Pour plus d'informations à propos de l'authentification et des droits d'accès aux données : lire la section [Security].

## Requête

{: .request-put }
> https://api.sharlotte.fr/suppliers/*_id*

## Paramètres

| Paramètres | Valeurs                                             |
|:-----------|:----------------------------------------------------|
| *_id*      | identifiant unique du document `Supplier` recherché |

## Body
{% capture _code %}{% highlight json linenos %}
{
    "name": "nouveaufournisseur"
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

## Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "64621c61dbf19f8fae0dae43",
    "name": "nouveaufournisseur",
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

[Sources]: user/sources.html
[User]: user/index.html
[Security]: security.html
[get-all]: #get-all
[get-one]: #get-one
[create-one]: #create-one
[update-one]: #update-one
[delete-one]: #delete-one