---
title: Acerca de la membresía de una organización
intro: Puedes convertirte en miembro de una organización para colaborar con los compañeros de trabajo o los colaboradores de código abierto en muchos repositorios a la vez.
redirect_from:
  - /articles/about-organization-membership
  - /github/setting-up-and-managing-your-github-user-account/about-organization-membership
  - /github/setting-up-and-managing-your-github-user-account/managing-your-membership-in-organizations/about-organization-membership
  - /account-and-profile/setting-up-and-managing-your-github-user-account/managing-your-membership-in-organizations/about-organization-membership
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
topics:
  - Accounts
shortTitle: Membresía de la organización
---

Un propietario de la organización puede invitarte a unirte a su organización como miembro, gerente de facturación o propietario. Un miembro o propietario de la organización con privilegios de administrador para un repositorio puede invitarte a colaborar en uno o más repositorios como un colaborador externo. Para obtener más información, consulta la sección "[Roles en una organización](/organizations/managing-peoples-access-to-your-organization-with-roles/roles-in-an-organization)".

Puedes acceder a las organizaciones de las que eres miembro en tu página de perfil. Para obtener más información, consulta "[Acceder a una organización](/articles/accessing-an-organization)".

Cuando aceptas una invitación para unirte a una organización, el propietario de la organización puede ver lo siguiente:

- La información de tu perfil público.
- Tu dirección de correo electrónico.
- Si tienes la autorización de dos factores activada.
- Los repositorios a los que tienes acceso dentro de la organización y tu nivel de acceso.
- Ciertas actividades dentro de la organización.
- País del origen de la solicitud.
- Tu dirección IP.

Para obtener más información, consulta la <a href="/articles/github-privacy-statement/" class="dotcom-only">{% data variables.product.prodname_dotcom %} Declaración de privacidad</a>.

  {% note %}

  **Nota:** Los propietarios no pueden ver las direcciones IP del miembro en el registro de auditoría de la organización. En el caso de un incidente de seguridad, como una cuenta comprometida o la divulgación involuntaria de datos confidenciales, los propietarios de la organización pueden solicitar los detalles de acceso a los repositorios privados. La información que devolvemos puede incluir tu dirección IP.

  {% endnote %}

Por defecto, la visibilidad de los miembros de tu organización se establece como privada. Puede elegir publicar miembros individuales de la organización en tu perfil. Para obtener más información, consulta "[Publicar u ocultar los miembros de la organización](/articles/publicizing-or-hiding-organization-membership)".

{% ifversion fpt or ghec %}

Si tu organización pertenece a una cuenta de empresa, automáticamente eres un miembro de la cuenta de empresa y visible para los propietarios de la cuenta de empresa. Para obtener más información, consulta la sección "[Acerca de las cuentas empresariales](/enterprise-cloud@latest/admin/overview/about-enterprise-accounts){% ifversion fpt %}" en la documentación de {% data variables.product.prodname_ghe_cloud %}.{% else %}".{% endif %}

{% endif %}

Puedes dejar una organización en cualquier momento. Para obtener más información, consulta "[Cómo eliminarte de una organización](/articles/removing-yourself-from-an-organization)".

## Leer más

- "[Acerca de las organizaciones](/articles/about-organizations)"
- "[Administrar tu membresía en organizaciones](/articles/managing-your-membership-in-organizations)"
