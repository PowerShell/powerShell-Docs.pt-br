---
ms.date: 09/13/2016
ms.topic: reference
title: Amostra StopProcessSample02
description: Amostra StopProcessSample02
ms.openlocfilehash: 96171413f9f04d12460d48ba91c2c927e1856fd1
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92666885"
---
# <a name="stopprocesssample02-sample"></a><span data-ttu-id="fbd34-103">Amostra StopProcessSample02</span><span class="sxs-lookup"><span data-stu-id="fbd34-103">StopProcessSample02 Sample</span></span>

<span data-ttu-id="fbd34-104">Este exemplo mostra como escrever um cmdlet que grava mensagens de depuração (WriteDebug), detalhadas (WriteVerbose) e de aviso (WriteWarning) ao parar os processos no computador local.</span><span class="sxs-lookup"><span data-stu-id="fbd34-104">This sample shows how to write a cmdlet that writes debug (WriteDebug), verbose (WriteVerbose), and warning (WriteWarning) messages while stopping processes on the local computer.</span></span> <span data-ttu-id="fbd34-105">Esse cmdlet é semelhante ao `Stop-Process` cmdlet fornecido pelo Windows PowerShell 2,0.</span><span class="sxs-lookup"><span data-stu-id="fbd34-105">This cmdlet is similar to the `Stop-Process` cmdlet provided by Windows PowerShell 2.0.</span></span>

### <a name="how-to-build-the-sample-by-using-visual-studio"></a><span data-ttu-id="fbd34-106">Como criar o exemplo usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fbd34-106">How to build the sample by using Visual Studio.</span></span>

1. <span data-ttu-id="fbd34-107">Abra o Windows Internet Explorer e navegue até o diretório StopProcessSample02 no diretório Samples.</span><span class="sxs-lookup"><span data-stu-id="fbd34-107">Open Windows Internet Explorer and navigate to the StopProcessSample02 directory under the Samples directory.</span></span>

    <span data-ttu-id="fbd34-108">Com o SDK do Windows PowerShell 2,0 instalado, navegue até a pasta StopProcessSample02.</span><span class="sxs-lookup"><span data-stu-id="fbd34-108">With the Windows PowerShell 2.0 SDK installed, navigate to the StopProcessSample02 folder.</span></span> <span data-ttu-id="fbd34-109">O local padrão é C:\Program Files (x86) \Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\csharp\StopProcessSample02.</span><span class="sxs-lookup"><span data-stu-id="fbd34-109">The default location is C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\csharp\StopProcessSample02.</span></span>

2. <span data-ttu-id="fbd34-110">Clique duas vezes no ícone do arquivo da solução (. sln).</span><span class="sxs-lookup"><span data-stu-id="fbd34-110">Double-click the icon for the solution (.sln) file.</span></span> <span data-ttu-id="fbd34-111">Isso abre o projeto de exemplo no Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fbd34-111">This opens the sample project in Microsoft Visual Studio.</span></span>

3. <span data-ttu-id="fbd34-112">No menu **Compilar**, selecione **Compilar Solução**.</span><span class="sxs-lookup"><span data-stu-id="fbd34-112">In the **Build** menu, select **Build Solution**.</span></span>

    <span data-ttu-id="fbd34-113">A biblioteca do exemplo será criada nas pastas \bin ou \bin\Debug padrão.</span><span class="sxs-lookup"><span data-stu-id="fbd34-113">The library for the sample will be built in the default \bin or \bin\debug folders.</span></span>

### <a name="how-to-run-the-sample"></a><span data-ttu-id="fbd34-114">Como executar a amostra</span><span class="sxs-lookup"><span data-stu-id="fbd34-114">How to run the sample</span></span>

1. <span data-ttu-id="fbd34-115">Crie a seguinte pasta de módulo:</span><span class="sxs-lookup"><span data-stu-id="fbd34-115">Create the following module folder:</span></span>

    `[user]/documents/windowspowershell/modules/StopProcessSample02`

2. <span data-ttu-id="fbd34-116">Copie o assembly de exemplo para a pasta do módulo.</span><span class="sxs-lookup"><span data-stu-id="fbd34-116">Copy the sample assembly to the module folder.</span></span>

3. <span data-ttu-id="fbd34-117">Inicie o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fbd34-117">Start Windows PowerShell.</span></span>

4. <span data-ttu-id="fbd34-118">Execute o seguinte comando para carregar o assembly no Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fbd34-118">Run the following command to load the assembly into Windows PowerShell:</span></span>

    `import-module stopprossessample02`

5. <span data-ttu-id="fbd34-119">Execute o seguinte comando para executar o cmdlet:</span><span class="sxs-lookup"><span data-stu-id="fbd34-119">Run the following command to run the cmdlet:</span></span>

    `stop-proc`

## <a name="requirements"></a><span data-ttu-id="fbd34-120">Requisitos</span><span class="sxs-lookup"><span data-stu-id="fbd34-120">Requirements</span></span>

