---
title: Alias
layout: default
---

# Alias
----

La table `Alias` stockent en base de données la liste des noms pouvant être utilisés pour la création d'un document de type [Units]. `Alias` doit être un (ou plusieurs) mot simple qui représente un conditionnement sous lequel on peut retrouver un ingrédient dans une recette


{: .example }
tranche, gousse, boite, paquet, pièce...


## Structure
----

| Champs | Description                | type     | Requis | Unique |
|:-------|:---------------------------|:---------|:-------|:-------|
| id     | identifiant unqiue MongoDB | objectId | Oui    | Oui    |
| name   | Un mot simple et explicite | string   | Oui    | Oui    |


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

1. [get-all]
1. [get-one]
1. [create-one]
1. [update-one]
1. [delete-one]

## get-all
PUBLIC
{: .label .label-green }

Renvoie la liste de tous les `Alias` qui existent en base de données.


### Requête
{: .request-get }
{{ base_url }}/alias

### Paramètres
*Aucun paramètre n'est nécessaire*

### Body
*Aucun contenu n'est nécessaire*

### Réponse
{% capture _code %}{% highlight json linenos %}
[{
    "id": "6460eb105983b6a7ad04f46d",
    "name": "tranche"
},
{
    "id": "6460eb105983b6a7ad04f46e",
    "name": "boite"
}]
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}



# Liens
----
[Units]: https://github.com/
[get-all]: #routes
[get-one]: #routes
[create-one]: #routes
[update-one]: #routes
[delete-one]: #routes