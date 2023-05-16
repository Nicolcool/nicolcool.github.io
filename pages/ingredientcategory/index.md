---
title: IngredientCategory
layout: default
nav_order: 4
has_children: true
---

# IngredientCategory
----

> La table `IngredientCategory` stocke en base de données la liste des catégories dans lesquelles les documents [Ingredient] peuvent être classés.

{: .example }
> Viandes, Poissons, Crèmerie, Fruits...

## Structure
----

| Champs      | Description                                                                               | Type     | Requis | Unique |
|:------------|:------------------------------------------------------------------------------------------|:---------|:-------|:-------|
| _id         | identifiant unique MongoDB                                                                | objectId | Oui    | Oui    |
| name        | Un mot simple et explicite                                                                | string   | Oui    | Oui    |
| description | Une description courte de ce qui doit ou ne doit pas être catégorisé dans cette catégorie | string   | Oui    | Oui    |

## Validation
----

### Base de données

{% capture _code %}{% highlight json linenos %}
{
    "$jsonSchema": {
        "required": ["name","description"],
        "properties": {
            "name": {
                "bsonType": "string",
                "description": "must be a string and is required."
            },
            "description": {
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

#[MongoDB\Field(type: "string")]
#[Assert\NotBlank(message: "Description is required.")]
#[Assert\Type('string')]
private string $description;
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

# Routes

1. [get-all]
1. [get-one]
1. [create-one]
1. [update-one]
1. [delete-one]

----

[Ingredient]: ingredient.html
[get-all]: #get-all
[get-one]: #get-one
[create-one]: #create-one
[update-one]: #update-one
[delete-one]: #delete-one