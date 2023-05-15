---
title: Ingredient
layout: default
---

# Ingrédient
----

> La table `Ingrédient` stocke en base de données la liste des ingrédients existants. En opposition aux [Product], les ingrédients n'ont pas pour vocation à être vendus tel quel. Les ingrédients sont séparés en deux familles : les matières premières et les appareils. Les matières premières ne sont composées de rien d'autre que d'elles même. Les appareils sont des ingrédients qui sont nécéssaires à la composition des [Product], mais qui sont eux même composés de plusieurs ingrédients.


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


# Routes

1. [get-all]
1. [get-one]
1. [create-one]
1. [update-one]
1. [delete-one]

<!-- DÉBUT DE LA ROUTE -->
## get-all
----
PUBLIC
{: .label .label-green }

USER
{: .label .label-yellow }

> Renvoie la liste de tous les `Ingrédient` qui existent en base de données et qui sont réglés en confidentialité `PUBLIC`. Renvoie également tous les autres ingrédients accessibles à l'utilisateur authentifié.


### Requête

{: .request-get }
> https://api.sharlotte.fr/ingredients

{: .request-get }
> https://api.sharlotte.fr/ingredients?page=1&limit=20

> *renvoie les 20 premiers résultats*

> https://api.sharlotte.fr/ingredients?page=2&limit=20

> *renvoie les résultats 21 à 40*

> https://api.sharlotte.fr/ingredients?search=jambon

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
    "id": "6460eb105983b6a7ad04f471",
    "name": "Jambon blanc, cuit",
    "slug": "jambonblanccuit",
    "category": {
        "id": "6460eb105983b6a7ad04f467",
        "name": "Viandes"
    },
    "calories": 301,
    "proteins": 12.16,
    "carbohydrates": 19.88,
    "sugars": 49.18,
    "fats": 29.38,
    "saturates": 26.5,
    "salt": 16.03,
    "owner": {
        "id": "6460eb0f5983b6a7ad04f464",
        "email": "shop1@brand.cool"
    },
    "privacy": "PRIVATE",
    "instructions": []
},
[...]
]
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->
<!-- DÉBUT DE LA ROUTE -->
## get-one
----
PUBLIC
{: .label .label-green }

USER
{: .label .label-yellow }

> Renvoie les informations d'un seul document `Ingrédient` depuis son identifiant unique, à condition que l'utilisateur authentifié y ai les droits d'accès si l'ingrédient n'est pas réglé en confidentialité `PUBLIC`.


### Requête

{: .request-get }
> https://api.sharlotte.fr/ingredients/*_id*

### Paramètres

| Paramètres | Valeurs                                               |
|:-----------|:------------------------------------------------------|
| *_id*      | identifiant unique du document `Ingrédient` recherché |

### Body
*Aucun contenu n'est nécessaire*

### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6460eb105983b6a7ad04f472",
    "name": "Pâte brisée",
    "slug": "patebrisee",
    "category": {
        "id": "6460eb105983b6a7ad04f468",
        "name": "Pâtes et fonds"
    },
    "calories": 313,
    "proteins": 27.53,
    "carbohydrates": 3.91,
    "sugars": 6.02,
    "fats": 19.82,
    "saturates": 29.58,
    "salt": 39.59,
    "owner": {
        "id": "6460eb0f5983b6a7ad04f464",
        "email": "shop1@brand.cool"
    },
    "privacy": "PRIVATE",
    "instructions": [
        "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
        "Vestibulum eget ex sed tortor rutrum vestibulum.",
        "Vivamus laoreet nunc molestie, sodales odio tempus, lobortis lorem."
    ]
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->
<!-- DÉBUT DE LA ROUTE -->
## create-one
----
USER
{: .label .label-yellow }

> Créer et ajoute un document `Ingrédient` à la base de données.


### Requête

{: .request-post }
> https://api.sharlotte.fr/ingredients

### Paramètres
*Aucun contenu n'est nécessaire*

### Body
{% capture _code %}{% highlight json linenos %}
{
    "name":"Nouvel ingrédient",
    "category":"644fbb9215f67a77ac0515d7",
    "privacy":"PUBLIC"
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

{: .note }
> Les champs optionels peuvent être omis de la requête.
> Le champs `slug` est traité automatiquement par le serveur à partir du champs `name`.
> Le champ `owner` est traité automatiquement par le serveur à partir de l'utilisateur authentifié.

### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6460eb105983b6a7ad04f472",
    "name": "Nouvel ingrédient",
    "slug": "nouvelingredient",
    "category": {
        "id": "644fbb9215f67a77ac0515d7",
        "name": "Catégorie d'ingrédients"
    },
    "owner": {
        "id": "6460eb0f5983b6a7ad04f464",
        "email": "shop1@brand.cool"
    },
    "privacy": "PUBLIC"
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->
<!-- DÉBUT DE LA ROUTE -->
## update-one
----
USER
{: .label .label-yellow }

> Modifie un document `Ingrédient` existant avec de nouvelles valeurs, à condition que l'utilisateur authentifié en soit le propriétaire.

> Pour plus d'informations à propos de l'authentification et des droits d'accès aux données : lire la section [Security].


### Requête

{: .request-put }
> https://api.sharlotte.fr/ingredients/*_id*

### Paramètres

| Paramètres | Valeurs                                               |
|:-----------|:------------------------------------------------------|
| *_id*      | identifiant unique du document `Ingrédient` recherché |

### Body
{% capture _code %}{% highlight json linenos %}
{
    "name": "Nouveau nom",
    "calorie":245
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6462baa4b24b095c4207a992",
    "name": "Nouveau nom",
    "slug": "nouveaunom",
    "calorie":245
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->
<!-- DÉBUT DE LA ROUTE -->
## delete-one
----
USER
{: .label .label-yellow }

> Supprime un document `Ingrédient` existant de la base de données, à condition que l'utilisateur authentifié en soit le propriétaire.

> Pour plus d'informations à propos de l'authentification et des droits d'accès aux données : lire la section [Security].

### Requête

{: .request-delete }
> https://api.sharlotte.fr/ingredients/*_id*

### Paramètres

| Paramètres | Valeurs                                               |
|:-----------|:------------------------------------------------------|
| *_id*      | identifiant unique du document `Ingrédient` recherché |

### Body
*Aucun contenu n'est nécessaire*

### Réponse
> HTTP - 204 - No Content
<!-- FIN DE LA ROUTE -->

----

[Product]: /User/produits.html
[IngredientCategory]: ingredientCategory.html
[Security]: security.html
[User]: /User/index.html
[get-all]: #get-all
[get-one]: #get-one
[create-one]: #create-one
[update-one]: #update-one
[delete-one]: #delete-one