---
title: User > Sources
layout: default
nav_order: 3
has_children: true
---

# Sources
----

> Le champs `sources` du document [User] permets à l'utilisateur d'enregistrer en base de données différentes sources d'approvisionnement pour un ingrédient donné. Un document `sources` associe ensembles un [Ingredient] et un [Supplier] en y ajoutant des informations additionnelles comme un prix.

## Structure
----

| Champs     | Description                                                        | type     | Requis | Unique |
|:-----------|:-------------------------------------------------------------------|:---------|:-------|:-------|
| id         | identifiant unique MongoDB                                         | objectId | Oui    | Oui    |
| ingredient | L'ingrédient ciblé par l'unité. Référence un document [Ingredient] | objectId | Oui    | Oui    |
| alias      | L'alias associé à l'ingrédient. Référence un document [Alias]      | objectId | Oui    | Oui    |
| value      | Une quantité exprimée en gramme                                    | double   | Oui    | Oui    |

{: .example }
Ci-dessous, on indique qu'une tranche de jambon pèse 45g. Dans une recette on pourra exprimé la quantité en nombre de tranches, quand c'est nécéssaire Sharlotte pourra la convertir en gramme pour traiter les données (calcul des infos nutritionnelles par exemple).

| id  | ingredient         | alias   | value |
|:----|:-------------------|:--------|:------|
| _id | jambon blanc, cuit | tranche | 45    |

## Validation
----

### Base de données

{% capture _code %}{% highlight json linenos %}
"$jsonSchema": {
    "required": ["name"],
    "properties": {
        "name": {
            "bsonType": "string",
            "description": "must be a string and is required."
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

1. [get-user-all]

----

[User]: ../user/index.html
[Ingredient]: ../ingredient/index.html
[Supplier]: ../supplier/index.html
[Alias]: ../alias/index.html
[get-user-all]: get-user-all.html