---
title: IngredientCategory
layout: default
nav_order: 7
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

[Ingredient]: ../ingredient/index.html
[get-all]: get-all.html
[get-one]: get-one.html
[create-one]: create-one.html
[update-one]: update-one.html
[delete-one]: delete-one.html