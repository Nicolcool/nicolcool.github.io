---
title: create-one
layout: default
nav_order: 3
parent: User
---

Admin
{: .label .label-red }

<!-- DÉBUT DE LA ROUTE -->
## create-one
----

> Créer et ajoute un document `User` à la base de données.


### Requête

{: .request-post }
> https://api.sharlotte.fr/admin/users

### Paramètres
*Aucun contenu n'est nécessaire*

### Body
{% capture _code %}{% highlight json linenos %}
{
    "email":"email@mail.com",
    "password":"bonjour",
    "roles":["ROLE_SHOP"],
    "labels":["Boutique","Commandes","Client-1"]
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

{: .note }
> Les champs optionels peuvent être omis de la requête.
> Le champs `password` est en clair dans la requête. Il est hashé par le serveur avant d'être inséré en base de données.

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