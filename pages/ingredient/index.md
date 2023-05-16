---
title: Ingredient
layout: default
nav_order: 6
has_children: true
---

# Ingredient
----

> La table `Ingredient` stocke en base de données la liste des ingrédients existants. En opposition aux [Product], les ingrédients n'ont pas pour vocation à être vendus tel quel. Les ingrédients sont séparés en deux familles : les matières premières et les appareils. Les matières premières ne sont composées de rien d'autre que d'elles même. Les appareils sont des ingrédients qui sont nécéssaires à la composition des [Product], mais qui sont eux même composés de plusieurs ingrédients.


{: .example }
> - "Poireau" est une matière première. 
> - "Pâte brisée" est un appareil composé de plusieurs ingrédients comme le beurre ou la farine. 
> - "Quiche aux poireaux" est un produit dont la recette contient des ingrédients de type matière première, mais aussi des appareils.


## Structure
----

| Champs        | Description                                                                                         | Type     | Requis | Unique |
|:--------------|:----------------------------------------------------------------------------------------------------|:---------|:-------|:-------|
| _id           | identifiant unique MongoDB                                                                          | objectId | Oui    | Oui    |
| name          | Un mot simple et explicite                                                                          | string   | Oui    | Oui    |
| slug          | Slug unique généré automatiquement à partir du champs `name`                                        | string   | Oui    | Oui    |
| category      | La catégorie dans laquelle le document est classé. Référence un document [IngredientCategory]       | objectId | Oui    | Non    |
| calories      | Nombre de calories, valeur exprimée pour 100g                                                       | int32    | Non    | Non    |
| proteins      | Quantité de protéines, valeur exprimée pour 100g                                                    | double   | Non    | Non    |
| carbohydrates | Quantité de glucides, valeur exprimée pour 100g                                                     | double   | Non    | Non    |
| sugars        | Quantité de sucre, valeur exprimée pour 100g                                                        | double   | Non    | Non    |
| fats          | Quantité de lipides, valeur exprimée pour 100g                                                      | double   | Non    | Non    |
| saturates     | Quantité de matière grasse saturées, valeur exprimée pour 100g                                      | double   | Non    | Non    |
| salt          | Quantité de sel, valeur exprimée pour 100g                                                          | double   | Non    | Non    |
| owner         | L'utilisateur propriétaire du document. Référence un document [User]                                | objectId | Oui    | Non    |
| privacy       | Le niveau de partage choisi pour l'ingrédient. Voir [Security] pour plus d'informations             | string   | Oui    | Non    |
| instructions  | Un tableau qui contient la liste des instructions (dans l'ordre) de la recette, quand il y en a une | array    | Non    | Non    |


## Validation
----

### Base de données

Le champ `privacy` doit contenir une valeur qui doit forcément appartenir à la liste suivante : "PUBLIC", "PRIVATE", "FAMILY". Pour plus d'information sur les droits d'accès aux données, voir [Security].

{% capture _code %}{% highlight json linenos %}
{
    "$jsonSchema": {
        "required": ["name","slug","category","owner","privacy"],
        "properties": {
            "name": {
                "bsonType": "string",
                "description": "must be a string and is required"
            },
            "slug": {
                "bsonType": "string",
                "description": "must be a string and is required"
            },
            "category": {
                "bsonType": "objectId",
                "description": "must be a objectId and is required"
            },
            "owner": {
                "bsonType": "objectId",
                "description": "must be a objectId and is required"
            },
            "privacy": {
                "bsonType": "string",
                "enum": ["PUBLIC","PRIVATE","FAMILY"],
                "description": "must be a string and is required"
            },
            "calorie": {
                "bsonType": "int",
                "description": "must be a int"
            },
            "proteins": {
                "bsonType": "double",
                "description": "must be a double"
            },
            "carbohydrates": {
                "bsonType": "double",
                "description": "must be a double"
            },
            "sugars": {
                "bsonType": "double",
                "description": "must be a double"
            },
            "fats": {
                "bsonType": "double",
                "description": "must be a double"
            },
            "saturates": {
                "bsonType": "double",
                "description": "must be a double"
            },
            "salt": {
                "bsonType": "double",
                "description": "must be a double"
            },
            "instructions": {
                "bsonType": "array",
                "description": "must be an array.",
                "items":{
                    "bsonType": "string"
                }
            }
        }
    }
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

### Serveur

{% capture _code %}{% highlight php linenos %}
#[MongoDB\Id]
private string $id;

#[MongoDB\Field(type: 'string')]
#[MongoDB\Index(unique: true)]
#[Assert\NotBlank(message: "Name is required.")]
#[Assert\Type('string')]
private string $name;

#[MongoDB\Field(type: 'string')]
#[MongoDB\Index(unique: true)]
#[Assert\NotBlank(message: "Slug is required.")]
#[Assert\Type('string')]
private string $slug;

#[MongoDB\ReferenceOne(targetDocument: IngredientCategory::class, storeAs:"id")]
#[Assert\NotBlank(message: "Ingredient must have one category.")]
private IngredientCategory $category;

// NUTRITION
#[MongoDB\Field(type: 'int')]
#[Assert\Type('int')]
private int $calories;

#[MongoDB\Field(type: 'float')]
#[Assert\Type('double')]
private float $proteins;

#[MongoDB\Field(type: 'float')]
#[Assert\Type('double')]
private float $carbohydrates;

#[MongoDB\Field(type: 'float')]
#[Assert\Type('double')]
private float $sugars;

#[MongoDB\Field(type: 'float')]
#[Assert\Type('double')]
private float $fats;

#[MongoDB\Field(type: 'float')]
#[Assert\Type('double')]
private float $saturates;

#[MongoDB\Field(type: 'float')]
#[Assert\Type('double')]
private float $salt;
// NUTRITION   

#[MongoDB\ReferenceOne(targetDocument: User::class, storeAs:"id")]
#[Assert\NotBlank(message: "One owner is required.")]
private User $owner;

#[MongoDB\Field(type: 'string')]
#[Assert\NotBlank(message: "Privacy setting must be set.")]
#[Assert\Type('string')]
private string $privacy;

#[MongoDB\Field(type: 'collection')]
#[Assert\Type('array')]
private $instructions;
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

----

[Product]: ../product/index.html
[IngredientCategory]: ../ingredientcategory/index.html
[Security]: ../security/index.html
[User]: ../user/index.html
[get-all]: get-all.html
[get-one]: get-one.html
[create-one]: create-one.html
[update-one]: update-one.html
[delete-one]: delete-one.html