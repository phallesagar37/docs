---
title: Configurar un procesador Markdown para tu sitio de páginas de GitHub usando Jekyll
intro: 'Puedes elegir un procesador Markdown para determinar la manera en que Markdown se representa en tu sitio de {% data variables.product.prodname_pages %}.'
redirect_from:
  - /articles/migrating-your-pages-site-from-maruku
  - /articles/updating-your-markdown-processor-to-kramdown
  - /articles/setting-a-markdown-processor-for-your-github-pages-site-using-jekyll
  - /github/working-with-github-pages/setting-a-markdown-processor-for-your-github-pages-site-using-jekyll
product: '{% data reusables.gated-features.pages %}'
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
topics:
  - Pages
shortTitle: Configurar un procesador de lenguaje de marcado
---

Las personas con permisos de escritura para un repositorio pueden configurar el procesador Markdown para un sitio de {% data variables.product.prodname_pages %}.

{% data variables.product.prodname_pages %} es compatible con dos procesadores de lenguaje de marcado: [kramdown](http://kramdown.gettalong.org/) y el procesador de lenguaje de marcado propio de {% data variables.product.prodname_dotcom %}, el cual se utiliza para procesar el [{% data variables.product.prodname_dotcom %} Lenguaje de marcado enriquecido (GFM)](https://github.github.com/gfm/) a través de {% data variables.product.product_name %}. Para obtener más información, consulta "[Acerca de la escritura y el formato en {% data variables.product.prodname_dotcom %}](/articles/about-writing-and-formatting-on-github)."

Puedes utilizar el Lenguaje de Marcado Enriquecido de {% data variables.product.prodname_dotcom %} con cualquier procesador, pero solo tu procesador de GFM empatará siempre con los resultados que ves en {% data variables.product.product_name %}.

{% data reusables.pages.navigate-site-repo %}
2. En tu repositorio, navega hasta el archivo *_config.yml*.
{% data reusables.repositories.edit-file %}
4. Encuentra la línea que comienza con `markdown:` y cambia el valor a `kramdown` o `GFM`. ![Configuración Markdown en config.yml](/assets/images/help/pages/config-markdown-value.png)
{% data reusables.files.write_commit_message %}
{% data reusables.files.choose-commit-email %}
{% data reusables.files.choose_commit_branch %}
{% data reusables.files.propose_new_file %}

## Leer más

- [Documentación de kramdown](https://kramdown.gettalong.org/documentation.html)
- [{% data variables.product.prodname_dotcom %} Especificaciones del formato Markdown](https://github.github.com/gfm/)