<span data-ttu-id="fbd34-121">Este exemplo requer o Windows PowerShell 2,0.</span><span class="sxs-lookup"><span data-stu-id="fbd34-121">This sample requires Windows PowerShell 2.0.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="fbd34-122">Demonstra</span><span class="sxs-lookup"><span data-stu-id="fbd34-122">Demonstrates</span></span>

<span data-ttu-id="fbd34-123">Este exemplo demonstra o seguinte.</span><span class="sxs-lookup"><span data-stu-id="fbd34-123">This sample demonstrates the following.</span></span>

- <span data-ttu-id="fbd34-124">Declarando uma classe de cmdlet usando o atributo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fbd34-124">Declaring a cmdlet class by using the Cmdlet attribute.</span></span>

- <span data-ttu-id="fbd34-125">Declarando parâmetros de cmdlet usando o atributo Parameter.</span><span class="sxs-lookup"><span data-stu-id="fbd34-125">Declaring a cmdlet parameters by using the Parameter attribute.</span></span>

- <span data-ttu-id="fbd34-126">Gravando mensagens detalhadas.</span><span class="sxs-lookup"><span data-stu-id="fbd34-126">Writing verbose messages.</span></span> <span data-ttu-id="fbd34-127">Para obter mais informações sobre o método usado para gravar mensagens detalhadas, consulte [System. Management. Automation. cmdlet. WriteVerbose](/dotnet/api/System.Management.Automation.Cmdlet.WriteVerbose).</span><span class="sxs-lookup"><span data-stu-id="fbd34-127">For more information about the method used to write verbose messages, see [System.Management.Automation.Cmdlet.WriteVerbose](/dotnet/api/System.Management.Automation.Cmdlet.WriteVerbose).</span></span>

- <span data-ttu-id="fbd34-128">Gravando mensagens de erro.</span><span class="sxs-lookup"><span data-stu-id="fbd34-128">Writing error messages.</span></span> <span data-ttu-id="fbd34-129">Para obter mais informações sobre o método usado para gravar mensagens de erro, consulte [System. Management. Automation. cmdlet. WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError).</span><span class="sxs-lookup"><span data-stu-id="fbd34-129">For more information about the method used to write error messages, see [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError).</span></span>

- <span data-ttu-id="fbd34-130">Gravando mensagens de aviso.</span><span class="sxs-lookup"><span data-stu-id="fbd34-130">Writing warning messages.</span></span> <span data-ttu-id="fbd34-131">Para obter mais informações sobre o método usado para gravar mensagens de aviso, consulte [System. Management. Automation. cmdlet. WriteWarning](/dotnet/api/System.Management.Automation.Cmdlet.WriteWarning).</span><span class="sxs-lookup"><span data-stu-id="fbd34-131">For more information about the method used to write warning messages, see [System.Management.Automation.Cmdlet.WriteWarning](/dotnet/api/System.Management.Automation.Cmdlet.WriteWarning).</span></span>

## <a name="example"></a><span data-ttu-id="fbd34-132">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fbd34-132">Example</span></span>

<span data-ttu-id="fbd34-133">Este exemplo mostra como gravar mensagens de depuração, detalhadas e de aviso usando os `WriteDebug` métodos, `WriteVerbose` e `WriteWarning` .</span><span class="sxs-lookup"><span data-stu-id="fbd34-133">This sample shows how to write debug, verbose, and warning messages by using the `WriteDebug`, `WriteVerbose`, and `WriteWarning` methods.</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Collections;
using Win32Exception = System.ComponentModel.Win32Exception;
using System.Management.Automation;             //Windows PowerShell namespace
using System.Globalization;

namespace Microsoft.Samples.PowerShell.Commands
{
   #region StopProcCommand

    /// <summary>
   /// This class implements the stop-proc cmdlet.
   /// </summary>
   [Cmdlet(VerbsLifecycle.Stop, "Proc",
       SupportsShouldProcess = true)]
   public class StopProcCommand : Cmdlet
   {
       #region Parameters

      /// <summary>
      /// This parameter provides the list of process names on
      /// which the Stop-Proc cmdlet will work.
      /// </summary>
       [Parameter(
          Position = 0,
          Mandatory = true,
          ValueFromPipeline = true,
          ValueFromPipelineByPropertyName = true
       )]
       public string[] Name
       {
          get { return processNames; }
          set { processNames = value; }
       }
       private string[] processNames;

       /// <summary>
       /// This parameter overrides the ShouldContinue call to force
       /// the cmdlet to stop its operation. This parameter should always
       /// be used with caution.
       /// </summary>
       [Parameter]
       public SwitchParameter Force
       {
           get { return force; }
           set { force = value; }
       }
       private bool force;

       /// <summary>
       /// This parameter indicates that the cmdlet should return
       /// an object to the pipeline after the processing has been
       /// completed.
       /// </summary>
       [Parameter]
       public SwitchParameter PassThru
       {
           get { return passThru; }
           set { passThru = value; }
       }
       private bool passThru;

       #endregion Parameters

       #region Cmdlet Overrides

