---
title: update-one
layout: default
nav_order: 4
parent: Ingredient
---

User
{: .label .label-yellow }

<!-- DÉBUT DE LA ROUTE -->
## update-one
----

> Modifie un document `Ingredient` existant avec de nouvelles valeurs, à condition que l'utilisateur authentifié en soit le propriétaire.

> Pour plus d'informations à propos de l'authentification et des droits d'accès aux données : lire la section [Security].


### Requête

{: .request-put }
> https://api.sharlotte.fr/ingredients/*_id*

### Paramètres

| Paramètres | Valeurs                                               |
|:-----------|:------------------------------------------------------|
| *_id*      | identifiant unique du document `Ingredient` recherché |

### Body
{% capture _code %}{% highlight json linenos %}
{
    "name": "Nouveau nom",
    "calorie":245
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6462baa4b24b095c4207a992",
    "name": "Nouveau nom",
    "slug": "nouveaunom",
    "calorie":245
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

[Security]: ../security/index.html
[get-all]: get-all.html
[get-one]: get-one.html
[create-one]: create-one.html
[update-one]: update-one.html
[delete-one]: delete-one.html