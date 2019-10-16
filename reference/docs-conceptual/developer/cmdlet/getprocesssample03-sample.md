---
title: Exemplo de GetProcessSample03 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fc9d80ee-6ebd-48cd-a7ea-53cb2b442a22
caps.latest.revision: 6
ms.openlocfilehash: ec5a8c284dd3fa772261099281aba1fb68c49118
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72369705"
---
# <a name="getprocesssample03-sample"></a><span data-ttu-id="71bce-102">Amostra GetProcessSample03</span><span class="sxs-lookup"><span data-stu-id="71bce-102">GetProcessSample03 Sample</span></span>

<span data-ttu-id="71bce-103">Este exemplo mostra como implementar um cmdlet que recupera os processos no computador local.</span><span class="sxs-lookup"><span data-stu-id="71bce-103">This sample shows how to implement a cmdlet that retrieves the processes on the local computer.</span></span> <span data-ttu-id="71bce-104">Ele fornece um parâmetro `Name` que pode aceitar um objeto do pipeline ou um valor de uma propriedade de um objeto cujo nome da propriedade é igual ao nome do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="71bce-104">It provides a `Name` parameter that can accept an object from the pipeline or a value from a property of an object whose property name is the same as the parameter name.</span></span> <span data-ttu-id="71bce-105">Este cmdlet é uma versão simplificada do cmdlet `Get-Process` fornecido pelo Windows PowerShell 2,0.</span><span class="sxs-lookup"><span data-stu-id="71bce-105">This cmdlet is a simplified version of the `Get-Process` cmdlet provided by Windows PowerShell 2.0.</span></span>

## <a name="how-to-build-the-sample-using-visual-studio"></a><span data-ttu-id="71bce-106">Como criar o exemplo usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71bce-106">How to build the sample using Visual Studio.</span></span>

1. <span data-ttu-id="71bce-107">Com o SDK do Windows PowerShell 2,0 instalado, navegue até a pasta GetProcessSample03.</span><span class="sxs-lookup"><span data-stu-id="71bce-107">With the Windows PowerShell 2.0 SDK installed, navigate to the GetProcessSample03 folder.</span></span> <span data-ttu-id="71bce-108">O local padrão é C:\Program Files (x86) \Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\csharp\GetProcessSample03.</span><span class="sxs-lookup"><span data-stu-id="71bce-108">The default location is C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\csharp\GetProcessSample03.</span></span>

2. <span data-ttu-id="71bce-109">Clique duas vezes no ícone do arquivo da solução (. sln).</span><span class="sxs-lookup"><span data-stu-id="71bce-109">Double-click the icon for the solution (.sln) file.</span></span> <span data-ttu-id="71bce-110">Isso abre o projeto de exemplo no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71bce-110">This opens the sample project in Visual Studio.</span></span>

3. <span data-ttu-id="71bce-111">No menu **Compilar** , selecione **Compilar solução**.</span><span class="sxs-lookup"><span data-stu-id="71bce-111">In the **Build** menu, select **Build Solution**.</span></span>

    <span data-ttu-id="71bce-112">A biblioteca do exemplo será criada nas pastas \bin ou \bin\Debug padrão.</span><span class="sxs-lookup"><span data-stu-id="71bce-112">The library for the sample will be built in the default \bin or \bin\debug folders.</span></span>

### <a name="how-to-run-the-sample"></a><span data-ttu-id="71bce-113">Como executar o exemplo</span><span class="sxs-lookup"><span data-stu-id="71bce-113">How to run the sample</span></span>

1. <span data-ttu-id="71bce-114">Crie a seguinte pasta de módulo:</span><span class="sxs-lookup"><span data-stu-id="71bce-114">Create the following module folder:</span></span>

    `[user]/documents/windowspowershell/modules/GetProcessSample03`

2. <span data-ttu-id="71bce-115">Copie o assembly de exemplo para a pasta do módulo.</span><span class="sxs-lookup"><span data-stu-id="71bce-115">Copy the sample assembly to the module folder.</span></span>

3. <span data-ttu-id="71bce-116">Inicie o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="71bce-116">Start Windows PowerShell.</span></span>

4. <span data-ttu-id="71bce-117">Execute o seguinte comando para carregar o assembly no Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="71bce-117">Run the following command to load the assembly into Windows PowerShell:</span></span>

    `Import-module getprossessample03`

5. <span data-ttu-id="71bce-118">Execute o seguinte comando para executar o cmdlet:</span><span class="sxs-lookup"><span data-stu-id="71bce-118">Run the following command to run the cmdlet:</span></span>

    `get-proc`

