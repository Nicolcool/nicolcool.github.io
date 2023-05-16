---
title: delete-one
layout: default
nav_order: 5
parent: User
---

Admin
{: .label .label-red }

<!-- DÉBUT DE LA ROUTE -->
## delete-one
----

> Supprime un document `User` existant de la base de données.


### Requête

{: .request-delete }
> https://api.sharlotte.fr/admin/users/*_id*

### Paramètres

| Paramètres | Valeurs                                          |
|:-----------|:-------------------------------------------------|
| *_id*      | identifiant unique du document `User` recherché |

### Body
*Aucun contenu n'est nécessaire*

### Réponse
> HTTP - 204 - No Content
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