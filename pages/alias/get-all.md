---
title: get-all
layout: default
nav_order: 1
parent: Alias
---

Public
{: .label .label-green }

<!-- DÉBUT DE LA ROUTE -->
# get-all
----

> Renvoie la liste de tous les `Alias` qui existent en base de données.

## Requête

{: .request-get }
> https://api.sharlotte.fr/alias

## Paramètres
*Aucun paramètre n'est nécessaire*

## Body
*Aucun contenu n'est nécessaire*

## Réponse
{% capture _code %}{% highlight json linenos %}
[{
    "id": "6460eb105983b6a7ad04f46d",
    "name": "tranche"
},
{
    "id": "6460eb105983b6a7ad04f46e",
    "name": "boite"
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

[Units]: user/units.html
[get-all]: #get-all
[get-one]: #get-one
[create-one]: #create-one
[update-one]: #update-one
[delete-one]: #delete-one