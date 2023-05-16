---
title: Alias
layout: default
nav_order: 5
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

[Units]: ../units/index.html
[get-all]: get-all.html
[get-one]: get-one.html
[create-one]: create-one.html
[update-one]: update-one.html
[delete-one]: delete-one.html