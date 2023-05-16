---
title: User
layout: default
nav_order: 2

---

# User
----

> La table `User` stocke en base de données la liste des utilisateurs.


## Structure
----

| Champs   | Description                | Type                 | Requis | Unique |
|:---------|:---------------------------|:---------------------|:-------|:-------|
| _id      | identifiant unique MongoDB | objectId             | Oui    | Oui    |
| email    | Un mot simple et explicite | string               | Oui    | Oui    |
| [brand]    | Un mot simple et explicite | objectId           | Non    | Non    |
| [manager]  | Un mot simple et explicite | objectId           | Non    | Non    |
| [roles]    | Un mot simple et explicite | array (of strings) | Oui    | Non    |
| password | Un mot simple et explicite | string               | Oui    | Non    |
| [labels]   | Un mot simple et explicite | array (of strings) | Non    | Non    |
| [units]    | Un mot simple et explicite | array (of objects) | Non    | Non    |
| [sources]  | Un mot simple et explicite | array (of objects) | Non    | Non    |
| [actives]  | Un mot simple et explicite | array (of strings) | Non    | Non    |


## Validation
----

### Base de données

{% capture _code %}{% highlight json linenos %}
{
    "$jsonSchema": {
        "required": ["email","roles","password"],
        "properties": {
            "email": {
                "bsonType": "string",
                "description": "must be a string and is required."
            },
            "roles": {
                "bsonType": "array",
                "description": "must be an array and is required.",
                "uniqueItems": true,
                "items":{
                    "enum": ["ROLE_ADMIN","ROLE_MANAGER-BRAND","ROLE_MANAGER-SHOP","ROLE_SHOP"]
                }
            },
            "password": {
                "bsonType": "string",
                "description": "must be a string and is required."
            },
            "labels": {
                "bsonType": "array",
                "description": "must be an array.",
                "uniqueItems": true
            },
            "actives": {
                "bsonType": "array",
                "description": "must be an array.",
                "uniqueItems": true,
                "items":{
                    "bsonType": "string"
                }
            },
            "brandManager": {
                "bsonType": "objectId",
                "description": "must be an objectId"
            },
            "shopManager": {
                "bsonType": "objectId",
                "description": "must be an objectId"
            },
            "units": {
                "bsonType": "array",
                "description": "must be an array",
                "items":{
                    "bsonType": "object",
                    "required": ["ingredient","alias","value"],
                    "properties": {
                        "ingredient": {
                            "bsonType": "objectId",
                            "description": "must be a objectId and is required."
                        },
                        "alias": {
                            "bsonType": "objectId",
                            "description": "must be a objectId and is required."
                        },
                        "value": {
                            "bsonType": "double",
                            "description": "must be a double and is required."
                        }
                    }
                }
            },
            "sources": {
                "bsonType": "array",
                "description": "must be an array",
                "items":{
                    "bsonType": "object",
                    "required": ["ingredient","supplier","HTprice","taxes"],
                    "properties": {
                        "ingredient": {
                            "bsonType": "objectId",
                            "description": "must be a objectId and is required."
                        },
                        "supplier": {
                            "bsonType": "objectId",
                            "description": "must be a objectId and is required."
                        },
                        "ref": {
                            "bsonType": "string",
                            "description": "must be a string."
                        },
                        "HTprice": {
                            "bsonType": "double",
                            "description": "must be a double and is required."
                        },
                        "taxes": {
                            "bsonType": "double",
                            "description": "must be a double and is required."
                        }
                    }
                }
            }
        }
    }
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

### Serveur

{% capture _code %}{% highlight php linenos %}
#[MongoDB\Id]
protected string $id;

#[MongoDB\Field(type: 'string')]
#[MongoDB\Index(unique: true)]
#[Assert\NotBlank(message: "email address is required.")]
#[Assert\Email(message: "Invalid email address.")]
protected string $email;

#[MongoDB\ReferenceOne(targetDocument: User::class, storeAs:"id")]
private ?User $brandManager = null;

#[MongoDB\ReferenceOne(targetDocument: User::class, storeAs:"id")]
private ?User $shopManager = null;

#[MongoDB\Field(type: 'collection', options: ['type' => 'string'])]
#[Assert\NotBlank(message: "At least one role is required.")]
#[Assert\Type('array')]
#[Assert\Unique]
protected $roles = [];

#[MongoDB\Field(type: 'string')]
#[Assert\NotBlank(message: "'password' is required.")]
#[Assert\Type('string')]
protected string $password;

#[MongoDB\Field(type: 'collection', options: ['type' => 'string'])]
#[Assert\Type(type:"array",message: "'labels' must be an array but is not required.")]
#[Assert\Type('array')]
#[Assert\Unique]
protected array $labels;

#[MongoDB\Field(type: 'collection', options: ['type' => 'string'])]
#[Assert\Type(type:"array",message: "'actives' must be an array but is not required.")]
#[Assert\Type('array')]
#[Assert\Unique]
protected $actives;

#[MongoDB\EmbedMany(targetDocument:Unit::class)]
private $units;

#[MongoDB\EmbedMany(targetDocument:Source::class)]
private $sources;
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
Admin
{: .label .label-red }

> Renvoie la liste de tous les `User` qui existent en base de données.


### Requête

{: .request-get }
> https://api.sharlotte.fr/admin/users

{: .request-get }
> https://api.sharlotte.fr/admin/users?page=1&limit=20
> 
> *renvoie les 20 premiers résultats*

{: .request-get }
> https://api.sharlotte.fr/admin/users?page=2&limit=20
> 
> *renvoie les résultats 21 à 40*

{: .request-get }
> https://api.sharlotte.fr/admin/users?search=BurgerRoi
> 
> *renvoie tout les résultats qui correspondent à la recherche, classés par ordre de correspondance*

### Paramètres

| Paramètres | Valeurs                                           |
|:-----------|:--------------------------------------------------|
| limit      | nombre de résultats affichés par page de réponses |
| page       | numéro de la page de réponses à afficher          |
| search     | phrase de recherche                               |

### Body
*Aucun contenu n'est nécessaire*

### Réponse
{% capture _code %}{% highlight json linenos %}
[{
    "id": "6460eb0f5983b6a7ad04f462",
    "email": "manager@brand.cool",
    "roles": [
        "ROLE_BRAND",
        "ROLE_USER"
    ],
    "labels": [
        "dolore",
        "repudiandae",
        "quia"
    ],
    "actives": null,
    "units": [ ... ],
    "sources": [ ... ]
},
{
    "id": "6460eb0f5983b6a7ad04f463",
    "email": "shop-manager@brand.cool",
    "roles": [
        "ROLE_MANAGER",
        "ROLE_USER"
    ],
    "labels": [
        "corrupti",
        "ipsa",
        "quibusdam"
    ],
    "actives": null,
    "units": [ ... ],
    "sources": [ ... ]
}]
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->
<!-- DÉBUT DE LA ROUTE -->
## get-one
----
Admin
{: .label .label-red }

> Renvoie les informations d'un seul document `User` depuis son identifiant unique.


### Requête

{: .request-get }
> https://api.sharlotte.fr/admin/users/*_id*

### Paramètres

| Paramètres | Valeurs                                         |
|:-----------|:------------------------------------------------|
| *_id*      | identifiant unique du document `User` recherché |

### Body
*Aucun contenu n'est nécessaire*

### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6460eb0f5983b6a7ad04f462",
    "email": "manager@brand.cool",
    "roles": [
        "ROLE_BRAND",
        "ROLE_USER"
    ],
    "labels": [
        "dolore",
        "repudiandae",
        "quia"
    ],
    "actives": null,
    "units": [ ... ],
    "sources": [ ... ]
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->
<!-- DÉBUT DE LA ROUTE -->
## create-one
----
Admin
{: .label .label-red }

> Créer et ajoute un document `User` à la base de données.


### Requête

{: .request-post }
> https://api.sharlotte.fr/admin/users

### Paramètres
*Aucun contenu n'est nécessaire*

### Body
{% capture _code %}{% highlight json linenos %}
{
    "email":"email@mail.com",
    "password":"bonjour",
    "roles":["ROLE_SHOP"],
    "labels":["Boutique","Commandes","Client-1"]
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

{: .note }
> Les champs optionels peuvent être omis de la requête.
> Le champs `password` est en clair dans la requête. Il est hashé par le serveur avant d'être insérer en base de données.

### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6462fa09e87d4b984d0dbc13",
    "email": "email@mail.com",
    "roles": [
        "ROLE_SHOP",
        "ROLE_USER"
    ],
    "labels": [
        "Boutique",
        "Commandes",
        "Client-1"
    ]
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->
<!-- DÉBUT DE LA ROUTE -->
## update-one
----
Admin
{: .label .label-red }

> Modifie un document `User` existant avec de nouvelles valeurs.


### Requête

{: .request-put }
> https://api.sharlotte.fr/admin/users/*_id*

### Paramètres

| Paramètres | Valeurs                                         |
|:-----------|:------------------------------------------------|
| *_id*      | identifiant unique du document `User` recherché |

### Body
{% capture _code %}{% highlight json linenos %}
{
    "password": "strongpassword"
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6462fa09e87d4b984d0dbc13",
    "email": "email@mail.com",
    "roles": [
        "ROLE_SHOP",
        "ROLE_USER"
    ],
    "labels": [
        "Boutique",
        "Commandes",
        "Client-1"
    ]
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->
<!-- DÉBUT DE LA ROUTE -->
## delete-one
----
Admin
{: .label .label-red }

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

----

[brand]: security.html#rôles
[manager]: security.html#rôles
[roles]: security.html#rôles
[labels]: user/labels.html
[units]: user/units.html
[sources]: user/sources.html
[actives]: user/actives.html
[get-all]: #get-all
[get-one]: #get-one
[create-one]: #create-one
[update-one]: #update-one
[delete-one]: #delete-one