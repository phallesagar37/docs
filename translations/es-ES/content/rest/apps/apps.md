---
title: GitHub Apps
allowTitleToDifferFromFilename: true
intro: 'The {% data variables.product.prodname_github_apps %} API enables you to retrieve information about {% data variables.product.prodname_github_apps %}.'
topics:
  - API
miniTocMaxHeadingLevel: 3
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
---

## About the {% data variables.product.prodname_github_apps %} API

{% data reusables.apps.general-apps-restrictions %}

Esta página lista las terminales a las que puedes acceder mientras te autenticas como una GitHub App. Consulta la sección "[Autenticarse como una GitHub App](/apps/building-github-apps/authenticating-with-github-apps/#authenticating-as-a-github-app)" para conocer más.

Cuando estás autenticado como una GitHub App, la API de GitHub Apps te habilita para obtener información de alto nivel sobre una GitHub App así como para obtener información específica sobre las instalaciones de éstas.

Puedes acceder a las terminales de la API v3 de REST mientras estás autenticado como una GitHub App. These endpoints have text that says "Works with GitHub Apps." También puedes acceder a estas terminales mientras estás autenticado como un usuario.

Un subconjunto de terminales de la API v3 de REST requiere que te autentiques como una instalación de una GitHub App. Consulta las [Instalaciones](/rest/reference/apps#installations) para obtener una lista de estas terminales.
