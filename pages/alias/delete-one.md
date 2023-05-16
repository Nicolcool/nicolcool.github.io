---
title: delete-one
layout: default
nav_order: 1
parent: Alias
---

Admin
{: .label .label-red }

<!-- DÉBUT DE LA ROUTE -->
# delete-one
----

> Supprime un document `Alias` existant de la base de données.

## Requête

{: .request-delete }
> https://api.sharlotte.fr/admin/alias/*_id*

## Paramètres

| Paramètres | Valeurs                                          |
|:-----------|:-------------------------------------------------|
| *_id*      | identifiant unique du document `Alias` recherché |

## Body
*Aucun contenu n'est nécessaire*

## Réponse
> HTTP - 204 - No Content
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