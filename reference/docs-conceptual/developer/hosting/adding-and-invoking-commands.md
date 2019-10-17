---
title: Adicionando e invocando comandos | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 62be8432-28c1-4ca2-bcdb-d0350163fa8c
caps.latest.revision: 5
ms.openlocfilehash: f776f13fe743a3f5f67de0d94883e3f754040ffc
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72367635"
---
# <a name="adding-and-invoking-commands"></a><span data-ttu-id="97ebd-102">Adicionar e invocar comandos</span><span class="sxs-lookup"><span data-stu-id="97ebd-102">Adding and invoking commands</span></span>

<span data-ttu-id="97ebd-103">Depois de criar um runspace, você pode adicionar PowerShellcommands e scripts do Windows a um pipeline e, em seguida, invocar o pipeline de forma síncrona ou assíncrona.</span><span class="sxs-lookup"><span data-stu-id="97ebd-103">After creating a runspace, you can add Windows PowerShellcommands and scripts to a pipeline, and then invoke the pipeline synchronously or asynchronously.</span></span>

## <a name="creating-a-pipeline"></a><span data-ttu-id="97ebd-104">Criando um pipeline</span><span class="sxs-lookup"><span data-stu-id="97ebd-104">Creating a pipeline</span></span>

 <span data-ttu-id="97ebd-105">A classe [System. Management. Automation. PowerShell](/dotnet/api/system.management.automation.powershell) fornece vários métodos para adicionar comandos, parâmetros e scripts ao pipeline.</span><span class="sxs-lookup"><span data-stu-id="97ebd-105">The [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) class provides several methods to add commands, parameters, and scripts to the pipeline.</span></span> <span data-ttu-id="97ebd-106">Você pode invocar o pipeline de forma síncrona chamando uma sobrecarga do método [System. Management. Automation. PowerShell. Invoke \*](/dotnet/api/System.Management.Automation.PowerShell.Invoke) , ou assincronamente, chamando uma sobrecarga de [System. Management. Automation. PowerShell. BeginInvoke \*](/dotnet/api/System.Management.Automation.PowerShell.BeginInvoke) e então o método [System. Management. Automation. PowerShell. EndInvoke \*](/dotnet/api/System.Management.Automation.PowerShell.EndInvoke) .</span><span class="sxs-lookup"><span data-stu-id="97ebd-106">You can invoke the pipeline synchronously by calling an overload of the [System.Management.Automation.Powershell.Invoke\*](/dotnet/api/System.Management.Automation.PowerShell.Invoke) method, or asynchronously by calling an overload of the [System.Management.Automation.Powershell.Begininvoke\*](/dotnet/api/System.Management.Automation.PowerShell.BeginInvoke) and then the [System.Management.Automation.Powershell.Endinvoke\*](/dotnet/api/System.Management.Automation.PowerShell.EndInvoke) method.</span></span>

### <a name="addcommand"></a><span data-ttu-id="97ebd-107">O AddCommand</span><span class="sxs-lookup"><span data-stu-id="97ebd-107">AddCommand</span></span>

1. <span data-ttu-id="97ebd-108">Crie um objeto [System. Management. Automation. PowerShell](/dotnet/api/system.management.automation.powershell) .</span><span class="sxs-lookup"><span data-stu-id="97ebd-108">Create a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) object.</span></span>

   ```csharp
   PowerShell ps = PowerShell.Create();
   ```

2. <span data-ttu-id="97ebd-109">Adicione o comando que você deseja executar.</span><span class="sxs-lookup"><span data-stu-id="97ebd-109">Add the command that you want to execute.</span></span>

   ```csharp
   ps.AddCommand("Get-Process");
   ```

