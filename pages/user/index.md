---
title: User
layout: default
nav_order: 2
has_children: true
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

----

[brand]: ../security.html#rôles
[manager]: ../security.html#rôles
[roles]: ../security.html#rôles
[labels]: user/labels.html
[units]: user/units.html
[sources]: user/sources.html
[actives]: user/actives.html
[get-all]: #get-all
[get-one]: #get-one
[create-one]: #create-one
[update-one]: #update-one
[delete-one]: #delete-one