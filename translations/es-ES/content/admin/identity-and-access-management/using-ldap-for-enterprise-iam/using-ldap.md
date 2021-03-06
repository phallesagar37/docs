---
title: Usar LDAP
redirect_from:
  - /enterprise/admin/articles/configuring-ldap-authentication
  - /enterprise/admin/articles/about-ldap-authentication
  - /enterprise/admin/articles/viewing-ldap-users
  - /enterprise/admin/hidden/enabling-ldap-sync
  - /enterprise/admin/hidden/ldap-sync
  - /enterprise/admin/user-management/using-ldap
  - /enterprise/admin/authentication/using-ldap
  - /admin/authentication/using-ldap
  - /enterprise/admin/authentication/authenticating-users-for-your-github-enterprise-server-instance/using-ldap
  - /admin/identity-and-access-management/authenticating-users-for-your-github-enterprise-server-instance/using-ldap
intro: 'If you use Lightweight Directory Access Protocol (LDAP) to centralize access across applications, you can integrate {% data variables.product.product_name %} by configuring LDAP authentication for your instance.'
versions:
  ghes: '*'
type: how_to
topics:
  - Accounts
  - Authentication
  - Enterprise
  - Identity
---

## About LDAP authentication for {% data variables.product.product_name %}

LDAP is a popular application protocol for access and maintenance of directory information services, and is one of the most common protocols for integration of third-party software with large company user directories. For more information, see "[Lightweight Directory Access Protocol](https://en.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol)" on Wikipedia.

If you use an LDAP directory for centralized authentication, you can configure LDAP authentication for the people who use {% data variables.product.product_location %}.

{% data reusables.enterprise_user_management.built-in-authentication %}

## Servicios LDAP admitidos

El {% data variables.product.prodname_ghe_server %} se integra con los siguientes servicios LDAP:

* Active Directory
* FreeIPA
* Oracle Directory Server Enterprise Edition
* OpenLDAP
* Open Directory
* 389-ds

## Consideraciones sobre el nombre de usuario con LDAP

{% data reusables.enterprise_user_management.consider-usernames-for-external-authentication %} Para obtener m??s informaci??n, consulta la secci??n "[Consideraciones de nombre de usuario para la autenticaci??n externa](/admin/identity-and-access-management/managing-iam-for-your-enterprise/username-considerations-for-external-authentication)".

## Configurar LDAP con {% data variables.product.product_location %}

Una vez configurado LDAP, los usuarios podr??n iniciar sesi??n en tu instancia con sus credenciales LDAP. Cuando los usuarios inician sesi??n por primera vez, sus nombres de perfil, direcciones de correo electr??nico y claves SSH se establecen con los atributos de LDAP desde tu directorio.

Cuando configuras el acceso de LDAP para los usuarios a trav??s de {% data variables.enterprise.management_console %}, tus licencias de usuario no se utilizar??n sino hasta que los usuarios ingresen en tu instancia por primera vez. Sin embargo, si creas una cuenta manualmente utilizando la configuraci??n de administrador para el sitio, esta licencia de usuario se tomar?? en cuenta.

{% warning %}

**Advertencia:** Antes de configurar LDAP en {% data variables.product.product_location %}, aseg??rate de que tu servicio LDAP admita resultados paginados.

{% endwarning %}

{% data reusables.enterprise_site_admin_settings.access-settings %}
{% data reusables.enterprise_site_admin_settings.management-console %}
{% data reusables.enterprise_management_console.authentication %}
3. En "Authentication" (Autenticaci??n), selecciona **LDAP**. ![Seleccionar LDAP](/assets/images/enterprise/management-console/ldap-select.png)
4. {% data reusables.enterprise_user_management.built-in-authentication-option %} ![Seleccionar la casilla de verificaci??n autenticaci??n integrada LDAP](/assets/images/enterprise/management-console/ldap-built-in-authentication.png)
5. Agrega tus par??metros de configuraci??n.

## Atributos de LDAP
Usa estos atributos para terminar de configurar LDAP para {% data variables.product.product_location %}.

