---
title: 'Inicio rápido: Configuración de las propiedades de una aplicación en el inquilino de Azure Active Directory (Azure AD)'
description: Este inicio rápido usa Azure Portal para configurar una aplicación que se ha registrado con su inquilino de Azure Active Directory (Azure AD).
services: active-directory
author: iantheninja
manager: CelesteDG
ms.service: active-directory
ms.subservice: app-mgmt
ms.topic: quickstart
ms.workload: identity
ms.date: 10/29/2019
ms.author: iangithinji
ms.openlocfilehash: 3b7a5d88aa40422dc46c6ca2c1681447cb030ea4
ms.sourcegitcommit: 2654d8d7490720a05e5304bc9a7c2b41eb4ae007
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/13/2021
ms.locfileid: "107379526"
---
# <a name="quickstart-configure-properties-for-an-application-in-your-azure-active-directory-azure-ad-tenant"></a>Inicio rápido: Configuración de las propiedades de una aplicación en el inquilino de Azure Active Directory (Azure AD)

En el inicio rápido anterior, agregó una aplicación a su inquilino de Azure Active Directory (Azure AD). Cuando se agrega una aplicación, se permite que el inquilino de Azure AD sepa que es el proveedor de identidades de la aplicación. Ahora configurará algunas de las propiedades de la aplicación.
 
## <a name="prerequisites"></a>Requisitos previos

Para configurar las propiedades de una aplicación en el inquilino de Azure AD, necesita:

