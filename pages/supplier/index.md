---
title: Supplier
layout: default
has_children: true
nav_order: 8
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

----

[Sources]: ../sources/index.html
[User]: ../user/index.html
[get-all]: get-all.html
[get-one]: get-one.html
[create-one]: create-one.html
[update-one]: update-one.html
[delete-one]: delete-one.html