| Nombre del atributo                                                                                             | Tipo      | Descripci??n                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| --------------------------------------------------------------------------------------------------------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Host`                                                                                                          | Requerido | El host LDAP, p. ej. `ldap.example.com` o `10.0.0.30`. Si el nombre del host solo est?? disponible desde tu red interna, es posible que primero debas configurar el DNS de {% data variables.product.product_location %} para que pueda resolver el nombre del host usando tus servidores de nombres internos.                                                                                                                                                                                                                                                                 |
| `Port (Puerto)`                                                                                                 | Requerido | El puerto que est??n escuchando los servicios LDAP. Los ejemplos incluyen: 389 y 636 (para LDAPS).                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `Encryption (Cifrado)`                                                                                          | Requerido | El m??todo de cifrado usado para garantizar las comunicaciones con el servidor LDAP. Los ejemplos incluyen el normal (sin cifrado), el SSL/LDAPS (cifrado desde el principio) y el StartTLS (se actualiza a comunicaci??n cifrada una vez que se conecta).                                                                                                                                                                                                                                                                                                                      |
| `Usuario de b??squeda de dominio`                                                                                | Opcional  | El usuario LDAP que busca a otros usuarios que iniciaron sesi??n, para permitir la autenticaci??n. Esto suele ser una cuenta de servicio creada espec??ficamente para integraciones de terceros. Usa un nombre certificado completo, como `cn=Administrator,cn=Users,dc=Example,dc=com`. Con Active Directory, tambi??n puedes usar la sintaxis `[DOMAIN]\[USERNAME]` (p. ej.,`WINDOWS\Administrator`) para el usuario de b??squeda de dominio.                                                                                                                                  |
| `Domain search password (Contrase??a de b??squeda de dominio)`                                                    | Opcional  | La contrase??a para el usuario de b??squeda de dominio.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `Grupo de administradores`                                                                                      | Opcional  | Los usuarios de este grupo son promovidos a administradores del sitio cuando inician sesi??n en tu aparato. Si no configuras un Grupo de administradores LDAP, la primera cuenta de usuario LDAP que inicie sesi??n en tu aparato ser?? promovida autom??ticamente a administrador del sitio.                                                                                                                                                                                                                                                                                     |
| `Domain base (Base de dominio)`                                                                                 | Requerido | El `Nombre Distintivo` (DN) completamente calificado de un sub??rbol LDAP que quieras buscar para usuarios y grupos. Puedes agregar tantos como quieras; sin embargo, cada grupo debe estar definido en la misma base de dominio que los usuarios que le pertenecen. Si especificas grupos de usuarios con restricciones, solo los usuarios que pertenecen a esos grupo estar??n al alcance. Te recomendamos que especifiques el primer nivel de tu ??rbol de directorios LDAP como tu base de dominio y que uses grupos de usuarios con restricciones para controlar el acceso. |
| `Restricted user groups (Grupos de usuarios con restricciones)`                                                 | Opcional  | Si se especifica, solo los usuarios de estos grupos tendr??n permiso para iniciar sesi??n. Solo necesitas especificar los nombres comunes (CN) de los grupos y puedes agregar tantos grupos como quieras. Si no se especifica ning??n grupo, *todos* los usuarios dentro del alcance de la base de dominio especificada podr??n iniciar sesi??n en tu instancia del {% data variables.product.prodname_ghe_server %}.                                                                                                                                                            |
| `User ID (Identificaci??n de usuario)`                                                                           | Requerido | El atributo de LDAP que identifica al usuario LDAP que intenta una autenticaci??n. Una vez que se establece una asignaci??n, los usuarios pueden modificar sus nombres de usuario del {% data variables.product.prodname_ghe_server %}. El campo deber??a ser `sAMAccountName` para la mayor??a de las instalaciones de Active Directory, pero puede ser `uid` para otras soluciones LDAP, como OpenLDAP. El valor predeterminado es `uid`.                                                                                                                                     |
| `Nombre de perfil`                                                                                              | Opcional  | El nombre que aparecer?? en la p??gina de perfil del {% data variables.product.prodname_ghe_server %} del usuario. A menos que la sincronizaci??n LDAP est?? activada, los usuarios pueden modificar sus nombres de perfil.                                                                                                                                                                                                                                                                                                                                                     |
| `Emails (Correos electr??nicos)`                                                                                 | Opcional  | Las direcciones de correo electr??nico para la cuenta del {% data variables.product.prodname_ghe_server %} de un usuario.                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `SSH keys (Claves SSH)`                                                                                         | Opcional  | Las claves SSH p??blicas vinculadas a la cuenta del {% data variables.product.prodname_ghe_server %} de un usuario. Las claves deben ser en formato OpenSSH.                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `Claves GPG`                                                                                                    | Opcional  | Las claves GPG vinculadas a la cuenta del {% data variables.product.prodname_ghe_server %} de un usuario.                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `Disable LDAP authentication for Git operations (Desactivar la autenticaci??n LDAP para las operaciones de Git)` | Opcional  | Si est?? seleccionado, [desactiva](#disabling-password-authentication-for-git-operations) la posibilidad del usuario de usar contrase??as LDAP para autenticar las operaciones de Git.                                                                                                                                                                                                                                                                                                                                                                                          |
| `Enable LDAP certificate verification (Activar la verificaci??n de certificado LDAP)`                            | Opcional  | Si est?? seleccionado, [activa](#enabling-ldap-certificate-verification) la verificaci??n de certificado LDAP.                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `Synchronization (Sincronizaci??n)`                                                                              | Opcional  | Si est?? seleccionado, [activa](#enabling-ldap-sync) la sincronizaci??n LDAP.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

### Desactivar la autenticaci??n de contrase??a para las operaciones de Git

Selecciona **Disable username and password authentication for Git operations** (Desactivar la autenticaci??n de nombre de usuario y contrase??a para las operaciones de Git) en los par??metros de tu LDAP para implementar el uso de los tokens de acceso personal o las claves SSH para el acceso a Git, que pueden ayudarte a prevenir que tu servidor se sobrecargue de solicitudes de autenticaci??n LDAP. Recomendamos esta configuraci??n, ya que un servidor LDAP de respuesta lenta, en especial combinado con una gran cantidad de solicitudes debido al sondeo, suele ser una causa de problemas e interrupciones.

![Desactivar la casilla de verificaci??n autenticaci??n de contrase??a LDAP](/assets/images/enterprise/management-console/ldap-disable-password-auth-for-git.png)

Cuando se selecciona esta opci??n, si un usuario intenta usar una contrase??a para las operaciones de Git a trav??s de la l??nea de comando, recibir?? un mensaje de error que dice: `La autenticaci??n de contrase??a no est?? permitida para las operaciones de Git. Debes usar un token de acceso personal.`

### Activar la verificaci??n de certificado LDAP

Selecciona **Enable LDAP certificate verification** (Activar verificaci??n de certificado LDAP) en tus par??metros LDAP para validar el certificado del servidor LDAP que usas con TLS.

![Casilla de verificaci??n de certificado LDAP](/assets/images/enterprise/management-console/ldap-enable-certificate-verification.png)

Cuando se selecciona esta opci??n, el certificado se valida para garantizar que:
- Si el certificado contiene al menos un nombre alternativo del firmante (SAN), uno de los SAN coincida con el nombre del host de LDAP. De lo contrario, que el nombre com??n (CN) coincida con el nombre del host de LDAP.
- El certificado no haya vencido.
- El certificado est?? firmado por una entidad de certificaci??n (CA) de confianza.

### Activar la sincronizaci??n LDAP

{% note %}

**Nota:** Los equipos que utilizan sincronizaci??n de LDAP se limitan a un m??ximo de 1499 miembros.

{% endnote %}

La sincronizaci??n LDAP te permite sincronizar usuarios y miembros del equipo del {% data variables.product.prodname_ghe_server %} con tus grupos LDAP establecidos. Esto te permite establecer un control de acceso basado en roles para los usuarios desde tu servidor LDAP, en lugar de hacerlo de forma manual dentro del {% data variables.product.prodname_ghe_server %}. Para obtener m??s informaci??n, consulta la secci??n "[Crear equipos](/enterprise/admin/guides/user-management/creating-teams#creating-teams-with-ldap-sync-enabled)."

Para activar la sincronizaci??n LDAP, en tus par??metros LDAP, selecciona **Synchronize Emails** (Sincronizar correos electr??nicos), **Synchronize SSH Keys** (Sincronizar claves SSH) o **Synchronize GPG Keys** (Sincronizar claves GPG).

![Casilla de verificaci??n de Sincronizaci??n](/assets/images/enterprise/management-console/ldap-synchronize.png)

Una vez que actives la sincronizaci??n LDAP, se ejecutar?? un trabajo de sincronizaci??n en el intervalo de tiempo especificado para realizar las siguientes operaciones en cada cuenta de usuario:

- Si has permitido la autenticaci??n integrada para usuarios externos a tu proveedor de identidad, y el usuario est?? usando la autenticaci??n integrada, pasa al siguiente usuario.
- Si no existe una asignaci??n LDAP para el usuario, intenta asignar el usuario a una entrada LDAP en el directorio. Si el usuario no se puede asignar a una entrada LDAP, susp??ndelo y pasa al siguiente usuario.
- Si hay una asignaci??n LDAP y falta la entrada LDAP correspondiente en el directorio, suspende el usuario y pasa al siguiente usuario.
- Si la entrada LDAP correspondiente se marc?? como desactivada, y el usuario a??n no se suspendi??, susp??ndelo y pasa al siguiente usuario.
- Si la entrada LDAP correspondiente no se marc?? como desactivada, el usuario est?? suspendido y _Reactivate suspended users_ (Reactivar usuarios suspendidos) est?? activado en el centro de administraci??n, anula la suspensi??n del usuario.
- Si uno o m??s grupos de usuarios restringidos se configuran en la instancia y la entrada de LDAP correspondiente no est?? en uno de estos grupos, suspende al usuario.
- Si se configuran uno o m??s grupos de usuarios restringidos en la instancia, la entrada de LDAP correspondiente se encuentra en alguno de estos grupos y _Reactivar usuarios suspendidos_ se encuentra habilitado en el Centro de Administraci??n, deja de suspender al usuario.
- Si la entrada LDAP correspondiente incluye un atributo `name`, actualiza el nombre de perfil del usuario.
- Si la entrada LDAP correspondiente est?? en el grupo de administradores, promueve al usuario a administrador del sitio.
- Si la entrada LDAP correspondiente no est?? en el grupo de administradores, degrada al usuario a una cuenta normal.
- Si un campo de usuario LDAP est?? definido para correos electr??nicos, sincroniza los par??metros del correo electr??nico del usuario con la entrada LDAP. Establece la primera entrada `mail` LDAP como el correo electr??nico principal.
- Si un campo de usuario LDAP est?? definido para claves p??blicas SSH, sincroniza las claves SSH p??blicas del usuario con la entrada LDAP.
- Si un campo de usuario LDAP est?? definido para claves GPG, sincroniza las claves GPG del usuario con la entrada LDAP.

{% note %}

**Nota**: Las entradas LDAP solo pueden estar marcadas como desactivadas si usas Active Directory y el atributo `userAccountControl` est?? presente y marcado con `ACCOUNTDISABLE`. Algunas variaciones de Active Directory, tales como AD LDS y ADAM, no son compatibles con el atributo `userAccountControl`.

{% endnote %}

Tambi??n se ejecutar?? un trabajo de sincronizaci??n en el intervalo de tiempo especificado para realizar las siguientes operaciones en cada equipo que haya sido asignado a un grupo LDAP:

- Si se elimin?? el grupo LDAP correspondiente de un equipo, elimina todos los miembros del equipo.
- Si las entradas de miembros LDAP se eliminaron del grupo LDAP, elimina los usuarios correspondientes del equipo. Si el usuario ya no es miembro de ning??n equipo en la organizaci??n, ret??ralo de esta. Si como resultado el usuario pierde acceso a alg??n repositorio, elimina toda bifurcaci??n privada que el usuario tenga de esos repositorios.
- Si las entradas de miembros LDAP se agregaron al grupo LDAP, agrega los usuarios correspondientes al equipo. Si como resultado el usuario recupera el acceso a alg??n repositorio, restablece toda bifurcaci??n privada de los repositorios que haya sido eliminada debido a que el usuario perdi?? acceso en los ??ltimos 90 d??as.

{% data reusables.enterprise_user_management.ldap-sync-nested-teams %}

{% warning %}

**Advertencia de seguridad:**

Cuando la sincronizaci??n LDAP est?? activada, los administradores del sitio y los propietarios de la organizaci??n pueden buscar en el directorio LDAP los grupos a los cuales asignar el equipo.

Esto posibilita divulgar informaci??n organizativa confidencial a contratistas u otros usuarios sin privilegios, incluidos los siguientes:

- La existencia de grupos LDAP espec??ficos visibles para el *Usuario de b??squeda de dominio*.
- Los miembros del grupo LDAP que tienen cuentas de usuario del {% data variables.product.prodname_ghe_server %}, que se divulga cuando se crea un equipo sincronizado con ese grupo LDAP.

Si no se desea divulgar dicha informaci??n, su empresa u organizaci??n debe restringir los permisos del *Usuario de b??squeda de dominio* en la consola de administraci??n. Si no es posible aplicar dicha restricci??n, comun??quese con el {% data variables.contact.contact_ent_support %}.

{% endwarning %}

### Clases de objetos del grupo LDAP admitidas

El {% data variables.product.prodname_ghe_server %} admite estas clases de objetos del grupo LDAP. Los grupos se pueden anidar.

- `grupo`
- `groupOfNames`
- `groupOfUniqueNames`
- `posixGroup`

## Ver y crear usuarios LDAP

Puedes ver la lista completa de usuarios LDAP que tienen acceso a tu instancia y aprovisionar nuevos usuarios.

{% data reusables.enterprise_site_admin_settings.sign-in %}
{% data reusables.enterprise_site_admin_settings.access-settings %}
3. En la barra lateral izquierda, haz clic en **LDAP users** (Usuarios LDAP). ![Pesta??a LDAP users (Usuarios LDAP)](/assets/images/enterprise/site-admin-settings/ldap-users-tab.png)
4. Para buscar un usuario, escribe un nombre de usuario completo o parcial y haz clic en **Search** (Buscar). Se mostrar??n los usuarios existentes en los resultados de b??squeda. Si un usuario no existe, haz clic en **Create** (Crear) para aprovisionar la nueva cuenta de usuario. ![B??squeda LDAP](/assets/images/enterprise/site-admin-settings/ldap-users-search.jpg)

## Actualizar cuentas LDAP

A menos que [la sincronizaci??n LDAP est?? activada](#enabling-ldap-sync), las modificaciones de las cuentas LDAP no se sincronizan autom??ticamente con el {% data variables.product.prodname_ghe_server %}.

* Para usar un nuevo grupo de administraci??n LDAP, los usuarios deben ser promovidos y degradados de forma manual en el {% data variables.product.prodname_ghe_server %} para reflejar las modificaciones en LDAP.
* Para agregar o eliminar cuentas LDAP de los grupos de administraci??n LDAP, [promueve o degrada las cuentas en el {% data variables.product.prodname_ghe_server %}](/enterprise/admin/guides/user-management/promoting-or-demoting-a-site-administrator).
* Para eliminar las cuentas LDAP, [suspende las cuentas del {% data variables.product.prodname_ghe_server %}](/enterprise/admin/guides/user-management/suspending-and-unsuspending-users).

### Sincronizar cuentas LDAP de forma manual

{% data reusables.enterprise_site_admin_settings.sign-in %}
{% data reusables.enterprise_site_admin_settings.access-settings %}
{% data reusables.enterprise_site_admin_settings.search-user %}
{% data reusables.enterprise_site_admin_settings.click-user %}
{% data reusables.enterprise_site_admin_settings.admin-top-tab %}
{% data reusables.enterprise_site_admin_settings.admin-tab %}
5. En "LDAP", haz clic en **Sync now** (Sincronizar ahora) para actualizar de forma manual la cuenta con los datos de tu servidor LDAP. ![Bot??n LDAP sync now (Sincronizar LDAP ahora)](/assets/images/enterprise/site-admin-settings/ldap-sync-now-button.png)

Tambi??n puedes [utilizar la API para activar una sincronizaci??n manual](/enterprise/user/rest/reference/enterprise-admin#ldap).

## Revocar acceso a {% data variables.product.product_location %}

Si [la sincronizaci??n LDAP est?? activada](#enabling-ldap-sync), al eliminar las credenciales LDAP de un usuario, se suspender?? su cuenta hasta la siguiente ejecuci??n de sincronizaci??n.

Si la sincronizaci??n LDAP **no** est?? activada, debes suspender de forma manual la cuenta del {% data variables.product.prodname_ghe_server %} despu??s de eliminar las credenciales LDAP. Para obtener m??s informaci??n, consulta "[Suspender y anular suspensi??n de usuarios](/enterprise/admin/guides/user-management/suspending-and-unsuspending-users)".
