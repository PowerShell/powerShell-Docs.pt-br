---
ms.date: 09/13/2016
ms.topic: reference
title: Amostra RemoteRunspace01
description: Amostra RemoteRunspace01
ms.openlocfilehash: 13c6213089700e779eb185fe48a67c1616fad437
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92658017"
---
# <a name="remoterunspace01-sample"></a><span data-ttu-id="76d0d-103">Amostra RemoteRunspace01</span><span class="sxs-lookup"><span data-stu-id="76d0d-103">RemoteRunspace01 Sample</span></span>

<span data-ttu-id="76d0d-104">Este exemplo mostra como criar um runspace remoto que é usado para estabelecer uma conexão remota.</span><span class="sxs-lookup"><span data-stu-id="76d0d-104">This sample shows how to create a remote runspace that is used to establish a remote connection.</span></span>

## <a name="requirements"></a><span data-ttu-id="76d0d-105">Requisitos</span><span class="sxs-lookup"><span data-stu-id="76d0d-105">Requirements</span></span>

 <span data-ttu-id="76d0d-106">Este exemplo requer o Windows PowerShell 2,0.</span><span class="sxs-lookup"><span data-stu-id="76d0d-106">This sample requires Windows PowerShell 2.0.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="76d0d-107">Demonstra</span><span class="sxs-lookup"><span data-stu-id="76d0d-107">Demonstrates</span></span>

- <span data-ttu-id="76d0d-108">Criando um objeto [System. Management. Automation. Runspaces. Wsmanconnectioninfo](/dotnet/api/System.Management.Automation.Runspaces.WSManConnectionInfo) .</span><span class="sxs-lookup"><span data-stu-id="76d0d-108">Creating a [System.Management.Automation.Runspaces.Wsmanconnectioninfo](/dotnet/api/System.Management.Automation.Runspaces.WSManConnectionInfo) object.</span></span>

- <span data-ttu-id="76d0d-109">Definindo as propriedades [System. Management. Automation. Runspaces. Runspaceconnectioninfo. OperationTimeout \*](/dotnet/api/System.Management.Automation.Runspaces.RunspaceConnectionInfo.OperationTimeout) e [System. Management. Automation. Runspaces. Runspaceconnectioninfo. OpenTimeout \*](/dotnet/api/System.Management.Automation.Runspaces.RunspaceConnectionInfo.OpenTimeout) do objeto [System. Management. Automation. Runspaces. Wsmanconnectioninfo](/dotnet/api/System.Management.Automation.Runspaces.WSManConnectionInfo) .</span><span class="sxs-lookup"><span data-stu-id="76d0d-109">Setting the [System.Management.Automation.Runspaces.Runspaceconnectioninfo.Operationtimeout\*](/dotnet/api/System.Management.Automation.Runspaces.RunspaceConnectionInfo.OperationTimeout) and [System.Management.Automation.Runspaces.Runspaceconnectioninfo.Opentimeout\*](/dotnet/api/System.Management.Automation.Runspaces.RunspaceConnectionInfo.OpenTimeout) properties of the [System.Management.Automation.Runspaces.Wsmanconnectioninfo](/dotnet/api/System.Management.Automation.Runspaces.WSManConnectionInfo) object.</span></span>

- <span data-ttu-id="76d0d-110">Criar um runspace remoto que usa o objeto [System. Management. Automation. Runspaces. Wsmanconnectioninfo](/dotnet/api/System.Management.Automation.Runspaces.WSManConnectionInfo) para estabelecer a conexão remota.</span><span class="sxs-lookup"><span data-stu-id="76d0d-110">Creating a remote runspace that uses the [System.Management.Automation.Runspaces.Wsmanconnectioninfo](/dotnet/api/System.Management.Automation.Runspaces.WSManConnectionInfo) object to establish the remote connection.</span></span>

- <span data-ttu-id="76d0d-111">Fechando o runspace remoto para liberar a conexão remota.</span><span class="sxs-lookup"><span data-stu-id="76d0d-111">Closing the remote runspace to release the remote connection.</span></span>

## <a name="example"></a><span data-ttu-id="76d0d-112">Exemplo</span><span class="sxs-lookup"><span data-stu-id="76d0d-112">Example</span></span>

<span data-ttu-id="76d0d-113">Este exemplo define uma conexão remota e, em seguida, usa essas informações de conexão para estabelecer uma conexão remota.</span><span class="sxs-lookup"><span data-stu-id="76d0d-113">This sample defines a remote connection and then uses that connection information to establish a remote connection.</span></span>

```csharp
namespace Microsoft.Samples.PowerShell.Runspaces
{
  using System;
  using System.Management.Automation;             // Windows PowerShell namespace.
  using System.Management.Automation.Runspaces;   // Windows PowerShell namespace.

  /// <summary>
  /// This class contains the Main entry point for the application.
  /// </summary>
  internal class RemoteRunspace01
  {
    /// <summary>
    /// This sample shows how to use a WSManConnectionInfo object to set
    /// various timeouts and how to establish a remote connection.
    /// </summary>
    /// <param name="args">This parameter is not used.</param>
    public static void Main(string[] args)
    {
      // Create a WSManConnectionInfo object using the default constructor
      // to connect to the "localHost". The WSManConnectionInfo object can
      // also specify connections to remote computers.
      WSManConnectionInfo connectionInfo = new WSManConnectionInfo();

      // Set the OperationTimeout property. The OperationTimeout is used to tell
      // Windows PowerShell how long to wait (in milliseconds) before timing out
      // for any operation. This includes sending input data to the remote computer,
      // receiving output data from the remote computer, and more. The user can
      // change this timeout depending on whether the connection is to a computer
      // in the data center or across a slow WAN.
      connectionInfo.OperationTimeout = 4 * 60 * 1000; // 4 minutes.

      // Set the OpenTimeout property. OpenTimeout is used to tell Windows PowerShell
      // how long to wait (in milliseconds) before timing out while establishing a
      // remote connection. The user can change this timeout depending on whether the
      // connection is to a computer in the data center or across a slow WAN.
      connectionInfo.OpenTimeout = 1 * 60 * 1000; // 1 minute.

      // Create a remote runspace using the connection information.
      using (Runspace remoteRunspace = RunspaceFactory.CreateRunspace(connectionInfo))
      {
        // Establish the connection by calling the Open() method to open the runspace.
        // The OpenTimeout value set previously will be applied while establishing
        // the connection. Establishing a remote connection involves sending and
        // receiving some data, so the OperationTimeout will also play a role in this process.
        remoteRunspace.Open();

        // Add the code to run commands in the remote runspace here. The
        // OperationTimeout value set previously will play a role here because
        // running commands involves sending and receiving data.

        // Close the connection. Call the Close() method to close the remote
        // runspace. The Dispose() method (called by using primitive) will call
        // the Close() method if it is not already called.
        remoteRunspace.Close();
      }
    }
  }
}
```