- Una cuenta de Azure con una suscripción activa. [Cree una cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- Uno de los siguientes roles: Administrador global, Administrador de aplicaciones en la nube, Administrador de aplicaciones o Propietario de la entidad de servicio.
- Opcional: Haber finalizado el inicio rápido de [Visualización de las aplicaciones](view-applications-portal.md).
- Opcional: Haber finalizado el inicio rápido de [Incorporación de una aplicación](add-application-portal.md).

>[!IMPORTANT]
>Use un entorno que no sea de producción para probar los pasos de esta guía de inicio rápido.

## <a name="configure-app-properties"></a>Configuración de las propiedades de una aplicación

Cuando termine de agregar una aplicación al inquilino de Azure AD, aparecerá la página de información general. Si está configurando una aplicación que ya se había agregado, consulte el primer inicio rápido. Este le guía a través de la visualización de las aplicaciones agregadas a su inquilino. 

Para editar las propiedades de la aplicación:

1. En el portal de Azure AD, seleccione **Aplicaciones empresariales**. Después, busque y seleccione la aplicación que desea configurar.
2. En la sección **Administrar**, seleccione **Propiedades** para abrir el panel **Propiedades** para editarlo.
3. Dedique un momento a comprender las opciones disponibles. Estas dependerán del modo en que la aplicación se integre con Azure AD. Por ejemplo, una aplicación que use el inicio de sesión único basado en SAML tendrá campos como *URL de acceso de usuario*, mientras que una aplicación que use el inicio de sesión único basado en OIDC no. Tenga en cuenta también que las aplicaciones agregadas mediante **Azure Active Directory > Registros de aplicaciones** son, de forma predeterminada, aplicaciones basadas en OIDC. Sin embargo, las aplicaciones agregadas mediante **Azure Active Directory > Aplicaciones empresariales** pueden usar una serie de estándares de inicio de sesión único. Todas las aplicaciones tendrán campos para configurar el momento en que se muestra una aplicación y se puede usar. Estos campos son:
    - La opción **¿Habilitado para que los usuarios inicien sesión?** determina si los usuarios asignados a la aplicación pueden iniciar sesión.
    - La opción **¿Asignación de usuarios?** determina si los usuarios que no están asignados a la aplicación pueden iniciar sesión.
    - La opción **¿Es visible para los usuarios?** determina si los usuarios asignados a una aplicación pueden verla en [Mis aplicaciones](https://myapps.microsoft.com) y en el iniciador de aplicaciones de Microsoft 365. (Vea el menú de gofres en la esquina superior izquierda de un sitio web de Microsoft 365).
    
    > [!TIP]
    > La asignación de usuarios se produce en la sección **Usuarios y grupos** de la navegación.

    Las tres opciones se pueden alternar de forma independiente entre sí y el comportamiento resultante no siempre resulta obvio. La siguiente es una tabla que podría servir de ayuda:
    
    | ¿Está habilitado para que los usuarios inicien sesión? | ¿Se requiere la asignación de usuarios? | ¿Es visible para los usuarios? | Comportamiento de los usuarios que se han asignado o no a la aplicación. |
    |---|---|---|---|
    | Sí | Sí | Sí | Los usuarios asignados pueden ver la aplicación e iniciar sesión.<br>Los usuarios sin asignar no pueden ver la aplicación y no pueden iniciar sesión. |
    | Sí | Sí | No  | Los usuarios asignados no pueden ver la aplicación, pero pueden iniciar sesión.<br>Los usuarios sin asignar no pueden ver la aplicación y no pueden iniciar sesión. |
    | Sí | No  | Sí | Los usuarios asignados pueden ver la aplicación e iniciar sesión.<br>Los usuarios sin asignar no pueden ver la aplicación, pero pueden iniciar sesión. |
    | Sí | No  | No  | Los usuarios asignados no pueden ver la aplicación, pero pueden iniciar sesión.<br>Los usuarios sin asignar no pueden ver la aplicación, pero pueden iniciar sesión. |
    | No  | Sí | Sí | Los usuarios asignados no pueden ver la aplicación y no pueden iniciar sesión.<br>Los usuarios sin asignar no pueden ver la aplicación y no pueden iniciar sesión. |
    | No  | Sí | No  | Los usuarios asignados no pueden ver la aplicación y no pueden iniciar sesión.<br>Los usuarios sin asignar no pueden ver la aplicación y no pueden iniciar sesión. |
    | No  | No  | Sí | Los usuarios asignados no pueden ver la aplicación y no pueden iniciar sesión.<br>Los usuarios sin asignar no pueden ver la aplicación y no pueden iniciar sesión. |
    | No  | No  | No  | Los usuarios asignados no pueden ver la aplicación y no pueden iniciar sesión.<br>Los usuarios sin asignar no pueden ver la aplicación y no pueden iniciar sesión. |

4. Cuando haya terminado, seleccione **Guardar**.

## <a name="use-a-custom-logo"></a>Uso de un logotipo personalizado

Para usar un logotipo personalizado:

1. Cree un logotipo de 215 por 215 píxeles y guárdelo en formato .png.
2. En el portal de Azure AD, seleccione **Aplicaciones empresariales**. Después, busque y seleccione la aplicación que desea configurar.
3. En la sección **Administrar**, seleccione **Propiedades** para abrir el panel **Propiedades** para editarlo. 
4. Seleccione el icono para cargar el logotipo.
5. Cuando haya terminado, seleccione **Guardar**.

    ![Captura de la pantalla Propiedades que muestra cómo cambiar el logotipo.](media/add-application-portal/change-logo.png)

   > [!NOTE]
   > La miniatura que se muestra en este panel de **Propiedades** no se actualiza inmediatamente. Puede cerrar y volver a abrir el panel **Propiedades** para ver el icono actualizado.


> [!TIP]
> La administración de aplicaciones se puede automatizar mediante Graph API, consulte el artículo sobre la [automatización de la administración de aplicaciones con Microsoft Graph API](/graph/application-saml-sso-configure-api).

## <a name="add-notes"></a>Agregar notas

Puede usar el campo de notas para agregar información que sea relevante para la administración de la aplicación en Azure AD. Notas es un campo de texto libre con un tamaño máximo de 1024 caracteres.

1. En el portal de Azure AD, seleccione **Aplicaciones empresariales**. Después, busque y seleccione la aplicación que desea configurar.
2. En la sección **Administrar**, seleccione **Propiedades** para abrir el panel **Propiedades** para editarlo.
3. Actualice el campo Notas y seleccione **Guardar**.

    ![Captura de la pantalla Propiedades que muestra cómo cambiar las notas](media/add-application-portal/notes-application.png)

    
## <a name="clean-up-resources"></a>Limpieza de recursos

Si no va a continuar con la serie de inicios rápidos, considere la posibilidad de eliminar la aplicación para limpiar el inquilino de prueba. La eliminación de la aplicación se trata en el último inicio rápido de esta serie, consulte [Eliminación de una aplicación](delete-application-portal.md).

## <a name="next-steps"></a>Pasos siguientes

Avance al siguiente artículo para aprender a asignar usuarios a la aplicación.
> [!div class="nextstepaction"]
> [Asignación de usuarios a una aplicación](add-application-portal-assign-users.md)