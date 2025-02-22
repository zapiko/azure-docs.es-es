---
title: Incorporación a Azure Security Center con PowerShell
description: Este documento le guía por el proceso de habilitar Azure Security Center con cmdlets de PowerShell.
author: memildin
manager: rkarlin
ms.service: security-center
ms.topic: quickstart
ms.date: 04/19/2021
ms.author: memildin
ms.openlocfilehash: f9ab258f59279112d0b90c5d460e6761ac911a2d
ms.sourcegitcommit: 3ed0f0b1b66a741399dc59df2285546c66d1df38
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2021
ms.locfileid: "107713361"
---
# <a name="automate-onboarding-of-azure-security-center-using-powershell"></a>Automatización de la incorporación de Azure Security Center mediante PowerShell

Puede proteger las cargas de trabajo de Azure mediante programación, con el módulo de PowerShell de Azure Security Center.
El uso de PowerShell le permite automatizar las tareas y evitar los errores humanos inherentes a las tareas manuales. Esto es especialmente útil en implementaciones a gran escala en las que intervienen docenas de suscripciones con cientos de miles de recursos, todos los cuales deben protegerse desde el principio.

La incorporación de Azure Security Center mediante PowerShell permite automatizar mediante programación la incorporación y la administración de los recursos de Azure y agregar los controles de seguridad necesarios.

En este artículo se proporciona un script de PowerShell de ejemplo que se puede modificar y usar en su entorno para implementar el centro de seguridad en sus suscripciones. 

En este ejemplo, se habilitará Security Center en una suscripción con el identificador: d07c0080-170c-4c24-861d-9c817742786c y se aplicará la configuración recomendada que proporciona un alto nivel de protección habilitando Azure Defender, que ofrece funcionalidades avanzadas de detección y protección contra amenazas:

1. Habilite [Azure Defender](azure-defender.md). 
 
2. Establezca el área de trabajo de Log Analytics a la que el agente de Log Analytics enviará los datos que recopila de las máquinas virtuales asociadas con la suscripción; en este ejemplo, un área de trabajo definida por el usuario existente (myWorkspace).

3. Active el aprovisionamiento automático del agente de Security Center que [implementa el agente de Log Analytics](security-center-enable-data-collection.md#auto-provision-mma).

5. Establezca el [CISO de la organización como contacto de seguridad de las alertas y eventos destacados de Security Center](security-center-provide-security-contact-details.md).

6. Asigne [directivas de seguridad predeterminadas](tutorial-security-policy.md) de Security Center.

## <a name="prerequisites"></a>Requisitos previos

Estos pasos deben realizarse antes de ejecutar los cmdlets de Security Center:

1. Ejecute PowerShell como administrador.

1. Ejecute los siguientes comandos en PowerShell:
      
    ```Set-ExecutionPolicy -ExecutionPolicy AllSigned```

    ```Install-Module -Name Az.Security -Force```

## <a name="onboard-security-center-using-powershell"></a>Incorporación de Security Center mediante PowerShell

1. Registre sus suscripciones en el proveedor de recursos de Security Center:

    ```Set-AzContext -Subscription "d07c0080-170c-4c24-861d-9c817742786c"```

    ```Register-AzResourceProvider -ProviderNamespace 'Microsoft.Security'```

1. Opcional: Establezca el nivel de cobertura (Azure defender activado/desactivado) de las suscripciones. Si no está definido, Defender está desactivado:

    ```Set-AzContext -Subscription "d07c0080-170c-4c24-861d-9c817742786c"```

    ```Set-AzSecurityPricing -Name "default" -PricingTier "Standard"```

1. Configure el área de trabajo de Log Analytics a la que los agentes enviarán notificaciones. Debe tener un área de trabajo de Log Analytics ya creada a la que las máquinas virtuales de la suscripción enviarán notificaciones. Puede definir varias suscripciones para enviar notificaciones a la misma área de trabajo. Si no está definida, se usará el área de trabajo predeterminada.

    ```Set-AzSecurityWorkspaceSetting -Name "default" -Scope "/subscriptions/d07c0080-170c-4c24-861d-9c817742786c" -WorkspaceId"/subscriptions/d07c0080-170c-4c24-861d-9c817742786c/resourceGroups/myRg/providers/Microsoft.OperationalInsights/workspaces/myWorkspace"```

1. Instalación de aprovisionamiento automático del agente de Log Analytics en las máquinas virtuales de Azure:
    
    ```Set-AzContext -Subscription "d07c0080-170c-4c24-861d-9c817742786c"```
    
    ```Set-AzSecurityAutoProvisioningSetting -Name "default" -EnableAutoProvision```

    > [!NOTE]
    > Se recomienda habilitar el aprovisionamiento automático para asegurarse de que las máquinas virtuales de Azure estén protegidos automáticamente por Azure Security Center.
    >

1. Opcional: se recomienda encarecidamente [definir los detalles de contacto de seguridad](security-center-provide-security-contact-details.md) para las suscripciones que incorpore, que se usarán como destinatarios de las notificaciones y alertas generadas por Security Center:

    ```Set-AzSecurityContact -Name "default1" -Email "CISO@my-org.com" -AlertAdmin -NotifyOnAlert```

1. Asigne la iniciativa de directiva predeterminada de Security Center:

    ```Register-AzResourceProvider -ProviderNamespace 'Microsoft.PolicyInsights'```

    ```$Policy = Get-AzPolicySetDefinition | where {$_.Properties.displayName -EQ 'Azure Security Benchmark'} New-AzPolicyAssignment -Name 'ASC Default <d07c0080-170c-4c24-861d-9c817742786c>' -DisplayName 'Security Center Default <subscription ID>' -PolicySetDefinition $Policy -Scope '/subscriptions/d07c0080-170c-4c24-861d-9c817742786c'```

Se ha incorporado correctamente Azure Security Center con PowerShell.

Ya puede usar estos cmdlets de PowerShell con scripts de automatización para recorrer en iteración mediante programación suscripciones y recursos. Esto ahorra tiempo y reduce la probabilidad de error humano. Puede usar este [script de ejemplo](https://github.com/Microsoft/Azure-Security-Center/blob/master/quickstarts/ASC-Samples.ps1) como referencia.




## <a name="see-also"></a>Consulte también
Para más información sobre cómo puede usar PowerShell para automatizar la incorporación a Security Center, consulte el artículo siguiente:

* [Az.Security](/powershell/module/az.security)

Para más información sobre Security Center, consulte el siguiente artículo:

* [Establecimiento de directivas de seguridad en Azure Security Center](tutorial-security-policy.md): aprenda a configurar directivas de seguridad para las suscripciones y los grupos de recursos de Azure.
* [Administración y respuesta a las alertas de seguridad en Azure Security Center](security-center-managing-and-responding-alerts.md) : obtenga información sobre cómo administrar y responder a alertas de seguridad.