---
title: Security
layout: default
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



## Authentification
----

Les utilisateurs sont stockés dans une table [User]. L'API de Sharlotte utilise le système JWT "JSON Web Token" pour gérer l'authentification des requêtes. Toutes les requêtes qui ne sont pas de type "Public" doivent envoyer un token d'authentification dans les headers avec le corps de la requête. Le token est composé du mot "Bearer" suivi d'un espace et du token en lui même. Il doit être associé à la clé "Authorization".

{% capture _code %}{% highlight text linenos %}
Authorization : Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE2ODQxOTY1MjksImV4c...
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

<!-- DÉBUT DE LA ROUTE -->
### Obtention d'un token
----

PUBLIC
{: .label .label-green }

> Renvoie un token d'authentification valide


#### Requête

{: .request-get }
> https://api.sharlotte.fr/login_check

#### Paramètres
*Aucun paramètre n'est nécessaire*

#### Body
{% capture _code %}{% highlight json linenos %}
{
    "username": "user@email.com",
    "passsord": "strongpassword"
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

#### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE2ODQxOTg3MTMsImV4cCI6MTY4NDIwMjMxMywicm9sZXMiOlsiUk9MRV9TSE9QIiwiUk9MRV9VU0VSIl0sInVzZXJuYW1lIjoic2hvcDFAYnJhbmQuY29vbCJ9.neNtT7ZDdmBvO3-mnA-PGyoDm0TX37kY7FkCauT4dKHEglhAQFN_h7fr-VBzAmnqivdok5B0LiTVyOL4esA8Isu03TUUylzD9Bkg6B0hdNEEypbSUpq_Zxctw3MpAXKCx-RXEc64yHg6xQTDqm4f31cMEkjoyFBDjvt1pv_Xc2CAsi-U5Ts4dUsmHGZRhgZXcehRF5MmF7oYSvvhDKNnGY5jkgwILqmr1zjJfgjwKSMgjkSA_N8fTS_DWFwKSuti3NZs7Jh0Kf002ggbC-2wTUPmsp3DPpn0hfT8RetOLOWka5MS051K5V2Mn_I7jTfqSx8w-0_4Mw-yEGeM_jFCGGlqqxio1vBx2yU7ZGN1bF-aahe2BPJ4WxGWwT9gx858De8lUfE_cm8LMhQdxp4jBzLXI__bh652xFbSqDlZZcW-DuyTBaiunC_iTqJTxMR_Xioqt1x8Rw77mixxUrsiCF7cQ9UJWaRQlTciczYoA1vco1GZm1XLXbKUPIoHdAVIQeC4RoGRYOUOfgETu13-mvUbrUVbBX51d9MgGzp-RR8JQ451Jwf4AynpWa1UiuY3417cloHmNtvgqs3JO4r4QA5WGQm10mcex1_fN9lqyGKYYhO87qCrgnTRtFlXbCgi9m-_Zxg7CF5CCX0FcQOpKFKyu3Nyaqjoo2-9unOKeOw"
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->

## Droits d'accès
----

Parmis tous les documents de la base de données, certains possèdent des droits d'accès particuliers. Pour ceux là, les requêtes peuvent renvoyer des résultats différents en fonction de l'utilisateur qui les formule.

### Rôles
----

Chaque utilisateur peut posséder l'un ou plusieurs de ces rôles :
1. `ROLE_ADMIN` : Administrateur système
1. `ROLE_USER` : Utilisateur lambda. Ce rôle est ajouté à tous les utilisateurs par defaut.
1. `ROLE_SHOP` : Utilisateur lié à une boutique unique.
1. `ROLE_MANAGER` : Utilisateur manager de plusieurs boutiques.
1. `ROLE_BRAND` : Utilisateur d'une entité marque.

Les documents utilisateurs peuvent également posséder un champs `brand` et un champs `manager`. Voir [User].

Par exemple :
- BurgerRoi est une marque de fastfoods. Ils ont un compte unique avec un rôle `ROLE_BRAND` qui leur permet d'avoir une vue sur tout les comptes liés à leur marque. 
- René ouvre un restaurant de la marque BurgerRoi, il dépend de la marque mais c'est lui qui gère son établissement. Il a un compte "renéshop@burgerroi.fr" avec un rôle `ROLE_SHOP` pour son restaurant. Son compte possède un champ `brand` qui référence le compte manager de BurgerRoi.
- Après quelques temps, René ouvre un second restaurant. Des responsables s'occupent de ses établissements, ils ont chacuns un compte. "renéshop@burgerroi.fr" et "renéshop-2@burgerroi.fr". Les deux comptes possèdent un champ `brand` qui référence le compte manager de BurgerRoi.
- Comme ses deux établissements utilisent beaucoup de recettes en commun, René se créer un compte manager avec son adresse personnelle. Son compte à le rôle `ROLE_MANAGER`. On ajoute à ses deux boutique le champs `manager` qui référence le compte manager de René.

```mermaid
graph TD;
    BRAND-->MANAGER;
    MANAGER-->Shop1;
    MANAGER-->Shop2;
```


```mermaid
graph TD;
    BurgerRoi-->René:test detde;
    René-->Shop1;
    René-->Shop2;
```

Cette relation permets de gérer les données de façons déscendante. Chaques compte à accès à ses propres données, celles de son manager ainsi que celles de sa marque. Ainsi BurgerRoi peux créer une recette qui sera accessible à toutes ses boutiques afin que chaque établissement ne refasse pas le travail de création des recettes. De la même façons, le propriétaire de plusieurs boutiques peut créer des données depuis un seul compte afin qu'elles soient accessibles à toutes ses boutiques rapidement.

### Droits d'accès
----

Certains documents possèdent un champs `privacy` qui permets de gérer son niveau de confidentialité. Il peut avoir l'une de ces valeurs :
1. PUBLIC : Le document est accessible à toute personne formulant une requête valide pour le lire.
1. FAMILY : Le document est accessible à son propriétaire ainsi qu'à tous ses descendants.
1. PRIVATE : Le document est uniquement accessible à son propriétaire.

{: .example }
> Le document "ABC" avec une `privacy` "FAMILY" d'une marque est accessible à son propriétaire ainsi qu'a tous les comptes "MANAGER" et "SHOP" qui référencent cette marque dans le champs `brand`.
>
> Le document "DEF" avec une `privacy` "FAMILY" d'un manager est accessible à son propriétaire ainsi qu'a tous les comptes "SHOP" qui référencent cet utilisateur dans le champs `manager`.

{: .note }
> Ces 3 règles de confidentialité accordent toujours des accès en lecture **uniquement**. L'écriture, la modification ou la suppression n'est toujours accessible qu'au propriétaire d'un document.

### Exemples
----

{: .request-get }
> https://api.sharlotte.fr/ingredients

La requête get-all permettant de récupérer la liste des ingrédients en base de données renvoie un résultat différent en fonction de l'auteur qui la formule.

> Anonyme : dans le cas d'une requête non authentifiée, la réponse renvoie la liste des ingrédients de `privacy` "PUBLIC" dans la base de données.

> `ROLE_SHOP` : la réponse renvoie la liste des ingrédients de `privacy` "PUBLIC" dans la base de données + les ingrédients de `privacy` "FAMILY" de son manager et/ou de sa `brand` + les ingrédient dont il est le propriétaire peut importe leur `privacy`.

> `ROLE_MANAGER` : la réponse renvoie la liste des ingrédients de `privacy` "PUBLIC" dans la base de données + les ingrédients de `privacy` "FAMILY" de sa `brand` + les ingrédient dont il est le propriétaire peut importe leur `privacy`.

> `ROLE_BRAND` : la réponse renvoie la liste des ingrédients de `privacy` "PUBLIC" dans la base de données + les ingrédient dont il est le propriétaire peut importe leur `privacy`.

----

[Droits d'accès]: #droits-daccès
[User]: user/index.html
[get-all]: #get-all
[get-one]: #get-one
[create-one]: #create-one
[update-one]: #update-one
[delete-one]: #delete-one