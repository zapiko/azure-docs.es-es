---
title: 'Tutorial: Integración de Azure Active Directory con Abstract | Microsoft Docs'
description: Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Abstract.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 07/16/2019
ms.author: jeedes
ms.openlocfilehash: e1c3236c4c1957b4d0daee8d30c71f03fb8674dd
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/19/2021
ms.locfileid: "97587832"
---
# <a name="tutorial-integrate-abstract-with-azure-active-directory"></a>Tutorial: Integración de Abstract con Azure Active Directory

En este tutorial aprenderá a integrar Abstract con Azure Active Directory (Azure AD). Al integrar Abstract con Azure AD, puede hacer lo siguiente:

* Controlar en Azure AD quién tiene acceso a Abstract.
* Permitir que los usuarios inicien sesión automáticamente en Abstract con sus cuentas de Azure AD.
* Administrar las cuentas desde una ubicación central (Azure Portal).

Para más información sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

## <a name="prerequisites"></a>Prerrequisitos

Para empezar, necesita los siguientes elementos:

* Una suscripción de Azure AD. Si no tiene una suscripción, puede crear una [cuenta gratuita](https://azure.microsoft.com/free/).
* Una suscripción habilitada para el inicio de sesión único (SSO) en Abstract.

## <a name="scenario-description"></a>Descripción del escenario

En este tutorial, va a configurar y probar el inicio de sesión único de Azure AD en un entorno de prueba.

* Abstract admite el inicio de sesión único iniciado por **SP e IDP**.

## <a name="adding-abstract-from-the-gallery"></a>Incorporación de Abstract desde la galería

Para configurar la integración de Abstract en Azure AD, será preciso agregar Abstract desde la galería a la lista de aplicaciones SaaS administradas.

1. Inicie sesión en [Azure Portal](https://portal.azure.com) con una cuenta personal, profesional o educativa de Microsoft.
1. En el panel de navegación de la izquierda, seleccione el servicio **Azure Active Directory**.
1. Vaya a **Aplicaciones empresariales** y seleccione **Todas las aplicaciones**.
1. Para agregar una nueva aplicación, seleccione **Nueva aplicación**.
1. En la sección **Agregar desde la galería**, escriba **Abstract** en el cuadro de búsqueda.
1. Seleccione **Abstract** en el panel de resultados y agregue la aplicación. Espere unos segundos mientras la aplicación se agrega al inquilino.


## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD

Configure y pruebe el inicio de sesión único de Azure AD con Abstract mediante un usuario de prueba llamado **B. Simon**. Para que el inicio de sesión único funcione, es necesario establecer una relación de vinculación entre un usuario de Azure AD y el usuario relacionado de Abstract.

Para configurar y probar el inicio de sesión único de Azure AD con Abstract, es preciso completar los siguientes bloques de creación:

1. **[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-sso)** , para permitir que los usuarios puedan utilizar esta característica.
2. **[Configuración del inicio de sesión único en Abstract](#configure-abstract-sso)**, para configurar los valores de Inicio de sesión único en la aplicación.
3. **[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)** , para probar el inicio de sesión único de Azure AD con Britta Simon.
4. **[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)** , para permitir que Britta Simon use el inicio de sesión único de Azure AD.
5. **[Creación de un usuario de prueba de Abstract](#create-abstract-test-user)**, para tener un homólogo de Britta Simon en Abstract que esté vinculado a su representación en Azure AD.
6. **[Prueba del inicio de sesión único](#test-sso)** : para comprobar si la configuración funciona.

### <a name="configure-azure-ad-sso"></a>Configuración del inicio de sesión único de Azure AD

Siga estos pasos para habilitar el inicio de sesión único de Azure AD en Azure Portal.

1. En [Azure Portal](https://portal.azure.com/), en la página de integración de la aplicación **Abstract**, busque la sección **Administrar** y seleccione **Inicio de sesión único**.
1. En la página **Seleccione un método de inicio de sesión único**, seleccione **SAML**.
1. En la página **Configurar el inicio de sesión único con SAML**, haga clic en el icono de edición o con forma de lápiz para abrir el cuadro de diálogo **Configuración básica de SAML** y modificar la configuración.

   ![Edición de la configuración básica de SAML](common/edit-urls.png)

1. En la sección **Configuración básica de SAML**, la aplicación está preconfigurada en el modo iniciado por **IDP** y las direcciones URL necesarias ya se han rellenado previamente con Azure. El usuario debe guardar la configuración, para lo que debe hacer clic en el botón **Guardar**.

1. Haga clic en **Establecer direcciones URL adicionales** y siga este paso si desea configurar la aplicación en el modo iniciado por **SP**:

    En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL: `https://app.abstract.com/signin`

4. En la página **Configurar el inicio de sesión único con SAML**, en la sección **Certificado de firma de SAML**, haga clic en el botón de copia para copiar **Dirección URL de metadatos de federación de aplicación** y guárdela en su equipo.

    ![Vínculo de descarga del certificado](common/copy-metadataurl.png)

### <a name="configure-abstract-sso"></a>Configuración del inicio de sesión único en Abstract

Asegúrese de recuperar los valores de `App Federation Metadata Url` y `Azure AD Identifier` de Azure Portal, ya que los necesitará para configurar el inicio de sesión único en Abstract.

Encontrará esta información en la página **Configuración del inicio de sesión único con SAML**:

* El valor de `App Federation Metadata Url` se encuentra en la sección **Certificado de firma de SAML**.
* El valor de `Azure AD Identifier` se encuentra en la sección **Configurar Abstract**.


Ahora está listo para configurar el inicio de sesión único en Abstract:

>[!Note]
>Tendrá que autenticarse con una cuenta de administrador de organización para tener acceso a la configuración de inicio de sesión único en Abstract.

1. Abra la [aplicación web Abstract](https://app.abstract.com/).
2. Vaya a la página **Permissions** (Permisos) en la barra lateral izquierda.
3. En la sección **Configure SSO** (Configurar inicio de sesión único), escriba los valores de **Metadata URL** (Dirección URL de metadatos) y de **Entity ID** (Identificador de entidad).
4. Escriba las excepciones manuales que pueda haber. Los correos electrónicos que aparezcan en la sección de excepciones manuales omitirán el inicio de sesión único y podrán iniciar sesión con el correo electrónico y la contraseña. 
5. Haga clic en **Guardar cambios**.

>[!Note] 
>En la lista de excepciones manuales deberá usar direcciones de correo electrónico principales. Si incluye en la lista el correo electrónico secundario de un usuario, se producirá un error en la activación del inicio de sesión único. En este caso, verá un mensaje de error con el correo electrónico principal de la cuenta que ha fallado. Agregue ese correo electrónico principal a la lista de excepciones manuales después de confirmar que conoce al usuario.

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD

En esta sección, va a crear un usuario de prueba llamado B.Simon en Azure Portal.

1. En el panel izquierdo de Azure Portal, seleccione **Azure Active Directory**, **Usuarios** y **Todos los usuarios**.
1. Seleccione **Nuevo usuario** en la parte superior de la pantalla.
1. En las propiedades del **usuario**, siga estos pasos:
   1. En el campo **Nombre**, escriba `B.Simon`.  
   1. En el campo **Nombre de usuario**, escriba username@companydomain.extension. Por ejemplo, `B.Simon@contoso.com`.
   1. Active la casilla **Show password** (Mostrar contraseña) y, después, anote el valor que se muestra en el cuadro **Contraseña**.
   1. Haga clic en **Crear**.

### <a name="assign-the-azure-ad-test-user"></a>Asignación del usuario de prueba de Azure AD

En esta sección, va a permitir que B. Simon acceda a Abstract utilizando el inicio de sesión único de Azure.

1. En Azure Portal, seleccione sucesivamente **Aplicaciones empresariales** y **Todas las aplicaciones**.
1. En la lista de aplicaciones, seleccione **Abstract**.
1. En la página de información general de la aplicación, busque la sección **Administrar** y seleccione **Usuarios y grupos**.

    ![Vínculo "Usuarios y grupos"](common/users-groups-blade.png)

1. Seleccione **Agregar usuario**. A continuación, en el cuadro de diálogo **Agregar asignación**, seleccione **Usuarios y grupos**.

    ![Vínculo de Agregar usuario](common/add-assign-user.png)

1. En el cuadro de diálogo **Usuarios y grupos**, seleccione **B.Simon** de la lista de usuarios y haga clic en el botón **Seleccionar** de la parte inferior de la pantalla.
1. Si espera que haya un valor de rol en la aserción de SAML, en el cuadro de diálogo **Seleccionar rol**, seleccione en la lista el rol adecuado para el usuario y haga clic en el botón **Seleccionar** en la parte inferior de la pantalla.
1. En el cuadro de diálogo **Agregar asignación**, haga clic en el botón **Asignar**.

### <a name="create-abstract-test-user"></a>Creación de un usuario de prueba de Abstract

Para probar el inicio de sesión único en Abstract:

1. Abra la [aplicación web Abstract](https://app.abstract.com/).
2. Vaya a la página **Permissions** (Permisos) en la barra lateral izquierda.
3. Haga clic en **Test with my Account** (Probar con mi cuenta). Si se produce un error en la prueba, [póngase en contacto con nuestro equipo de soporte técnico](https://help.abstract.com/hc/).

>[!Note]
>Tendrá que autenticarse con una cuenta de administrador de organización para tener acceso a la configuración de inicio de sesión único en Abstract.
Esta cuenta de administrador de organización deberá estar asignada a Abstract en Azure Portal.

### <a name="test-sso"></a>Prueba de SSO 

En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.

Al hacer clic en el icono de Abstract en el Panel de acceso, debería iniciar sesión automáticamente en la instancia de Abstract para la que configuró el inicio de sesión único. Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](../user-help/my-apps-portal-end-user-access.md).

## <a name="additional-resources"></a>Recursos adicionales

- [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](./tutorial-list.md)

- [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

- [¿Qué es el acceso condicional en Azure Active Directory?](../conditional-access/overview.md)