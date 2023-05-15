---
title: Alias
layout: default
---

# Alias
La table Alias stockent en base de données la liste des noms pouvant être utilisés pour la création d'un document de type [Units]. L'alias doit être un (ou plusieurs) mot simple qui représente un conditionnement sous lequel on peut retrouver un ingrédient dans une recette

{: .highlight }
exemple : tranche, gousse, boite, paquet, pièce...



If [Jekyll] is installed on your computer, you can also build and preview the created site *locally*. This lets you test changes before committing them, and avoids waiting for GitHub Pages.[^1] And you will be able to deploy your local build to a different platform than GitHub Pages.

More specifically, the created site:

- uses a gem-based approach, i.e. uses a `Gemfile` and loads the `just-the-docs` gem
- uses the [GitHub Pages / Actions workflow] to build and publish the site on GitHub Pages

Other than that, you're free to customize sites that you create with this template, however you like. You can easily change the versions of `just-the-docs` and Jekyll it uses, as well as adding further plugins.

{: .note-title }
> GET
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

[Units]: 
