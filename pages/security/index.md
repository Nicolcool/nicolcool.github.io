---
title: Security
layout: default
nav_order: 1
has_children: true
---

# Sécurité
----

> Les différentes routes sont accessibles via 3 niveaux de sécurité différents. "USER", "ADMIN" ou "PUBLIC". Tout au long de la documentation, chaque route est annotée de l'étiquette de sécurité correspondante.

User
{: .label .label-yellow }

Admin
{: .label .label-red }

Public
{: .label .label-green }

{: .note }
Lorsqu'une route est annotée avec plusieurs étiquettes, c'est qu'elle est accessible depuis tous les niveaux de sécurité donnés mais peux donner des résultats différents. Voir [Droits d'accès]

1. User : la requête doit être authentifiée pour être acceptée, peut-importe l'utilisateur qui la formule.
1. Admin : la requête doit être authentifiée par un utilisateur administrateur pour être acceptée.
1. Public : la requête est accessible sans authentification.

> De façon générale, lorsqu'une route est de type Admin, le chemin correspondant commence par "admin/"

----

[Droits d'accès]: ../security/access.html