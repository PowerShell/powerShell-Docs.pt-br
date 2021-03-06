---
ms.date: 07/16/2020
ms.topic: reference
title: Recurso Package de DSC
description: Recurso Package de DSC
ms.openlocfilehash: 4bcc6dc68a37ebe434e30339452cd7269f984ae9
ms.sourcegitcommit: 196c7f8cd24560cac70c88acc89909f17a86aea9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2020
ms.locfileid: "93142864"
---
# <a name="dsc-package-resource"></a>Recurso Package de DSC

> Aplica-se a: Windows PowerShell 4.0, Windows PowerShell 5.x

O recurso **Package** na Configuração de Estado Desejado (DSC) do Windows PowerShell fornece um mecanismo para instalar ou desinstalar pacotes, tais como os pacotes do Windows Installer e setup.exe, em um nó de destino.

[!INCLUDE [Updated DSC Resources](../../../../../includes/dsc-resources.md)]

## <a name="syntax"></a>Sintaxe

```Syntax
Package [string] #ResourceName
{
    Name = [string]
    Path = [string]
    ProductId = [string]
    [ Arguments = [string] ]
    [ Credential = [PSCredential] ]
    [ LogPath = [string] ]
    [ ReturnCode = [UInt32[]] ]
    [ DependsOn = [string[]] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ PsDscRunAsCredential = [PSCredential] ]
}
```

## <a name="properties"></a>Propriedades

|Propriedade |DESCRIÇÃO |
|---|---|
|Nome |Indica o nome do pacote para o qual você deseja garantir um estado específico. |
|Caminho |Indica o caminho em que o pacote reside. |
|ProductId |Indica a ID do produto que identifica o pacote com exclusividade. |
|Argumentos |Lista uma cadeia de caracteres de argumentos que será passada para o pacote exatamente conforme fornecido. |
|Credencial |Fornece acesso ao pacote em uma fonte remota. Essa propriedade não é usada para instalar o pacote. O pacote é sempre instalado no sistema local. |
|LogPath |Indica o caminho completo em que você deseja que o provedor salve um arquivo de log para instalar ou desinstalar o pacote. |
|ReturnCode |Indica o código de retorno esperado. Se o código de retorno real não corresponder ao valor esperado fornecido aqui, a configuração gerará um erro. |

## <a name="common-properties"></a>Propriedades comuns

|Propriedade |DESCRIÇÃO |
|---|---|
|DependsOn |Indica que a configuração de outro recurso deve ser executada antes de ele ser configurado. Por exemplo, se a ID do bloco de script de configuração do recurso que você deseja executar primeiro for ResourceName e seu tipo for ResourceType, a sintaxe para usar essa propriedade será `DependsOn = "[ResourceType]ResourceName"`. |
|Ensure |Indica se o pacote foi instalado. Defina esta propriedade como **Absent** para garantir que o pacote não seja instalado (ou desinstalar o pacote, se ele estiver instalado). Defina-a como **Present** para garantir que o pacote seja instalado. O valor padrão é **Present** . |
|PsDscRunAsCredential |Define a credencial para executar todo o recurso. |

> [!NOTE]
> A propriedade comum **PsDscRunAsCredential** foi adicionada ao WMF 5.0 para permitir a execução de qualquer recurso de DSC no contexto de outras credenciais. Para saber mais, confira [Usar credenciais com recursos de DSC](../../../configurations/runasuser.md).

## <a name="example"></a>Exemplo

Este exemplo executa o instalador .msi que está localizado no caminho especificado e tem a ID do produto especificado.

```powershell
Configuration PackageTest
{
    Package PackageExample
    {
        Ensure      = "Present"  # You can also set Ensure to "Absent"
        Path        = "$Env:SystemDrive\TestFolder\TestProject.msi"
        Name        = "TestPackage"
        ProductId   = "ACDDCDAF-80C6-41E6-A1B9-8ABD8A05027E"
    }
}
```
