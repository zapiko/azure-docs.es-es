---
title: Recomendaciones basadas en agente
description: Sepa en qué consiste el concepto de recomendaciones de seguridad y cómo se usan en dispositivos de Defender para IoT.
ms.topic: conceptual
ms.date: 02/16/2021
ms.openlocfilehash: a29957f459edad8b768daea7bc4567d77c80b165
ms.sourcegitcommit: 32e0fedb80b5a5ed0d2336cea18c3ec3b5015ca1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2021
ms.locfileid: "104784992"
---
# <a name="security-recommendations-for-iot-devices"></a>Recomendaciones de seguridad para dispositivos IoT

Defender para IoT analiza los dispositivos IoT y los recursos de Azure y hace recomendaciones de seguridad para reducir la superficie expuesta a ataques.
Las recomendaciones de seguridad requieren una acción y su objetivo es ayudar a los clientes a cumplir los procedimientos recomendados de seguridad.

En este artículo, encontrará una lista de recomendaciones que se pueden activar en los dispositivos IoT.

## <a name="agent-based-recommendations"></a>Recomendaciones basadas en agente

Las recomendaciones de dispositivo proporcionan información y sugerencias para mejorar la posición de seguridad de los dispositivos.

| severity | Nombre | Origen de datos | Descripción |
|--|--|--|--|
| Media | Puertos abiertos en el dispositivo | Defender-IoT-micro-agent Classic| Se encontró un punto de conexión de escucha en el dispositivo. |
| Media | Se encontró una directiva de firewall permisiva en una de las cadenas. | Defender-IoT-micro-agent Classic| Se encontró una directiva de firewall permitida en las cadenas de firewall principales (ENTRADA/SALIDA). La directiva debe denegar todo el tráfico de manera predeterminada y definir reglas para permitir la comunicación necesaria hacia y desde el dispositivo. |
| Media | Se encontró una regla de firewall permisiva en la cadena de entrada | Defender-IoT-micro-agent Classic| Se encontró una regla en el firewall que contiene un patrón permisivo para una amplia gama de direcciones IP o puertos. |
| Media | Se encontró una regla de firewall permisiva en la cadena de salida | Defender-IoT-micro-agent Classic| Se encontró una regla en el firewall que contiene un patrón permisivo para una amplia gama de direcciones IP o puertos. |
| Media | Error de validación de línea base de sistema operativo | Defender-IoT-micro-agent Classic| El dispositivo no cumple las [pruebas comparativas de CIS Linux](https://www.cisecurity.org/cis-benchmarks/). |

### <a name="agent-based-operational-recommendations"></a>Recomendaciones operativas basadas en agente

Las recomendaciones operativas proporcionan información y sugerencias para mejorar la configuración de los agentes de seguridad.

| severity | Nombre | Origen de datos | Descripción |
|--|--|--|--|
| Bajo | El agente envía mensajes sin utilizar | Defender-IoT-micro-agent Classic | 10 % o más de los mensajes de seguridad tenían un tamaño inferior a 4 KB durante las últimas 24 horas. |
| Bajo | Configuración de gemelo de seguridad no óptima | Defender-IoT-micro-agent Classic | La configuración del gemelo de seguridad no es óptima. |
| Bajo | Conflicto de configuración de gemelo de seguridad | Defender-IoT-micro-agent Classic | Se identificaron conflictos en la configuración del gemelo de seguridad. |

## <a name="next-steps"></a>Pasos siguientes

- [Información general](overview.md) del servicio Defender para IoT
- Aprenda a [acceder a los datos de seguridad](how-to-security-data-access.md)
- Más información sobre cómo [investigar un dispositivo](how-to-investigate-device.md)
