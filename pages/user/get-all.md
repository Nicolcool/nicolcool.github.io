---
title: get-all
layout: default
nav_order: 1
parent: User
---

Admin
{: .label .label-red }

## get-all
----

> Renvoie la liste de tous les `User` qui existent en base de données.


### Requête

{: .request-get }
> https://api.sharlotte.fr/admin/users

{: .request-get }
> https://api.sharlotte.fr/admin/users?page=1&limit=20
> 
> *renvoie les 20 premiers résultats*

{: .request-get }
> https://api.sharlotte.fr/admin/users?page=2&limit=20
> 
> *renvoie les résultats 21 à 40*

{: .request-get }
> https://api.sharlotte.fr/admin/users?search=BurgerRoi
> 
> *renvoie tout les résultats qui correspondent à la recherche, classés par ordre de correspondance*

### Paramètres

| Paramètres | Valeurs                                           |
|:-----------|:--------------------------------------------------|
| limit      | nombre de résultats affichés par page de réponses |
| page       | numéro de la page de réponses à afficher          |
| search     | phrase de recherche                               |

### Body
*Aucun contenu n'est nécessaire*

### Réponse
{% capture _code %}{% highlight json linenos %}
[{
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
},
{
    "id": "6460eb0f5983b6a7ad04f463",
    "email": "shop-manager@brand.cool",
    "roles": [
        "ROLE_MANAGER",
        "ROLE_USER"
    ],
    "labels": [
        "corrupti",
        "ipsa",
        "quibusdam"
    ],
    "actives": null,
    "units": [ ... ],
    "sources": [ ... ]
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

[get-all]: get-all.html
[get-one]: get-one.html
[create-one]: create-one.html
[update-one]: update-one.html
[delete-one]: delete-one.html