3. <span data-ttu-id="97ebd-110">Invoque o comando.</span><span class="sxs-lookup"><span data-stu-id="97ebd-110">Invoke the command.</span></span>

   ```csharp
   ps.Invoke();
   ```

 <span data-ttu-id="97ebd-111">Se você chamar o método [System. Management. Automation. PowerShell. AddCommand \*](/dotnet/api/System.Management.Automation.PowerShell.AddCommand) mais de uma vez antes de chamar o método [System. Management. Automation. PowerShell. Invoke \*](/dotnet/api/System.Management.Automation.PowerShell.Invoke) , o resultado do primeiro comando será canalizado para o segundo e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="97ebd-111">If you call the [System.Management.Automation.Powershell.Addcommand\*](/dotnet/api/System.Management.Automation.PowerShell.AddCommand) method more than once before you call the [System.Management.Automation.Powershell.Invoke\*](/dotnet/api/System.Management.Automation.PowerShell.Invoke) method, the result of the first command is piped to the second, and so on.</span></span> <span data-ttu-id="97ebd-112">Se você não quiser canalizar o resultado de um comando anterior para um comando, adicione-o chamando o [System. Management. Automation. PowerShell. setstatement \*](/dotnet/api/System.Management.Automation.PowerShell.AddStatement) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="97ebd-112">If you do not want to pipe the result of a previous command to a command, add it by calling the [System.Management.Automation.Powershell.Addstatement\*](/dotnet/api/System.Management.Automation.PowerShell.AddStatement) instead.</span></span>

### <a name="addparameter"></a><span data-ttu-id="97ebd-113">AddParameter</span><span class="sxs-lookup"><span data-stu-id="97ebd-113">AddParameter</span></span>

 <span data-ttu-id="97ebd-114">O exemplo anterior executa um único comando sem parâmetros.</span><span class="sxs-lookup"><span data-stu-id="97ebd-114">The previous example executes a single command without any parameters.</span></span> <span data-ttu-id="97ebd-115">Você pode adicionar parâmetros ao comando usando o método [System. Management. Automation. PSCommand. AddParameter \*](/dotnet/api/System.Management.Automation.PSCommand.AddParameter) , por exemplo, o código a seguir obtém uma lista de todos os processos nomeados `PowerShell` em execução no computador.</span><span class="sxs-lookup"><span data-stu-id="97ebd-115">You can add parameters to the command by using the [System.Management.Automation.Pscommand.Addparameter\*](/dotnet/api/System.Management.Automation.PSCommand.AddParameter) method For example, the following code gets a list of all of the processes that are named `PowerShell` running on the machine.</span></span>

```csharp
PowerShell.Create().AddCommand("Get-Process")
                   .AddParameter("Name", "PowerShell")
                   .Invoke();
```

 <span data-ttu-id="97ebd-116">Você pode adicionar parâmetros adicionais chamando [System. Management. Automation. PSCommand. AddParameter \*](/dotnet/api/System.Management.Automation.PSCommand.AddParameter) repetidamente.</span><span class="sxs-lookup"><span data-stu-id="97ebd-116">You can add additional parameters by calling [System.Management.Automation.Pscommand.Addparameter\*](/dotnet/api/System.Management.Automation.PSCommand.AddParameter) repeatedly.</span></span>

```csharp
PowerShell.Create().AddCommand("Get-Process")
                   .AddParameter("Name", "PowerShell")
                   .AddParameter("Id", "12768")
                   .Invoke();
```

 <span data-ttu-id="97ebd-117">Você também pode adicionar um dicionário de nomes e valores de parâmetro chamando o método [System. Management. Automation. PowerShell. Parameters \*](/dotnet/api/System.Management.Automation.PowerShell.AddParameters) .</span><span class="sxs-lookup"><span data-stu-id="97ebd-117">You can also add a dictionary of parameter names and values by calling the [System.Management.Automation.Powershell.Addparameters\*](/dotnet/api/System.Management.Automation.PowerShell.AddParameters) method.</span></span>

```csharp
IDictionary parameters = new Dictionary<String, String>();
parameters.Add("Name", "PowerShell");

parameters.Add("Id", "12768");
PowerShell.Create().AddCommand("Get-Process")
   .AddParameters(parameters)
      .Invoke()

```

