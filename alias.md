---
title: Alias
layout: default
---

# Alias
----

La table Alias stockent en base de données la liste des noms pouvant être utilisés pour la création d'un document de type [Units]. L'alias doit être un (ou plusieurs) mot simple qui représente un conditionnement sous lequel on peut retrouver un ingrédient dans une recette


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

### Validation BDD

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

### Validation Serveur

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

{: .request }
> **GET**
>
> A paragraph


{% capture _code %}{% highlight php linenos %}
public function setId(string $id): self{
    $this->id = $id;
    return $this;
}
{% endhighlight %}{% endcapture %}{% include fixlinenos.html %}{{ _code }}

[Browse our documentation][Just the Docs] to learn more about how to use this theme.

To `get started` with creating a site, just click "[use this template]"!

If you want to maintain your docs in the `docs` directory of an existing project repo, see [Hosting your docs from an existing project repo](https://github.com/just-the-docs/just-the-docs-template/blob/main/README.md#hosting-your-docs-from-an-existing-project-repo) in the template README.

----

[^1]: [It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site).

[Units]: https://github.com/