       /// <summary>
       /// The ProcessRecord method does the following for each of the
       /// requested process names:
       /// 1) Check that the process is not a critical process.
       /// 2) Attempt to stop that process.
       /// If no process is requested then nothing occurs.
       /// </summary>
       protected override void ProcessRecord()
       {
           foreach (string name in processNames)
           {
               string message = null;

               // For every process name passed to the cmdlet, get the associated
               // processes.
               // Write a nonterminating error for failure to retrieve
               // a process.

               // Write a user-friendly verbose message to the pipeline. These
               // messages are intended to give the user detailed information
               // on the operations performed by the cmdlet. These messages will
               // appear with the -Verbose option.
               message = String.Format(CultureInfo.CurrentCulture,
                              "Attempting to stop process \"{0}\".", name);
               WriteVerbose(message);

               Process[] processes;

               try
               {
                   processes = Process.GetProcessesByName(name);
               }
               catch (InvalidOperationException ioe)
               {
                   WriteError(new ErrorRecord(ioe,
                                     "UnableToAccessProcessByName",
                                         ErrorCategory.InvalidOperation,
                                             name));
                   continue;
               }

               // Try to stop the processes that have been retrieved.
               foreach (Process process in processes)
               {
                   string processName;

                   try
                   {
                       processName = process.ProcessName;
                   }
                   catch (Win32Exception e)
                   {
                       WriteError(new ErrorRecord(e, "ProcessNameNotFound",
                                         ErrorCategory.ObjectNotFound, process));
                       continue;
                   }

                   // Write a debug message to the host that can be used when
                   // troubleshooting a problem. All debug messages will appear
                   // with the -Debug option.
                   message = String.Format(CultureInfo.CurrentCulture,
                                 "Acquired name for pid {0} : \"{1}\"",
                                        process.Id, processName);
                   WriteDebug(message);

                   // Confirm the operation first.
                   // This is always false if the WhatIf parameter is specified.
                   if (!ShouldProcess(string.Format(CultureInfo.CurrentCulture,
                                        "{0} ({1})",
                                            processName, process.Id)))
                   {
                       continue;
                   }

                   // Make sure that the user really wants to stop a critical
                   // process that can possibly stop the computer.
                   bool criticalProcess = criticalProcessNames.Contains(processName.ToLower(CultureInfo.CurrentCulture));

                   if (criticalProcess && !force)
                   {
                       message = String.Format(CultureInfo.CurrentCulture,
                                    "The process \"{0}\" is a critical process and should not be stopped. Are you sure you wish to stop the process?",
                                        processName);

                       // It is possible that the ProcessRecord method is called
                       // multiple times when objects are received as inputs from
                       // the pipeline. So to retain YesToAll and NoToAll input that
                       // the user may enter across multiple calls to this function,
                       // they are stored as private members of the cmdlet.
                       if (!ShouldContinue(message, "Warning!",
                                    ref yesToAll, ref noToAll))
                       {
                           continue;
                       }
                   } // if (criticalProcess...

                   // Display a warning message if the cmdlet is stopping a
                   // critical process.
                   if (criticalProcess)
                   {
                       message = String.Format(CultureInfo.CurrentCulture,
                                     "Stopping the critical process \"{0}\".",
                                          processName);
                       WriteWarning(message);
                   } // if (criticalProcess...

                   // Stop the named process.
                   try
                   {
                       process.Kill();
                   }
                   catch (Exception e)
                   {
                       if ((e is Win32Exception) || (e is SystemException) ||
                           (e is InvalidOperationException))
                       {
                           // This process could not be stopped so write
                           // a nonterminating error.
                           WriteError(new ErrorRecord(
                                            e,
                                            "CouldNotStopProcess",
                                            ErrorCategory.CloseError,
                                            process)
                                      );
                           continue;
                       } // if ((e is...
                           else throw;
                   } // catch

                   message = String.Format(CultureInfo.CurrentCulture,
                                  "Stopped process \"{0}\", pid {1}.",
                                        processName, process.Id);

                   WriteVerbose(message);

                   // If the PassThru parameter is specified,
                   // return the terminated process object to the pipeline.
                   if (passThru)
                   {
                       message = String.Format(CultureInfo.CurrentCulture,
                                     "Writing process \"{0}\" to pipeline",
                                          processName);
                       WriteDebug(message);
                       WriteObject(process);
                   } // if (passThru...
               } // foreach (Process...
            } // foreach (string...
        } // ProcessRecord

       #endregion Cmdlet Overrides

       #region Private Data

       private bool yesToAll, noToAll;

       /// <summary>
       /// Partial list of critical processes that should not be
       /// stopped.  Lower case is used for case insensitive matching.
       /// </summary>
       private ArrayList criticalProcessNames = new ArrayList(
          new string[] { "system", "winlogon", "spoolsv" }
       );

       #endregion Private Data

   } // StopProcCommand

   #endregion StopProcCommand
}
```

## <a name="see-also"></a><span data-ttu-id="fbd34-134">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="fbd34-134">See Also</span></span>

[<span data-ttu-id="fbd34-135">Escrevendo um Cmdlet do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="fbd34-135">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