### <a name="addstatement"></a><span data-ttu-id="97ebd-118">Addstatement</span><span class="sxs-lookup"><span data-stu-id="97ebd-118">AddStatement</span></span>

 <span data-ttu-id="97ebd-119">Você pode simular o envio em lote usando o método [System. Management. Automation. PowerShell. addstatement \*](/dotnet/api/System.Management.Automation.PowerShell.AddStatement) , que adiciona uma instrução adicional ao final do pipeline. o código a seguir obtém uma lista de processos em execução com o nome `PowerShell` e, em seguida, Obtém a lista de serviços em execução.</span><span class="sxs-lookup"><span data-stu-id="97ebd-119">You can simulate batching by using the [System.Management.Automation.Powershell.Addstatement\*](/dotnet/api/System.Management.Automation.PowerShell.AddStatement) method, which adds an additional statement to the end of the pipeline The following code gets a list of running processes with the name `PowerShell`, and then gets the list of running services.</span></span>

```csharp
PowerShell ps = PowerShell.Create();
ps.AddCommand("Get-Process").AddParameter("Name", "PowerShell");
ps.AddStatement().AddCommand("Get-Service");
ps.Invoke();
```

### <a name="addscript"></a><span data-ttu-id="97ebd-120">AddScript</span><span class="sxs-lookup"><span data-stu-id="97ebd-120">AddScript</span></span>

 <span data-ttu-id="97ebd-121">Você pode executar um script existente chamando o método [System. Management. Automation. PowerShell. addScript \*](/dotnet/api/System.Management.Automation.PowerShell.AddScript) .</span><span class="sxs-lookup"><span data-stu-id="97ebd-121">You can run an existing script by calling the [System.Management.Automation.Powershell.Addscript\*](/dotnet/api/System.Management.Automation.PowerShell.AddScript) method.</span></span> <span data-ttu-id="97ebd-122">O exemplo a seguir adiciona um script ao pipeline e o executa.</span><span class="sxs-lookup"><span data-stu-id="97ebd-122">The following example adds a script to the pipeline and runs it.</span></span> <span data-ttu-id="97ebd-123">Este exemplo pressupõe que já existe um script chamado `MyScript.ps1` em uma pasta chamada `D:\PSScripts`.</span><span class="sxs-lookup"><span data-stu-id="97ebd-123">This example assumes there is already a script named `MyScript.ps1` in a folder named `D:\PSScripts`.</span></span>

```csharp
PowerShell ps = PowerShell.Create();
ps.AddScript("D:\PSScripts\MyScript.ps1").Invoke();
```

 <span data-ttu-id="97ebd-124">Também há uma versão do método [System. Management. Automation. PowerShell. addScript \*](/dotnet/api/System.Management.Automation.PowerShell.AddScript) que usa um parâmetro booliano denominado `useLocalScope`.</span><span class="sxs-lookup"><span data-stu-id="97ebd-124">There is also a version of the [System.Management.Automation.Powershell.Addscript\*](/dotnet/api/System.Management.Automation.PowerShell.AddScript) method that takes a boolean parameter named `useLocalScope`.</span></span> <span data-ttu-id="97ebd-125">Se esse parâmetro for definido como `true`, o script será executado no escopo local.</span><span class="sxs-lookup"><span data-stu-id="97ebd-125">If this parameter is set to `true`, then the script is run in the local scope.</span></span> <span data-ttu-id="97ebd-126">O código a seguir executará o script no escopo local.</span><span class="sxs-lookup"><span data-stu-id="97ebd-126">The following code will run the script in the local scope.</span></span>

```csharp
PowerShell ps = PowerShell.Create();
ps.AddScript(@"D:\PSScripts\MyScript.ps1", true).Invoke();
```

### <a name="invoking-a-pipeline-synchronously"></a><span data-ttu-id="97ebd-127">Invocar um pipeline de forma síncrona</span><span class="sxs-lookup"><span data-stu-id="97ebd-127">Invoking a pipeline synchronously</span></span>

 <span data-ttu-id="97ebd-128">Depois de adicionar elementos ao pipeline, você o invoca.</span><span class="sxs-lookup"><span data-stu-id="97ebd-128">After you add elements to the pipeline, you invoke it.</span></span> <span data-ttu-id="97ebd-129">Para invocar o pipeline de forma síncrona, você chama uma sobrecarga do método [System. Management. Automation. PowerShell. Invoke \*](/dotnet/api/System.Management.Automation.PowerShell.Invoke) .</span><span class="sxs-lookup"><span data-stu-id="97ebd-129">To invoke the pipeline synchronously, you call an overload of the [System.Management.Automation.Powershell.Invoke\*](/dotnet/api/System.Management.Automation.PowerShell.Invoke) method.</span></span> <span data-ttu-id="97ebd-130">O exemplo a seguir mostra como invocar de forma síncrona um pipeline.</span><span class="sxs-lookup"><span data-stu-id="97ebd-130">The following example shows how to synchronously invoke a pipeline.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Management.Automation;

