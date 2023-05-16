---
title: delete-all
layout: default
nav_order: 5
parent: Ingredient
---

<!-- DÉBUT DE LA ROUTE -->
## delete-one
----
User
{: .label .label-yellow }

> Supprime un document `Ingredient` existant de la base de données, à condition que l'utilisateur authentifié en soit le propriétaire.

> Pour plus d'informations à propos de l'authentification et des droits d'accès aux données : lire la section [Security].

### Requête

{: .request-delete }
> https://api.sharlotte.fr/ingredients/*_id*

### Paramètres

| Paramètres | Valeurs                                               |
|:-----------|:------------------------------------------------------|
| *_id*      | identifiant unique du document `Ingredient` recherché |

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

[Product]: user/produit.html
[IngredientCategory]: ingredientcategory.html
[Security]: security.html
[User]: user/index.html
[get-all]: #get-all
[get-one]: #get-one
[create-one]: #create-one
[update-one]: #update-one
[delete-one]: #delete-one