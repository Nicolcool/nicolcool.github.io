---
title: IngredientCategory
layout: default
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

<!-- DÉBUT DE LA ROUTE -->
## get-all
----
PUBLIC
{: .label .label-green }

> Renvoie la liste de tous les `IngredientCategory` qui existent en base de données.


### Requête

{: .request-get }
> https://api.sharlotte.fr/ingredientcats

### Paramètres
*Aucun contenu n'est nécessaire*

### Body
*Aucun contenu n'est nécessaire*

### Réponse
{% capture _code %}{% highlight json linenos %}
[{
    "id": "6460eb105983b6a7ad04f467",
    "name": "Viandes",
    "description": "Eum et et minima soluta eos molestiae earum molestias. Illo velit veniam et unde placeat et dolorem reprehenderit."
},
{
    "id": "6460eb105983b6a7ad04f468",
    "name": "Fromages",
    "description": "Doloremque quod qui neque consequatur. Nam facere sed reprehenderit exercitationem ut mollitia quo fugit. Fuga iste perferendis quod tenetur ut consequatur ut eos."
}]
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->
<!-- DÉBUT DE LA ROUTE -->
## get-one
----
PUBLIC
{: .label .label-green }

> Renvoie les informations d'un seul document `IngredientCategory` depuis son identifiant unique.

### Requête

{: .request-get }
> https://api.sharlotte.fr/ingredientcats/*_id*

### Paramètres

| Paramètres | Valeurs                                                       |
|:-----------|:--------------------------------------------------------------|
| *_id*      | identifiant unique du document `IngredientCategory` recherché |

### Body
*Aucun contenu n'est nécessaire*

### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6460eb105983b6a7ad04f467",
    "name": "Viandes",
    "description": "Eum et et minima soluta eos molestiae earum molestias. Illo velit veniam et unde placeat et dolorem reprehenderit."
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->
<!-- DÉBUT DE LA ROUTE -->
## create-one
----
ADMIN
{: .label .label-red }

> Créer et ajoute un document `IngredientCategory` à la base de données.


### Requête

{: .request-post }
> https://api.sharlotte.fr/admin/ingredientcats

### Paramètres
*Aucun contenu n'est nécessaire*

### Body
{% capture _code %}{% highlight json linenos %}
{
    "name":"Nouvelle catégorie",
    "description":"Lorem ipsum dolor sit amet, consectetur adipiscing elit."
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6462cc280d8c1c3efd0b43d2",
    "name": "Nouvelle catégorie",
    "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit."
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->
<!-- DÉBUT DE LA ROUTE -->
## update-one
----
ADMIN
{: .label .label-red }

> Modifie un document `IngredientCategory` existant avec de nouvelles valeurs.


### Requête

{: .request-put }
> https://api.sharlotte.fr/admin/ingredientcats/*_id*

### Paramètres

| Paramètres | Valeurs                                                       |
|:-----------|:--------------------------------------------------------------|
| *_id*      | identifiant unique du document `IngredientCategory` recherché |

### Body
{% capture _code %}{% highlight json linenos %}
{
    "name": "Nouveau nom",
    "description":"Nouvelle description"
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6462cc280d8c1c3efd0b43d2",
    "name": "Nouveau nom",
    "description":"Nouvelle description"
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->
<!-- DÉBUT DE LA ROUTE -->
## delete-one
----
ADMIN
{: .label .label-red }

> Supprime un document `IngredientCategory` existant de la base de données.

### Requête

{: .request-delete }
> https://api.sharlotte.fr/admin/ingredientcats/*_id*

### Paramètres

| Paramètres | Valeurs                                                       |
|:-----------|:--------------------------------------------------------------|
| *_id*      | identifiant unique du document `IngredientCategory` recherché |

### Body
*Aucun contenu n'est nécessaire*

### Réponse
> HTTP - 204 - No Content
<!-- FIN DE LA ROUTE -->

----

[Ingredient]: ingredient.html
[get-all]: #get-all
[get-one]: #get-one
[create-one]: #create-one
[update-one]: #update-one
[delete-one]: #delete-one