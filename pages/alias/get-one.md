---
title: get-one
layout: default
nav_order: 2
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

[get-all]: get-all.html
[get-one]: get-one.html
[create-one]: create-one.html
[update-one]: update-one.html
[delete-one]: delete-one.html