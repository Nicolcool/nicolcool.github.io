---
title: Supplier
layout: default
has_children: true
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

----

[Sources]: user/sources.html
[User]: user/index.html
[Security]: security.html
[get-all]: #get-all
[get-one]: #get-one
[create-one]: #create-one
[update-one]: #update-one
[delete-one]: #delete-one