---
title: Métodos de processamento de entrada de cmdlet | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- virtual methods (PowerShell SDK]
ms.assetid: b0bb8172-c9fa-454b-9f1b-57c3fe60671b
caps.latest.revision: 12
ms.openlocfilehash: a28c8d3df19bc72bf338d6abc4e02768c5097209
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72369865"
---
# <a name="cmdlet-input-processing-methods"></a><span data-ttu-id="7e45e-102">Métodos de processamento de entrada de cmdlet</span><span class="sxs-lookup"><span data-stu-id="7e45e-102">Cmdlet Input Processing Methods</span></span>

<span data-ttu-id="7e45e-103">Os cmdlets devem substituir um ou mais dos métodos de processamento de entrada descritos neste tópico para executar seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="7e45e-103">Cmdlets must override one or more of the input processing methods described in this topic to perform their work.</span></span>
<span data-ttu-id="7e45e-104">Esses métodos permitem que o cmdlet execute operações de pré-processamento, processamento de entrada e pós-processamento.</span><span class="sxs-lookup"><span data-stu-id="7e45e-104">These methods allow the cmdlet to perform operations of pre-processing, input processing, and post-processing.</span></span>
<span data-ttu-id="7e45e-105">Esses métodos também permitem que você interrompa o processamento de cmdlets.</span><span class="sxs-lookup"><span data-stu-id="7e45e-105">These methods also allow you to stop cmdlet processing.</span></span>
<span data-ttu-id="7e45e-106">Para obter um exemplo mais detalhado de como usar esses métodos, consulte o [tutorial do SelectStr](selectstr-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="7e45e-106">For a more detailed example of how to use these methods, see [SelectStr Tutorial](selectstr-tutorial.md).</span></span>

## <a name="pre-processing-operations"></a><span data-ttu-id="7e45e-107">Operações de pré-processamento</span><span class="sxs-lookup"><span data-stu-id="7e45e-107">Pre-Processing Operations</span></span>

<span data-ttu-id="7e45e-108">Os cmdlets devem substituir o método [System. Management. Automation. cmdlet. BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) para adicionar quaisquer operações de pré-processamento que sejam válidas para todos os registros que serão processados posteriormente pelo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7e45e-108">Cmdlets should override the [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) method to add any preprocessing operations that are valid for all the records that will be processed later by the cmdlet.</span></span>
<span data-ttu-id="7e45e-109">Quando o PowerShell processa um pipeline de comando, o PowerShell chama esse método uma vez para cada instância do cmdlet no pipeline.</span><span class="sxs-lookup"><span data-stu-id="7e45e-109">When PowerShell processes a command pipeline, PowerShell calls this method once for each instance of the cmdlet in the pipeline.</span></span>
<span data-ttu-id="7e45e-110">Para obter mais informações sobre como o PowerShell invoca o pipeline de comando, consulte [ciclo de vida de processamento de cmdlet](/previous-versions/ms714429(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="7e45e-110">For more information about how PowerShell invokes the command pipeline, see [Cmdlet Processing Lifecycle](/previous-versions/ms714429(v=vs.85)).</span></span>

<span data-ttu-id="7e45e-111">O código a seguir mostra uma implementação do método BeginProcessing.</span><span class="sxs-lookup"><span data-stu-id="7e45e-111">The following code shows an implementation of the BeginProcessing method.</span></span>

```csharp
protected override void BeginProcessing()
{
  // Replace the WriteObject method with the logic required by your cmdlet.
  WriteObject("This is a test of the BeginProcessing template.");
}
```

## <a name="input-processing-operations"></a><span data-ttu-id="7e45e-112">Operações de processamento de entrada</span><span class="sxs-lookup"><span data-stu-id="7e45e-112">Input Processing Operations</span></span>

<span data-ttu-id="7e45e-113">Os cmdlets podem substituir o método [System. Management. Automation. cmdlet. ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) para processar a entrada que é enviada para o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7e45e-113">Cmdlets can override the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method to process the input that is sent to the cmdlet.</span></span>
<span data-ttu-id="7e45e-114">Quando o PowerShell processa um pipeline de comando, o PowerShell chama esse método para cada registro de entrada que é processado pelo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7e45e-114">When PowerShell processes a command pipeline, PowerShell calls this method for each input record that is processed by the cmdlet.</span></span>
<span data-ttu-id="7e45e-115">Para obter mais informações sobre como o PowerShell invoca o pipeline de comando, consulte [ciclo de vida de processamento de cmdlet](/previous-versions/ms714429(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="7e45e-115">For more information about how PowerShell invokes the command pipeline, see [Cmdlet Processing Lifecycle](/previous-versions/ms714429(v=vs.85)).</span></span>

<span data-ttu-id="7e45e-116">O código a seguir mostra uma implementação do método ProcessRecord.</span><span class="sxs-lookup"><span data-stu-id="7e45e-116">The following code shows an implementation of the ProcessRecord method.</span></span>

```csharp
protected override void ProcessRecord()
{
  // Replace the WriteObject method with the logic required by your cmdlet.
  WriteObject("This is a test of the ProcessRecord template.");
}
```

## <a name="post-processing-operations"></a><span data-ttu-id="7e45e-117">Operações de pós-processamento</span><span class="sxs-lookup"><span data-stu-id="7e45e-117">Post-Processing Operations</span></span>

<span data-ttu-id="7e45e-118">Os cmdlets devem substituir o método [System. Management. Automation. cmdlet. Endprocessor](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) para adicionar quaisquer operações de pós-processamento que sejam válidas para todos os registros que foram processados pelo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7e45e-118">Cmdlets should override the [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) method to add any post-processing operations that are valid for all the records that were processed by the cmdlet.</span></span>
<span data-ttu-id="7e45e-119">Por exemplo, o cmdlet pode precisar limpar as variáveis de objeto após o processamento terminar.</span><span class="sxs-lookup"><span data-stu-id="7e45e-119">For example, your cmdlet might have to clean up object variables after it is finished processing.</span></span>

<span data-ttu-id="7e45e-120">Quando o PowerShell processa um pipeline de comando, o PowerShell chama esse método uma vez para cada instância do cmdlet no pipeline.</span><span class="sxs-lookup"><span data-stu-id="7e45e-120">When PowerShell processes a command pipeline, PowerShell calls this method once for each instance of the cmdlet in the pipeline.</span></span>
<span data-ttu-id="7e45e-121">No entanto, é importante lembrar que o tempo de execução do PowerShell não chamará o método endprocessor se o cmdlet for cancelado no meio de seu processamento de entrada ou se ocorrer um erro de encerramento em qualquer parte do cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7e45e-121">However, it is important to remember that the PowerShell runtime will not call the EndProcessing method if the cmdlet is canceled midway through its input processing or if a terminating error occurs in any part of the cmdlet.</span></span>
<span data-ttu-id="7e45e-122">Por esse motivo, um cmdlet que requer a limpeza de objeto deve implementar o padrão [System. IDisposable](/dotnet/api/System.IDisposable) completo, incluindo um finalizador, para que o tempo de execução possa chamar os métodos EndProcessing e [System. IDisposable. Dispose](/dotnet/api/System.IDisposable.Dispose) no final de processamento.</span><span class="sxs-lookup"><span data-stu-id="7e45e-122">For this reason, a cmdlet that requires object cleanup should implement the complete [System.IDisposable](/dotnet/api/System.IDisposable) pattern, including a finalizer, so that the runtime can call both the EndProcessing and [System.IDisposable.Dispose](/dotnet/api/System.IDisposable.Dispose) methods at the end of processing.</span></span>
<span data-ttu-id="7e45e-123">Para obter mais informações sobre como o PowerShell invoca o pipeline de comando, consulte [ciclo de vida de processamento de cmdlet](/previous-versions/ms714429(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="7e45e-123">For more information about how PowerShell invokes the command pipeline, see [Cmdlet Processing Lifecycle](/previous-versions/ms714429(v=vs.85)).</span></span>

<span data-ttu-id="7e45e-124">O código a seguir mostra uma implementação do método endprocessor.</span><span class="sxs-lookup"><span data-stu-id="7e45e-124">The following code shows an implementation of the EndProcessing method.</span></span>

```csharp
protected override void EndProcessing()
{
  // Replace the WriteObject method with the logic required by your cmdlet.
  WriteObject("This is a test of the EndProcessing template.");
}
```

## <a name="see-also"></a><span data-ttu-id="7e45e-125">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="7e45e-125">See Also</span></span>

[<span data-ttu-id="7e45e-126">System. Management. Automation. cmdlet. BeginProcessing</span><span class="sxs-lookup"><span data-stu-id="7e45e-126">System.Management.Automation.Cmdlet.BeginProcessing</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing)

[<span data-ttu-id="7e45e-127">System. Management. Automation. cmdlet. ProcessRecord</span><span class="sxs-lookup"><span data-stu-id="7e45e-127">System.Management.Automation.Cmdlet.ProcessRecord</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord)

[<span data-ttu-id="7e45e-128">Sistema. Management. Automation. cmdlet. endprocessation</span><span class="sxs-lookup"><span data-stu-id="7e45e-128">System.Management.Automation.Cmdlet.EndProcessing</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing)

[<span data-ttu-id="7e45e-129">Tutorial do SelectStr</span><span class="sxs-lookup"><span data-stu-id="7e45e-129">SelectStr Tutorial</span></span>](selectstr-tutorial.md)

[<span data-ttu-id="7e45e-130">System. IDisposable</span><span class="sxs-lookup"><span data-stu-id="7e45e-130">System.IDisposable</span></span>](/dotnet/api/System.IDisposable)

[<span data-ttu-id="7e45e-131">SDK do shell do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e45e-131">Windows PowerShell Shell SDK</span></span>](../windows-powershell-reference.md)