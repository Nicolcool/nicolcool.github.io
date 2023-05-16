---
title: Alias
layout: default
has_children: true
---

# Alias
----

> La table `Alias` stocke en base de données la liste des noms pouvant être utilisés pour la création d'un document de type [Units]. `Alias` doit être un (ou plusieurs) mot > simple qui représente un conditionnement sous lequel on peut retrouver un ingrédient dans une recette.


{: .example }
tranche, gousse, boite, paquet, pièce...


## Structure
----

| Champs | Description                | Type     | Requis | Unique |
|:-------|:---------------------------|:---------|:-------|:-------|
| _id    | identifiant unique MongoDB | objectId | Oui    | Oui    |
| name   | Un mot simple et explicite | string   | Oui    | Oui    |


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
#[Assert\NotBlank(message: "Name is required.")]
#[Assert\Type('string')]
private string $name;
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

# Routes

1. [get-all]
1. [get-one]
1. [create-one]
1. [update-one]
1. [delete-one]

----

[Units]: user/units.html
[get-all]: #get-all
[get-one]: #get-one
[create-one]: #create-one
[update-one]: #update-one
[delete-one]: #delete-one