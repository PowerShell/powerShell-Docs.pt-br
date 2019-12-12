---
title: Criando controles personalizados | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c3baa406-cd33-4420-be5a-07ef09d93480
caps.latest.revision: 8
ms.openlocfilehash: 3504ab1d974c55e9279172d0e851961474ccb926
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "72363375"
---
# <a name="creating-custom-controls"></a><span data-ttu-id="8bd4c-102">Criar controles personalizados</span><span class="sxs-lookup"><span data-stu-id="8bd4c-102">Creating Custom Controls</span></span>

<span data-ttu-id="8bd4c-103">Os controles personalizados são os componentes mais flexíveis de um arquivo de formatação.</span><span class="sxs-lookup"><span data-stu-id="8bd4c-103">Custom controls are the most flexible components of a formatting file.</span></span> <span data-ttu-id="8bd4c-104">Ao contrário das exibições de tabela, lista e amplas que definem uma estrutura formal de dados, como uma tabela de dados, os controles personalizados permitem que você defina como uma parte de dados individual é exibida.</span><span class="sxs-lookup"><span data-stu-id="8bd4c-104">Unlike table, list, and wide views that define a formal structure of data, such as a table of data, custom controls allow you to define how an individual piece of data is displayed.</span></span> <span data-ttu-id="8bd4c-105">Você pode definir um conjunto comum de controles personalizados que estão disponíveis para todas as exibições do arquivo de formatação, pode definir controles personalizados que estão disponíveis para uma exibição específica ou pode definir um conjunto de controles que estão disponíveis para um grupo de objetos.</span><span class="sxs-lookup"><span data-stu-id="8bd4c-105">You can define a common set of custom controls that are available to all the views of the formatting file, you can define custom controls that are available to a specific view, or you can define a set of controls that are available to a group of objects.</span></span>

## <a name="custom-control-example"></a><span data-ttu-id="8bd4c-106">Exemplo de controle personalizado</span><span class="sxs-lookup"><span data-stu-id="8bd4c-106">Custom Control Example</span></span>

<span data-ttu-id="8bd4c-107">O exemplo a seguir mostra um controle personalizado que é definido no arquivo Certificates. Format. ps1xml.</span><span class="sxs-lookup"><span data-stu-id="8bd4c-107">The following example shows a custom control that is defined in the Certificates.Format.ps1xml file.</span></span> <span data-ttu-id="8bd4c-108">Esse controle personalizado é usado para separar os objetos [System. Management. Automation. Signature](/dotnet/api/System.Management.Automation.Signature) exibidos em uma exibição de tabela.</span><span class="sxs-lookup"><span data-stu-id="8bd4c-108">This custom control is used to separate the [System.Management.Automation.Signature](/dotnet/api/System.Management.Automation.Signature) objects displayed in a table view.</span></span>

```xml
<Controls>
  <Control>
    <Name>SignatureTypes-GroupingFormat</Name>
    <CustomControl>
      <CustomEntries>
        <CustomEntry>
          <CustomItem>
            <Frame>
              <LeftIndent>4</LeftIndent>
              <CustomItem>
                <Text AssemblyName="System.Management.Automation" BaseName="FileSystemProviderStrings"
                  ResourceId="DirectoryDisplayGrouping"/>
                <ExpressionBinding>
                  <ScriptBlock>split-path $_.Path</ScriptBlock>
                </ExpressionBinding>
                <NewLine/>
              </CustomItem>
            </Frame>
          </CustomItem>
        </CustomEntry>
      </CustomEntries>
    </CustomControl>
  </Control>
</Controls>

```

## <a name="see-also"></a><span data-ttu-id="8bd4c-109">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="8bd4c-109">See Also</span></span>

[<span data-ttu-id="8bd4c-110">Gravando um arquivo de formatação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bd4c-110">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
