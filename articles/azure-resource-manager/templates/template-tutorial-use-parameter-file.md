---
title: 'Tutorial: Uso de un archivo de parámetros para implementar la plantilla'
description: Use archivos de parámetros que contengan los valores que se usarán para implementar la plantilla de Azure Resource Manager.
author: mumian
ms.date: 09/10/2020
ms.topic: tutorial
ms.author: jgao
ms.openlocfilehash: 81ce0d00079c65ae76a31ec474b5bc632746db2d
ms.sourcegitcommit: 2e123f00b9bbfebe1a3f6e42196f328b50233fc5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2021
ms.locfileid: "108074234"
---
# <a name="tutorial-use-parameter-files-to-deploy-your-arm-template"></a>Tutorial: Uso de archivos de parámetros para implementar la plantilla de Resource Manager

En este tutorial, aprenderá a usar [archivos de parámetros](parameter-files.md) para almacenar los valores que se pasan durante la implementación. En los tutoriales anteriores, usó parámetros insertados con el comando de implementación. Este enfoque funcionó para probar la plantilla de Azure Resource Manager (plantilla de ARM), pero al automatizar las implementaciones puede ser más fácil pasar un conjunto de valores del entorno. Los archivos de parámetros facilitan el empaquetado de los valores de los parámetros de un entorno específico. En este tutorial, creará archivos de parámetros para entornos de desarrollo y producción. Su tiempo de realización es de unos **12 minutos**.

## <a name="prerequisites"></a>Prerrequisitos

Aunque no es obligatorio, se recomienda realizar el [tutorial sobre etiquetas](template-tutorial-add-tags.md).

