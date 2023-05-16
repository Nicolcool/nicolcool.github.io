---
title: update-one
layout: default
nav_order: 1
parent: Alias
---

Admin
{: .label .label-red }

<!-- DÉBUT DE LA ROUTE -->
# update-one
----

> Modifie un document `Alias` existant avec de nouvelles valeurs.

## Requête

{: .request-put }
> https://api.sharlotte.fr/admin/alias/*_id*

## Paramètres

| Paramètres | Valeurs                                          |
|:-----------|:-------------------------------------------------|
| *_id*      | identifiant unique du document `Alias` recherché |

## Body
{% capture _code %}{% highlight json linenos %}
{
    "name": "nouveaunom"
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

## Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "64620c30dbf19f8fae0dae42",
    "name": "nouveaunom"
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

[Units]: user/units.html
[get-all]: #get-all
[get-one]: #get-one
[create-one]: #create-one
[update-one]: #update-one
[delete-one]: #delete-one