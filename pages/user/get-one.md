---
title: get-one
layout: default
nav_order: 2
parent: User
---

Admin
{: .label .label-red }

<!-- DÉBUT DE LA ROUTE -->
## get-one
----

> Renvoie les informations d'un seul document `User` depuis son identifiant unique.


### Requête

{: .request-get }
> https://api.sharlotte.fr/admin/users/*_id*

### Paramètres

| Paramètres | Valeurs                                         |
|:-----------|:------------------------------------------------|
| *_id*      | identifiant unique du document `User` recherché |

### Body
*Aucun contenu n'est nécessaire*

### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6460eb0f5983b6a7ad04f462",
    "email": "manager@brand.cool",
    "roles": [
        "ROLE_BRAND",
        "ROLE_USER"
    ],
    "labels": [
        "dolore",
        "repudiandae",
        "quia"
    ],
    "actives": null,
    "units": [ ... ],
    "sources": [ ... ]
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

[brand]: ../security.html#rôles
[manager]: ../security.html#rôles
[roles]: ../security.html#rôles
[labels]: user/labels.html
[units]: user/units.html
[sources]: user/sources.html
[actives]: user/actives.html
[get-all]: #get-all
[get-one]: #get-one
[create-one]: #create-one
[update-one]: #update-one
[delete-one]: #delete-one