## <a name="requirements"></a><span data-ttu-id="71bce-119">Requisitos</span><span class="sxs-lookup"><span data-stu-id="71bce-119">Requirements</span></span>

<span data-ttu-id="71bce-120">Este exemplo requer o Windows PowerShell 2,0.</span><span class="sxs-lookup"><span data-stu-id="71bce-120">This sample requires Windows PowerShell 2.0.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="71bce-121">Demonstrar</span><span class="sxs-lookup"><span data-stu-id="71bce-121">Demonstrates</span></span>

<span data-ttu-id="71bce-122">Este exemplo demonstra o seguinte.</span><span class="sxs-lookup"><span data-stu-id="71bce-122">This sample demonstrates the following.</span></span>

- <span data-ttu-id="71bce-123">Declarando uma classe de cmdlet usando o atributo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="71bce-123">Declaring a cmdlet class using the Cmdlet attribute.</span></span>

- <span data-ttu-id="71bce-124">Declarando um parâmetro de cmdlet usando o atributo Parameter.</span><span class="sxs-lookup"><span data-stu-id="71bce-124">Declaring a cmdlet parameter using the Parameter attribute.</span></span>

- <span data-ttu-id="71bce-125">Especificando a posição do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="71bce-125">Specifying the position of the parameter.</span></span>

- <span data-ttu-id="71bce-126">Especificando que o parâmetro recebe entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="71bce-126">Specifying that the parameter takes input from the pipeline.</span></span> <span data-ttu-id="71bce-127">A entrada pode ser Obtida de um objeto ou de um valor de uma propriedade de um objeto cujo nome de propriedade é igual ao nome do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="71bce-127">The input can be taken from an object or a value from a property of an object whose property name is the same as the parameter name.</span></span>

- <span data-ttu-id="71bce-128">Declarando um atributo de validação para a entrada de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="71bce-128">Declaring a validation attribute for the parameter input.</span></span>

## <a name="example"></a><span data-ttu-id="71bce-129">Exemplo</span><span class="sxs-lookup"><span data-stu-id="71bce-129">Example</span></span>

<span data-ttu-id="71bce-130">Este exemplo mostra uma implementação do cmdlet Get-proc que inclui um parâmetro `Name` que aceita entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="71bce-130">This sample shows an implementation of the Get-Proc cmdlet that includes a `Name` parameter that accepts input from the pipeline.</span></span>

```csharp
namespace Microsoft.Samples.PowerShell.Commands
{
  using System;
  using System.Diagnostics;
  using System.Management.Automation;           // Windows PowerShell namespace
  #region GetProcCommand

  /// <summary>
  /// This class implements the get-proc cmdlet.
  /// </summary>
  [Cmdlet(VerbsCommon.Get, "Proc")]
  public class GetProcCommand : Cmdlet
  {
    #region Parameters

    /// <summary>
    /// The names of the processes retrieved by the cmdlet.
    /// </summary>
    private string[] processNames;

    /// <summary>
    /// Gets or sets the names of the
    /// process that the cmdlet will retrieve.
    /// </summary>
    [Parameter(
               Position = 0,
               ValueFromPipeline = true,
               ValueFromPipelineByPropertyName = true)]
    [ValidateNotNullOrEmpty]
    public string[] Name
    {
      get { return this.processNames; }
      set { this.processNames = value; }
    }

    #endregion Parameters

    #region Cmdlet Overrides

    /// <summary>
    /// The ProcessRecord method calls the Process.GetProcesses
    /// method to retrieve the processes specified by the Name
    /// parameter. Then, the WriteObject method writes the
    /// associated processes to the pipeline.
    /// </summary>
    protected override void ProcessRecord()
    {
      // If no process names are passed to the cmdlet, get all
      // processes.
      if (this.processNames == null)
      {
        WriteObject(Process.GetProcesses(), true);
      }
      else
      {
        // If process names are passed to the cmdlet, get and write
        // the associated processes.
        foreach (string name in this.processNames)
        {
          WriteObject(Process.GetProcessesByName(name), true);
        }
      } // End if (processNames ...)
    } // End ProcessRecord.

    #endregion Overrides
  } // End GetProcCommand.
  #endregion GetProcCommand
}
```

## <a name="see-also"></a><span data-ttu-id="71bce-131">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="71bce-131">See Also</span></span>

<span data-ttu-id="71bce-132">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md) (Escrevendo um Cmdlet do Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="71bce-132">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md)</span></span>