namespace HostPS1e
{
  class HostPS1e
  {
    static void Main(string[] args)
    {
      // Using the PowerShell.Create and AddCommand
      // methods, create a command pipeline.
      PowerShell ps = PowerShell.Create().AddCommand ("Sort-Object");

      // Using the PowerShell.Invoke method, run the command
      // pipeline using the supplied input.
      foreach (PSObject result in ps.Invoke(new int[] { 3, 1, 6, 2, 5, 4 }))
      {
          Console.WriteLine("{0}", result);
      } // End foreach.
    } // End Main.
  } // End HostPS1e.
}
```

### <a name="invoking-a-pipeline-asynchronously"></a><span data-ttu-id="97ebd-131">Invocar um pipeline de forma assíncrona</span><span class="sxs-lookup"><span data-stu-id="97ebd-131">Invoking a pipeline asynchronously</span></span>

 <span data-ttu-id="97ebd-132">Você invoca um pipeline de forma assíncrona chamando uma sobrecarga de [System. Management. Automation. PowerShell. BeginInvoke \*](/dotnet/api/System.Management.Automation.PowerShell.BeginInvoke) para criar um objeto [IAsyncResult](https://msdn.microsoft.com/library/system.iasyncresult\(v=vs.110\).aspx) e, em seguida, chamar [System. Management. Automation. PowerShell. EndInvoke \*](/dotnet/api/System.Management.Automation.PowerShell.EndInvoke) método.</span><span class="sxs-lookup"><span data-stu-id="97ebd-132">You invoke a pipeline asynchronously by calling an overload of the [System.Management.Automation.Powershell.Begininvoke\*](/dotnet/api/System.Management.Automation.PowerShell.BeginInvoke) to create an [IAsyncResult](https://msdn.microsoft.com/library/system.iasyncresult\(v=vs.110\).aspx) object, and then calling the [System.Management.Automation.Powershell.Endinvoke\*](/dotnet/api/System.Management.Automation.PowerShell.EndInvoke) method.</span></span>

 <span data-ttu-id="97ebd-133">O exemplo a seguir mostra como invocar um pipeline de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="97ebd-133">The following example shows how to invoke a pipeline asynchronously.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Management.Automation;

namespace HostPS3
{
  class HostPS3
  {
    static void Main(string[] args)
    {
      // Use the PowerShell.Create and PowerShell.AddCommand
      // methods to create a command pipeline that includes
      // Get-Process cmdlet. Do not include spaces immediately
      // before or after the cmdlet name as that will cause
      // the command to fail.
      PowerShell ps = PowerShell.Create().AddCommand("Get-Process");

      // Create an IAsyncResult object and call the
      // BeginInvoke method to start running the
      // command pipeline asynchronously.
      IAsyncResult async = ps.BeginInvoke();

      // Using the PowerShell.Invoke method, run the command
      // pipeline using the default runspace.
      foreach (PSObject result in ps.EndInvoke(async))
      {
        Console.WriteLine("{0,-20}{1}",
                result.Members["ProcessName"].Value,
                result.Members["Id"].Value);
      } // End foreach.
      System.Console.WriteLine("Hit any key to exit.");
      System.Console.ReadKey();
    } // End Main.
  } // End HostPS3.
}
```

## <a name="see-also"></a><span data-ttu-id="97ebd-134">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="97ebd-134">See Also</span></span>

 [<span data-ttu-id="97ebd-135">Criando um InitialSessionState</span><span class="sxs-lookup"><span data-stu-id="97ebd-135">Creating an InitialSessionState</span></span>](./creating-an-initialsessionstate.md)

 [<span data-ttu-id="97ebd-136">Criando um runspace restrito</span><span class="sxs-lookup"><span data-stu-id="97ebd-136">Creating a constrained runspace</span></span>](./creating-a-constrained-runspace.md)