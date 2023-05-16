---
title: get-one
layout: default
nav_order: 1
parent: Alias
---

Public
{: .label .label-green }

<!-- DÉBUT DE LA ROUTE -->
# get-one
----

> Renvoie les informations d'un seul document `Alias` depuis son identifiant unique.

## Requête

{: .request-get }
> https://api.sharlotte.fr/alias/*_id*

## Paramètres

| Paramètres | Valeurs                                          |
|:-----------|:-------------------------------------------------|
| *_id*      | identifiant unique du document `Alias` recherché |

## Body
*Aucun contenu n'est nécessaire*

## Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6460eb105983b6a7ad04f46d",
    "name": "tranche"
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