Debe tener Visual Studio Code con la extensión Herramientas de Resource Manager y Azure PowerShell o la CLI de Azure. Para más información, consulte las [herramientas de plantilla](template-tutorial-create-first-template.md#get-tools).

## <a name="review-template"></a>Revisión de la plantilla

La plantilla tiene muchos parámetros que puede proporcionar durante la implementación. Al final del tutorial anterior, la plantilla tenía el siguiente aspecto:

:::code language="json" source="~/resourcemanager-templates/get-started-with-templates/add-tags/azuredeploy.json":::

Esta plantilla funciona bien, pero ahora desea administrar fácilmente los parámetros que pasa a la plantilla.

## <a name="add-parameter-files"></a>Adición de archivos de parámetros

Los archivos de parámetros son archivos JSON con una estructura similar a la plantilla. En el archivo, proporcione los valores de los parámetros que desea pasar durante la implementación.

Proporcione valores para los parámetros de la plantilla en el archivo de parámetros. El nombre de cada parámetro del archivo de parámetros debe coincidir con el nombre de un parámetro de la plantilla. El nombre no distingue entre mayúsculas y minúsculas, pero para ver fácilmente los valores coincidentes se recomienda que coincida con el uso de mayúsculas y minúsculas de la plantilla.

No es necesario proporcionar un valor para cada parámetro. Si un parámetro no especificado tiene un valor predeterminado, se usa ese valor durante la implementación. Si un parámetro no tiene un valor predeterminado y no se especifica en el archivo de parámetros, se le pedirá que proporcione un valor durante la implementación.

No se puede especificar un nombre de parámetro en el archivo de parámetros que no coincida con un nombre de parámetro en la plantilla. Recibirá un error cuando se proporcionan parámetros desconocidos.

En Visual Studio Code, cree un archivo con el siguiente contenido. Guarde el archivo con el nombre _azuredeploy.parameters.dev.json_.

:::code language="json" source="~/resourcemanager-templates/get-started-with-templates/add-tags/azuredeploy.parameters.dev.json":::

Este archivo es el archivo de parámetros para el entorno de desarrollo. Observe que usa **Standard_LRS** para la cuenta de almacenamiento, asigna un nombre a los recursos con el prefijo **dev** y establece la etiqueta `Environment` en **Dev**.

De nuevo, cree un nuevo archivo con el siguiente contenido. Guarde el archivo con el nombre _azuredeploy.parameters.prod.json_.

:::code language="json" source="~/resourcemanager-templates/get-started-with-templates/add-tags/azuredeploy.parameters.prod.json":::

Este archivo es el archivo de parámetros para el entorno de producción. Observe que usa **Standard_GRS** para la cuenta de almacenamiento, asigna un nombre a los recursos con el prefijo **contoso** y establece la etiqueta `Environment` en **Production**. En un entorno de producción real, también deseará usar una instancia de App Service con una SKU que no sea gratuita, pero seguiremos con esa SKU para este tutorial.

## <a name="deploy-template"></a>Implementar plantilla

Use la CLI de Azure o Azure PowerShell para implementar la plantilla.

Como prueba final de la plantilla, vamos a crear dos nuevos grupos de recursos. Uno para el entorno de desarrollo y otro para el entorno de producción.

En el caso de las variables de plantilla y parámetro, reemplace `{path-to-the-template-file}`, `{path-to-azuredeploy.parameters.dev.json}`, `{path-to-azuredeploy.parameters.prod.json}` y las llaves `{}` por las rutas de acceso al archivo de plantilla y parámetro.

En primer lugar, se implementará en el entorno de desarrollo.

# <a name="powershell"></a>[PowerShell](#tab/azure-powershell)

```azurepowershell
$templateFile = "{path-to-the-template-file}"
$parameterFile="{path-to-azuredeploy.parameters.dev.json}"
New-AzResourceGroup `
  -Name myResourceGroupDev `
  -Location "East US"
New-AzResourceGroupDeployment `
  -Name devenvironment `
  -ResourceGroupName myResourceGroupDev `
  -TemplateFile $templateFile `
  -TemplateParameterFile $parameterFile
```

# <a name="azure-cli"></a>[CLI de Azure](#tab/azure-cli)

Para ejecutar este comando de implementación, debe tener la [última versión](/cli/azure/install-azure-cli) de la CLI de Azure.

```azurecli
templateFile="{path-to-the-template-file}"
devParameterFile="{path-to-azuredeploy.parameters.dev.json}"
az group create \
  --name myResourceGroupDev \
  --location "East US"
az deployment group create \
  --name devenvironment \
  --resource-group myResourceGroupDev \
  --template-file $templateFile \
  --parameters $devParameterFile
```

---

Ahora, se implementará en el entorno de producción.

# <a name="powershell"></a>[PowerShell](#tab/azure-powershell)

```azurepowershell
$parameterFile="{path-to-azuredeploy.parameters.prod.json}"
New-AzResourceGroup `
  -Name myResourceGroupProd `
  -Location "West US"
New-AzResourceGroupDeployment `
  -Name prodenvironment `
  -ResourceGroupName myResourceGroupProd `
  -TemplateFile $templateFile `
  -TemplateParameterFile $parameterFile
```

# <a name="azure-cli"></a>[CLI de Azure](#tab/azure-cli)

```azurecli
prodParameterFile="{path-to-azuredeploy.parameters.prod.json}"
az group create \
  --name myResourceGroupProd \
  --location "West US"
az deployment group create \
  --name prodenvironment \
  --resource-group myResourceGroupProd \
  --template-file $templateFile \
  --parameters $prodParameterFile
```

---

> [!NOTE]
> Si se produjo un error en la implementación, use el modificador `verbose` para obtener información sobre los recursos que se están creando. Utilice el modificador `debug` para más información sobre la depuración.

## <a name="verify-deployment"></a>Comprobación de la implementación

Para comprobar la implementación, explore el grupo de recursos desde Azure Portal.

1. Inicie sesión en [Azure Portal](https://portal.azure.com).
1. En el menú izquierdo, seleccione **Grupos de recursos**.
1. Verá los dos nuevos grupos de recursos que implementó en este tutorial.
1. Seleccione cualquier grupo de recursos y consulte los recursos implementados. Observe que coinciden con los valores especificados en el archivo de parámetros para ese entorno.

## <a name="clean-up-resources"></a>Limpieza de recursos

1. En Azure Portal, seleccione **Grupos de recursos** en el menú de la izquierda.
2. Escriba el nombre del grupo de recursos en el campo **Filtrar por nombre**. Si ha completado esta serie, tiene tres grupos de recursos que eliminar: **myResourceGroup**, **myResourceGroupDev** y **myResourceGroupProd**.
3. Seleccione el nombre del grupo de recursos.
4. Seleccione **Eliminar grupo de recursos** del menú superior.

## <a name="next-steps"></a>Pasos siguientes

Enhorabuena, ha terminado esta introducción a la implementación de plantillas en Azure. Si tiene comentarios y sugerencias, háganoslo saber en la sección de comentarios. Gracias.

En la siguiente serie de tutoriales encontrará más información sobre la implementación de plantillas.

> [!div class="nextstepaction"]
> [Implementación de una plantilla local](./deployment-tutorial-local-template.md)
