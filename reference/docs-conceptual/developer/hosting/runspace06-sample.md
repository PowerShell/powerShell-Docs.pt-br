---
title: Exemplo de Runspace06 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 471c85f3-9287-45c2-b4bc-833caa1b7634
caps.latest.revision: 8
ms.openlocfilehash: 3850aec88bc800718a82f51c91fbd0cb3c705089
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72367585"
---
# <a name="runspace06-sample"></a>Amostra Runspace06

Este exemplo mostra como adicionar um módulo a um objeto [System. Management. Automation. Runspaces. Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) para que o módulo seja carregado quando o runspace for aberto. O módulo fornece um cmdlet Get-proc (definido pelo [exemplo GetProcessSample02](../cmdlet/getprocesssample02-sample.md)) que é executado de forma síncrona usando um objeto [System. Management. Automation. PowerShell](/dotnet/api/system.management.automation.powershell) .

## <a name="requirements"></a>Requisitos

Este exemplo requer o Windows PowerShell 2,0.

## <a name="demonstrates"></a>Demonstrar

Este exemplo demonstra o seguinte.

- Criando um objeto [System. Management. Automation. Runspaces. Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) .

- Adicionando o módulo ao objeto [System. Management. Automation. Runspaces. Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) .

- Criação de um objeto [System. Management. Automation. Runspaces. runspace](/dotnet/api/System.Management.Automation.Runspaces.Runspace) que usa o objeto [System. Management. Automation. Runspaces. Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) .

- Criando um objeto [System. Management. Automation. PowerShell](/dotnet/api/system.management.automation.powershell) que usa o runspace.

- Adicionar o cmdlet Get-proc do módulo ao pipeline do objeto [System. Management. Automation. PowerShell](/dotnet/api/system.management.automation.powershell) .

- Executando o comando de forma síncrona.

- Extraindo propriedades dos objetos [System. Management. Automation. PSObject](/dotnet/api/System.Management.Automation.PSObject) retornados pelo comando.

## <a name="example"></a>Exemplo

Este exemplo cria um runspace que usa um objeto [System. Management. Automation. Runspaces. Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) para definir os elementos que estão disponíveis quando o runspace é aberto. Neste exemplo, um módulo que define um cmdlet Get-proc é adicionado ao estado de sessão inicial.

```csharp
namespace Microsoft.Samples.PowerShell.Runspaces
{
  using System;
  using System.Collections.ObjectModel;
  using System.Management.Automation;
  using System.Management.Automation.Runspaces;
  using PowerShell = System.Management.Automation.PowerShell;

  /// <summary>
  /// This class contains the Main entry point for this host application.
  /// </summary>
  internal class Runspace06
  {
    /// <summary>
    /// This sample shows how to define an initial session state that is
    /// used when creating a runspace. The sample invokes a command from
    /// a binary module that is loaded by the initial session state.
    /// </summary>
    /// <param name="args">Parameter not used.</param>
    /// <remarks>
    /// This sample assumes that user has coppied the GetProcessSample02.dll
    /// that is produced by the GetProcessSample02 sample to the current
    /// directory.
    /// This sample demonstrates the following:
    /// 1. Creating a default initial session state.
    /// 2. Adding a module to the initial session state.
    /// 3. Creating a runspace that uses the initial session state.
    /// 4. Creating a PowerShell object that uses the runspace.
    /// 5. Adding the module's get-proc cmdlet to the PowerShell object.
    /// 6. Running the command synchronously.
    /// 7. Using PSObject objects to extract and display properties from
    ///    the objects returned by the cmdlet.
    /// </remarks>
    private static void Main(string[] args)
    {
        // Create the default initial session state and add the module.
      InitialSessionState iss = InitialSessionState.CreateDefault();
      iss.ImportPSModule(new string[] { @".\GetProcessSample02.dll" });

      // Create a runspace. Notice that no PSHost object is supplied to the
      // CreateRunspace method so the default host is used. See the Host
      // samples for more information on creating your own custom host.
      using (Runspace myRunSpace = RunspaceFactory.CreateRunspace(iss))
      {
        myRunSpace.Open();

        // Create a PowerShell object.
        using (PowerShell powershell = PowerShell.Create())
        {
          // Add the cmdlet and specify the runspace.
          powershell.AddCommand(@"GetProcessSample02\get-proc");
          powershell.Runspace = myRunSpace;

          Collection<PSObject> results = powershell.Invoke();

          Console.WriteLine("Process              HandleCount");
          Console.WriteLine("--------------------------------");

          // Display the results.
          foreach (PSObject result in results)
          {
            Console.WriteLine(
                              "{0,-20} {1}",
                              result.Members["ProcessName"].Value,
                              result.Members["HandleCount"].Value);
          }
        }

        // Close the runspace to release any resources.
        myRunSpace.Close();
      }

      System.Console.WriteLine("Hit any key to exit...");
      System.Console.ReadKey();
    }
  }
}
```

## <a name="see-also"></a>Consulte Também

[Escrevendo um aplicativo host do Windows PowerShell](./writing-a-windows-powershell-host-application.md)