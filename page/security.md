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
Lorsqu'une route est annotée avec plusieurs étiquettes, c'est qu'elle est accessible depuis les deux niveaux de sécurité mais peux donner des résultats différents. Voir [Droits d'accès]

1. User : la requête doit être authentifiée pour être acceptée, peut-importe l'utilisateur qui la formule.
1. Admin : la requête doit être authentifiée par un utilisateur administrateur pour être acceptée.
1. Public : la requête est accessible sans authentification.

> De façon générale, lorsqu'une route est de type Admin, le chemin correspondant commence par "admin/"



## Authentification
----

Les utilisateurs sont stockés dans une table [User]. L'API de Sharlotte utilise le système JWT "JSON Web Token" pour gérer l'authentification des requêtes. Toutes les requêtes qui ne sont pas de type "Public" doivent envoyer un token d'authentification dans les headers avec le corps de la requête. Le token est composé du mot "Bearer" suivi d'un espace et du token en lui même. Il doit être associé à la clé "Authorization".

{% capture _code %}{% highlight http linenos %}
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


----

[Droits d'accès]: #droits-d'accès
[User]: user/index.html
[get-all]: #get-all
[get-one]: #get-one
[create-one]: #create-one
[update-one]: #update-one
[delete-one]: #delete-one