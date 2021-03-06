---
ms.date: 07/16/2020
ms.topic: reference
title: Recurso Log de DSC
description: Recurso Log de DSC
ms.openlocfilehash: 281d1f8aeeb4d075f073419ac02a0f81888ed2b5
ms.sourcegitcommit: 196c7f8cd24560cac70c88acc89909f17a86aea9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2020
ms.locfileid: "93142456"
---
# <a name="dsc-log-resource"></a>Recurso Log de DSC

> Aplica-se a: Windows PowerShell 4.0, Windows PowerShell 5.x

O recurso **Log** na Configuração de Estado Desejado (DSC) do Windows PowerShell fornece um mecanismo para escrever mensagens no log de eventos Microsoft-Windows-Desired State Configuration/Analytic.

[!INCLUDE [Updated DSC Resources](../../../../../includes/dsc-resources.md)]

## <a name="syntax"></a>Sintaxe

```Syntax
Log [string] #ResourceName
{
    Message = [string]
    [ DependsOn = [string[]] ]
    [ PsDscRunAsCredential = [PSCredential] ]
}
```

> [!NOTE]
> Por padrão, somente os logs operacionais da DSC são habilitados. Antes que o log Analítico esteja disponível ou visível, ele deve ser habilitado. Para obter mais informações, veja [Onde estão os logs de eventos da DSC?](../../../troubleshooting/troubleshooting.md#where-are-dsc-event-logs).

## <a name="properties"></a>Propriedades

| Propriedade |                                                   DESCRIÇÃO                                                    |
| -------- | ---------------------------------------------------------------------------------------------------------------- |
| Mensagem  | Indica a mensagem que você deseja escreve no log de eventos Microsoft-Windows-Desired State Configuration/Analytic. |

## <a name="common-properties"></a>Propriedades comuns

|       Propriedade       |                                                                                                                                                          DESCRIÇÃO                                                                                                                                                           |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| DependsOn            | Indica que a configuração de outro recurso deve ser executada antes de ele ser configurado. Por exemplo, se a ID do bloco de script de configuração do recurso que você deseja executar primeiro for ResourceName e seu tipo for ResourceType, a sintaxe para usar essa propriedade será `DependsOn = "[ResourceType]ResourceName"`. |
| PsDscRunAsCredential | Define a credencial para executar todo o recurso.                                                                                                                                                                                                                                                                        |

> [!NOTE]
> A propriedade comum **PsDscRunAsCredential** foi adicionada ao WMF 5.0 para permitir a execução de qualquer recurso de DSC no contexto de outras credenciais. Para saber mais, confira [Usar credenciais com recursos de DSC](../../../configurations/runasuser.md).

## <a name="example"></a>Exemplo

O exemplo a seguir mostra como incluir uma mensagem no log de eventos Microsoft-Windows-Desired State Configuration/Analytic.

> [!NOTE]
> Se você executar [Test-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/test-dscconfiguration) com esse recurso configurado, ele sempre retornará **$false** .

```powershell
Configuration logResourceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node localhost
    {
        Log LogExample
        {
            Message = 'This message will appear in the Microsoft-Windows-Desired State Configuration/Analytic event log.'
        }
    }
}
```
