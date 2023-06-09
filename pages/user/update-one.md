---
title: update-one
layout: default
nav_order: 4
parent: User
---

Admin
{: .label .label-red }

<!-- DÉBUT DE LA ROUTE -->
## update-one
----

> Modifie un document `User` existant avec de nouvelles valeurs.


### Requête

{: .request-put }
> https://api.sharlotte.fr/admin/users/*_id*

### Paramètres

| Paramètres | Valeurs                                         |
|:-----------|:------------------------------------------------|
| *_id*      | identifiant unique du document `User` recherché |

### Body
{% capture _code %}{% highlight json linenos %}
{
    "password": "strongpassword"
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6462fa09e87d4b984d0dbc13",
    "email": "email@mail.com",
    "roles": [
        "ROLE_SHOP",
        "ROLE_USER"
    ],
    "labels": [
        "Boutique",
        "Commandes",
        "Client-1"
    ]
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