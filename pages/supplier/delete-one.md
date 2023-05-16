---
title: delete-one
layout: default
parent: Supplier
nav_order: 5
---

User
{: .label .label-yellow }

<!-- DÉBUT DE LA ROUTE -->
# delete-one
----

> Supprime un document `Supplier` existant de la base de données, à condition que l'utilisateur en possède les droits d'accès.

> Pour plus d'informations à propos de l'authentification et des droits d'accès aux données : lire la section [Security].

## Requête

{: .request-delete }
> https://api.sharlotte.fr/supplier/*_id*

## Paramètres

| Paramètres | Valeurs                                             |
|:-----------|:----------------------------------------------------|
| *_id*      | identifiant unique du document `Supplier` recherché |

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

[get-all]: get-all.html
[get-one]: get-one.html
[create-one]: create-one.html
[update-one]: update-one.html
[delete-one]: delete-one.html