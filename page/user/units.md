---
title: Units
layout: default
---

# Alias
----

> Le champs `units` du document [User] stocke la liste des unités personnalisée créées par l'utilisateur. L'unité utilisées dans tous les calculs est toujours le gramme, c'est la plus pratique et la plus précise pour le calcul des recettes, infos nutritionnelles etc. En revanche il peut arriver qu'une unité personnalisée soit plus pratique à l'usage. Dans ce cas l'utilisateur peut créer sa propre unité pour un ingrédient donné.


{: .example }
L'ingrédient `Jambon blanc, cuit` est parfois exprimé au poids dans les recettes. Mais il peut arriver (par exemple avec des petites quantités) qu'il soit plus pratique de travailler en tranches.

Un document `units` associe ensembles un [Ingredient], un [Alias] et une quantité.


## Structure
----

| Champs     | Description                                                        | type     | Requis | Unique |
|:-----------|:-------------------------------------------------------------------|:---------|:-------|:-------|
| id         | identifiant unique MongoDB                                         | objectId | Oui    | Oui    |
| ingredient | L'ingrédient ciblé par l'unité. Référence un document [Ingredient] | objectId | Oui    | Oui    |
| alias      | L'alias associé à l'ingrédient. Référence un document [Alias]      | objectId | Oui    | Oui    |
| value      | Une quantité exprimée en gramme                                    | double   | Oui    | Oui    |

{: .example }
| id                 | ingredient         | alias   | value |
|:-------------------|:-------------------|:--------|:------|
| identifiant unique | jambon blanc, cuit | tranche | 45    |

> Ici on indique qu'une tranche de jambon pèse 45g. Dans une recette on pourra exprimé la quantité en nombre de tranches, quand c'est nécéssaire Sharlotte pourra la convertir en gramme pour traiter les données (calcul des infos nutritionnelles par exemple).


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

<!-- DÉBUT DE LA ROUTE -->
## get-all
----
PUBLIC
{: .label .label-green }

> Renvoie la liste de tous les `Alias` qui existent en base de données.


### Requête

{: .request-get }
> https://api.sharlotte.fr/alias

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
<!-- FIN DE LA ROUTE -->
<!-- DÉBUT DE LA ROUTE -->
## get-one
----
PUBLIC
{: .label .label-green }

> Renvoie les informations d'un seul document `Alias` depuis son identifiant unique.


### Requête

{: .request-get }
> https://api.sharlotte.fr/alias/*_id*

### Paramètres

| Paramètres | Valeurs                                          |
|:-----------|:-------------------------------------------------|
| *_id*      | identifiant unique du document `alias` recherché |

### Body
*Aucun contenu n'est nécessaire*

### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "6460eb105983b6a7ad04f46d",
    "name": "tranche"
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->
<!-- DÉBUT DE LA ROUTE -->
## create-one
----
ADMIN
{: .label .label-red }

> Créer et ajoute un document `Alias` à la base de données.


### Requête

{: .request-post }
> https://api.sharlotte.fr/admin/alias

### Paramètres
*Aucun contenu n'est nécessaire*

### Body
{% capture _code %}{% highlight json linenos %}
{
    "name": "nouvelalias"
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "64620c30dbf19f8fae0dae42",
    "name": "nouvelalias"
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->
<!-- DÉBUT DE LA ROUTE -->
## update-one
----
ADMIN
{: .label .label-red }

> Modifie un document `Alias` existant avec de nouvelles valeurs.


### Requête

{: .request-put }
> https://api.sharlotte.fr/admin/alias/*_id*

### Paramètres

| Paramètres | Valeurs                                          |
|:-----------|:-------------------------------------------------|
| *_id*      | identifiant unique du document `alias` recherché |

### Body
{% capture _code %}{% highlight json linenos %}
{
    "name": "nouveaunom"
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

### Réponse
{% capture _code %}{% highlight json linenos %}
{
    "id": "64620c30dbf19f8fae0dae42",
    "name": "nouveaunom"
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}
<!-- FIN DE LA ROUTE -->
<!-- DÉBUT DE LA ROUTE -->
## delete-one
----
ADMIN
{: .label .label-red }

> Supprime un document `Alias` existant de la base de données.


### Requête

{: .request-delete }
> https://api.sharlotte.fr/admin/alias/*_id*

### Paramètres

| Paramètres | Valeurs                                          |
|:-----------|:-------------------------------------------------|
| *_id*      | identifiant unique du document `alias` recherché |

### Body
*Aucun contenu n'est nécessaire*

### Réponse
> HTTP - 204 - No Content
<!-- FIN DE LA ROUTE -->
----

[User]: index.md
[Alias]: ../alias.md
[Ingredient]: ../ingredient.md
[get-all]: #get-all
[get-one]: #get-one
[create-one]: #create-one
[update-one]: #update-one
[delete-one]: #delete-one