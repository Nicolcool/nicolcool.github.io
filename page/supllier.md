---
title: Supplier
layout: default
---

# Supplier
----

> La table `Supplier` stocke en base de données la liste des fournisseurs pouvant être utilisés pour la création d'un document de type [Sources]. `Supplier` doit être un (ou plusieurs) mot.


{: .example }
METRO, TransGourmet, PromoCash...


## Structure
----

| Champs | Description                                                          | Type     | Requis | Unique |
|:-------|:---------------------------------------------------------------------|:---------|:-------|:-------|
| _id    | identifiant unique MongoDB                                           | objectId | Oui    | Oui    |
| name   | Un mot simple et explicite                                           | string   | Oui    | Oui    |
| owner  | L'utilisateur propriétaire du document. Référence un document [User] | objectId | Oui    | Non    |


## Validation
----

### Base de données

{% capture _code %}{% highlight json linenos %}
{
    "$jsonSchema": {
        "required": ["name"],
        "properties": {
            "name": {
                "bsonType": "string",
                "description": "must be a string and is required."
            }
        }
    }
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

### Serveur

{% capture _code %}{% highlight php linenos %}
#[MongoDB\Id]
private string $id;

#[MongoDB\Field(type: "string")]
#[MongoDB\Index(unique: true)]
#[Assert\NotBlank(message: "name is required.")]
private string $name;

#[MongoDB\ReferenceOne(targetDocument: User::class, storeAs:"id")]
#[Assert\NotBlank(message: "owner is required.")]
private User $owner;
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}


# Routes

1. [get-all]
1. [get-one]
1. [create-one]
1. [update-one]
1. [delete-one]

<!-- DÉBUT DE LA ROUTE -->
## get-all
----
USER
{: .label .label-yellow }

> Renvoie la liste de tous les `Supplier` qui existent en base de données et qui sont accessibles à l'utilisateur authentifié.

> Pour plus d'informations à propos de l'authentification et des droits d'accès aux données : lire la section [Security].

### Requête

{: .request-get }
> https://api.sharlotte.fr/suppliers

### Paramètres
*Aucun paramètre n'est nécessaire*

### Body
*Aucun contenu n'est nécessaire*

### Réponse
{% capture _code %}{% highlight json linenos %}
[{
    "id": "6460eb105983b6a7ad04f46a",
    "name": "Fournisseur 1",
    "owner": {
        "email": "manager@brand.cool"
    }
},
{
    "id": "6460eb105983b6a7ad04f46b",
    "name": "Fournisseur 2",
    "owner": {
        "email": "shop1@brand.cool"
    }
}]
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->
<!-- DÉBUT DE LA ROUTE -->
## get-one
----
USER
{: .label .label-yellow }

> Renvoie les informations d'un seul document `Supplier` depuis son identifiant unique et dont l'utilisateur authentifié possède les droits d'accès.

> Pour plus d'informations à propos de l'authentification et des droits d'accès aux données : lire la section [Security].


### Requête

{: .request-get }
> https://api.sharlotte.fr/suppliers/*_id*

### Paramètres

| Paramètres | Valeurs                                             |
|:-----------|:----------------------------------------------------|
| *_id*      | identifiant unique du document `Supplier` recherché |

### Body
*Aucun contenu n'est nécessaire*

### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6460eb105983b6a7ad04f46a",
    "name": "Fournisseur",
    "owner": {
        "email": "manager@brand.cool"
    }
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->
<!-- DÉBUT DE LA ROUTE -->
## create-one
----
USER
{: .label .label-yellow }

> Créer et ajoute un document `Supplier` à la base de données.


### Requête

{: .request-post }
> https://api.sharlotte.fr/suppliers

### Paramètres
*Aucun contenu n'est nécessaire*

### Body
{% capture _code %}{% highlight json linenos %}
{
    "name": "fournisseur"
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

{: .note }
> Le champ `owner` est traité automatiquement par le serveur à partir de l'utilisateur authentifié.

### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "64621c61dbf19f8fae0dae43",
    "name": "fournisseur",
    "owner": {
        "email": "shop1@brand.cool"
    }
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->
<!-- DÉBUT DE LA ROUTE -->
## update-one
----
USER
{: .label .label-yellow }

> Modifie un document `Supplier` existant avec de nouvelles valeurs, à condition que l'utilisateur authentifié en possède les droits d'accès.

> Pour plus d'informations à propos de l'authentification et des droits d'accès aux données : lire la section [Security].


### Requête

{: .request-put }
> https://api.sharlotte.fr/suppliers/*_id*

### Paramètres

| Paramètres | Valeurs                                             |
|:-----------|:----------------------------------------------------|
| *_id*      | identifiant unique du document `Supplier` recherché |

### Body
{% capture _code %}{% highlight json linenos %}
{
    "name": "nouveaufournisseur"
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "64621c61dbf19f8fae0dae43",
    "name": "nouveaufournisseur",
    "owner": {
        "email": "shop1@brand.cool"
    }
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->
<!-- DÉBUT DE LA ROUTE -->
## delete-one
----
User
{: .label .label-yellow }

> Supprime un document `Supplier` existant de la base de données, à condition que l'utilisateur en possède les droits d'accès.

> Pour plus d'informations à propos de l'authentification et des droits d'accès aux données : lire la section [Security].


### Requête

{: .request-delete }
> https://api.sharlotte.fr/supplier/*_id*

### Paramètres

| Paramètres | Valeurs                                             |
|:-----------|:----------------------------------------------------|
| *_id*      | identifiant unique du document `Supplier` recherché |

### Body
*Aucun contenu n'est nécessaire*

### Réponse
> HTTP - 204 - No Content
<!-- FIN DE LA ROUTE -->

----

[Sources]: user/sources.html
[User]: user/index.html
[Security]: security.html
[get-all]: #get-all
[get-one]: #get-one
[create-one]: #create-one
[update-one]: #update-one
[delete-one]: #delete-one