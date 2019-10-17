---
title: Interpretando objetos ErrorRecord | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2a65b964-5bc6-4ade-a66b-b6afa7351ce7
caps.latest.revision: 9
ms.openlocfilehash: 32ebf2531237bfd1042310ccc4155193a58401fd
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72365415"
---
# <a name="interpreting-errorrecord-objects"></a><span data-ttu-id="7471a-102">Interpretar objetos ErrorRecord</span><span class="sxs-lookup"><span data-stu-id="7471a-102">Interpreting ErrorRecord Objects</span></span>

<span data-ttu-id="7471a-103">Na maioria dos casos, um objeto [System. Management. Automation. ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) representa um erro de não finalização gerado por um comando ou script.</span><span class="sxs-lookup"><span data-stu-id="7471a-103">In most cases, an [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) object represents a non-terminating error generated by a command or script.</span></span> <span data-ttu-id="7471a-104">Os erros de encerramento também podem especificar as informações adicionais em um ErrorRecord por meio da interface [System. Management. Automation. Icontainserrorrecord](/dotnet/api/System.Management.Automation.IContainsErrorRecord) .</span><span class="sxs-lookup"><span data-stu-id="7471a-104">Terminating errors can also specify the additional information in an ErrorRecord via the [System.Management.Automation.Icontainserrorrecord](/dotnet/api/System.Management.Automation.IContainsErrorRecord) interface.</span></span>

<span data-ttu-id="7471a-105">Se você quiser escrever um manipulador de erro em seu script ou um host para tratar erros específicos que ocorrem durante a execução do comando ou do script, você deve interpretar o objeto [System. Management. Automation. ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) para determinar se ele representa a classe de erro que você deseja manipular.</span><span class="sxs-lookup"><span data-stu-id="7471a-105">If you want to write an error handler in your script or a host to handle specific errors that occur during command or script execution, you must interpret the [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) object to determine whether it represents the class of error that you want to handle.</span></span>

<span data-ttu-id="7471a-106">Quando um cmdlet encontra um erro de encerramento ou de não encerramento, ele deve criar um registro de erro que descreva a condição de erro.</span><span class="sxs-lookup"><span data-stu-id="7471a-106">When a cmdlet encounters a terminating or non-terminating error, it should create an error record that describes the error condition.</span></span> <span data-ttu-id="7471a-107">O aplicativo host deve investigar esses registros de erros e executar qualquer ação que reduza o erro.</span><span class="sxs-lookup"><span data-stu-id="7471a-107">The host application must investigate these error records and perform whatever action will mitigate the error.</span></span> <span data-ttu-id="7471a-108">O aplicativo host também deve investigar registros de erro para erros de não encerramento que falharam ao processar um registro, mas que pudesse continuar e deve investigar os registros de erro para erros de encerramento que fizeram com que o pipeline fosse interrompido.</span><span class="sxs-lookup"><span data-stu-id="7471a-108">The host application must also investigate error records for nonterminating errors that failed to process a record but were able to continue, and it must investigate error records for terminating errors that caused the pipeline to stop.</span></span>

> [!NOTE]
> <span data-ttu-id="7471a-109">Para erros de encerramento, o cmdlet chama o método [System. Management. Automation. cmdlet. ThrowTerminatingError \*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) .</span><span class="sxs-lookup"><span data-stu-id="7471a-109">For terminating errors, the cmdlet calls the [System.Management.Automation.Cmdlet.Throwterminatingerror\*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) method.</span></span> <span data-ttu-id="7471a-110">Para erros de não encerramento, o cmdlet chama o método [System. Management. Automation. cmdlet. WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) .</span><span class="sxs-lookup"><span data-stu-id="7471a-110">For non-terminating errors, the cmdlet calls the [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) method.</span></span>

## <a name="error-record-design"></a><span data-ttu-id="7471a-111">Design do registro de erros</span><span class="sxs-lookup"><span data-stu-id="7471a-111">Error Record Design</span></span>

<span data-ttu-id="7471a-112">Os registros de erro são projetados para fornecer informações de erro adicionais que não estão disponíveis em exceções, garantindo que as informações combinadas em cada registro de erro sejam exclusivas.</span><span class="sxs-lookup"><span data-stu-id="7471a-112">Error records are designed to provide additional error information that is not available in exceptions while ensuring that the combined information in each error record is unique.</span></span> <span data-ttu-id="7471a-113">Essa exclusividade permite que o aplicativo host inspecione as diferentes partes do registro de erros para que ele possa identificar a condição de erro e a ação que o host deve executar.</span><span class="sxs-lookup"><span data-stu-id="7471a-113">This uniqueness allows the host application to inspect the different parts of the error record so that it can identify the error condition and the action the host must take.</span></span>

## <a name="interpreting-error-records"></a><span data-ttu-id="7471a-114">Interpretando registros de erro</span><span class="sxs-lookup"><span data-stu-id="7471a-114">Interpreting Error Records</span></span>

<span data-ttu-id="7471a-115">Você pode examinar várias partes do registro de erro para identificar o erro.</span><span class="sxs-lookup"><span data-stu-id="7471a-115">You can review several parts of the error record to identify the error.</span></span> <span data-ttu-id="7471a-116">Essas partes incluem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7471a-116">These parts include the following:</span></span>

- <span data-ttu-id="7471a-117">A categoria de erro</span><span class="sxs-lookup"><span data-stu-id="7471a-117">The error category</span></span>

- <span data-ttu-id="7471a-118">A exceção de erro</span><span class="sxs-lookup"><span data-stu-id="7471a-118">The error exception</span></span>

- <span data-ttu-id="7471a-119">O identificador de erro totalmente qualificado (FQID)</span><span class="sxs-lookup"><span data-stu-id="7471a-119">The fully qualified error identifier (FQID)</span></span>

- <span data-ttu-id="7471a-120">Outras informações</span><span class="sxs-lookup"><span data-stu-id="7471a-120">Other information</span></span>

### <a name="the-error-category"></a><span data-ttu-id="7471a-121">A categoria de erro</span><span class="sxs-lookup"><span data-stu-id="7471a-121">The Error Category</span></span>

<span data-ttu-id="7471a-122">A categoria de erro do registro de erro é uma das constantes predefinidas fornecidas pela enumeração [System. Management. Automation. ErrorCategory](/dotnet/api/System.Management.Automation.ErrorCategory) .</span><span class="sxs-lookup"><span data-stu-id="7471a-122">The error category of the error record is one of the predefined constants provided by the [System.Management.Automation.Errorcategory](/dotnet/api/System.Management.Automation.ErrorCategory) enumeration.</span></span> <span data-ttu-id="7471a-123">Essas informações estão disponíveis por meio da propriedade [System. Management. Automation. ErrorRecord. CategoryInfo](/dotnet/api/System.Management.Automation.ErrorRecord.CategoryInfo) do objeto [System. Management. Automation. ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) .</span><span class="sxs-lookup"><span data-stu-id="7471a-123">This information  is available through the [System.Management.Automation.ErrorRecord.CategoryInfo](/dotnet/api/System.Management.Automation.ErrorRecord.CategoryInfo) property of the [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) object.</span></span>

<span data-ttu-id="7471a-124">O cmdlet pode especificar as categorias CloseError, OpenError, invalidatype, ReadError e WriteError e outras categorias de erro.</span><span class="sxs-lookup"><span data-stu-id="7471a-124">The cmdlet can specify the CloseError, OpenError, InvalidType, ReadError, and WriteError categories, and other error categories.</span></span> <span data-ttu-id="7471a-125">O aplicativo host pode usar a categoria de erro para capturar grupos de erros.</span><span class="sxs-lookup"><span data-stu-id="7471a-125">The host application can use the error category to capture groups of errors.</span></span>

### <a name="the-exception"></a><span data-ttu-id="7471a-126">A exceção</span><span class="sxs-lookup"><span data-stu-id="7471a-126">The Exception</span></span>

<span data-ttu-id="7471a-127">A exceção incluída no registro de erro é fornecida pelo cmdlet e pode ser acessada por meio da propriedade [System. Management. Automation. ErrorRecord. Exception \*](/dotnet/api/System.Management.Automation.ErrorRecord.Exception) do objeto [System. Management. Automation. ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) .</span><span class="sxs-lookup"><span data-stu-id="7471a-127">The exception included in the error record is provided by the cmdlet and can be accessed through the [System.Management.Automation.ErrorRecord.Exception\*](/dotnet/api/System.Management.Automation.ErrorRecord.Exception) property of the [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) object.</span></span>

<span data-ttu-id="7471a-128">Os aplicativos host podem usar a palavra-chave `is` para identificar que a exceção é de uma classe específica ou de uma classe derivada.</span><span class="sxs-lookup"><span data-stu-id="7471a-128">Host applications can use the `is` keyword to identify that the exception is of a specific class or of a derived class.</span></span> <span data-ttu-id="7471a-129">É melhor ramificar o tipo de exceção, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="7471a-129">It is better to branch on the exception type, as shown in the following example.</span></span>

`if (MyNonTerminatingError.Exception is AccessDeniedException)`

<span data-ttu-id="7471a-130">Dessa forma, você captura as classes derivadas.</span><span class="sxs-lookup"><span data-stu-id="7471a-130">This way, you catch the derived classes.</span></span> <span data-ttu-id="7471a-131">No entanto, há problemas se a exceção for desserializada.</span><span class="sxs-lookup"><span data-stu-id="7471a-131">However, there are problems if the exception is deserialized.</span></span>

### <a name="the-fqid"></a><span data-ttu-id="7471a-132">O FQID</span><span class="sxs-lookup"><span data-stu-id="7471a-132">The FQID</span></span>

<span data-ttu-id="7471a-133">O FQID é a informação mais específica que você pode usar para identificar o erro.</span><span class="sxs-lookup"><span data-stu-id="7471a-133">The FQID is the most specific information you can use to identify the error.</span></span> <span data-ttu-id="7471a-134">É uma cadeia de caracteres que inclui um identificador definido por cmdlet, o nome da classe de cmdlet e a fonte que relatou o erro.</span><span class="sxs-lookup"><span data-stu-id="7471a-134">It is a string that includes a cmdlet-defined identifier, the name of the cmdlet class, and the source that reported the error.</span></span> <span data-ttu-id="7471a-135">Em geral, um registro de erro é análogo a um registro de evento de um log de eventos do Windows.</span><span class="sxs-lookup"><span data-stu-id="7471a-135">In general, an error record is analogous to an event record of a Windows Event log.</span></span> <span data-ttu-id="7471a-136">O FQID é análogo à seguinte tupla, que identifica a classe do registro de evento: (*nome do log*, *origem*, *ID do evento*).</span><span class="sxs-lookup"><span data-stu-id="7471a-136">The FQID is analogous to the following tuple, which identifies the class of the event record: (*log name*, *source*, *event ID*).</span></span>

<span data-ttu-id="7471a-137">O FQID foi projetado para ser inspecionado como uma única cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="7471a-137">The FQID is designed to be inspected as a single string.</span></span> <span data-ttu-id="7471a-138">No entanto, há casos em que o identificador de erro é projetado para ser analisado pelo aplicativo host.</span><span class="sxs-lookup"><span data-stu-id="7471a-138">However, cases exist in which the error identifier is designed to be parsed by the host application.</span></span> <span data-ttu-id="7471a-139">O exemplo a seguir é um identificador de erro totalmente qualificado bem formado.</span><span class="sxs-lookup"><span data-stu-id="7471a-139">The following example is a well-formed fully qualified error identifier.</span></span>

`CommandNotFoundException,Microsoft.PowerShell.Commands.GetCommandCommand.`

<span data-ttu-id="7471a-140">No exemplo anterior, o primeiro token é o identificador de erro, que é seguido pelo nome da classe de cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7471a-140">In the previous example, the first token is the error identifier, which is followed by the name of the cmdlet class.</span></span> <span data-ttu-id="7471a-141">O identificador de erro pode ser um único token ou pode ser um identificador separado por ponto que permite a ramificação na inspeção do identificador.</span><span class="sxs-lookup"><span data-stu-id="7471a-141">The error identifier can be a single token, or it can be a dot-separated identifier that allows for branching on inspection of the identifier.</span></span> <span data-ttu-id="7471a-142">Não use espaço em branco ou pontuação no identificador de erro.</span><span class="sxs-lookup"><span data-stu-id="7471a-142">Do not use white space or punctuation in the error identifier.</span></span> <span data-ttu-id="7471a-143">É especialmente importante não usar uma vírgula; uma vírgula é usada pelo Windows PowerShell para separar o identificador e o nome da classe do cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7471a-143">It is especially important not to use a comma; a comma is used by Windows PowerShell to separate the identifier and the cmdlet class name.</span></span>

### <a name="other-information"></a><span data-ttu-id="7471a-144">Outras informações</span><span class="sxs-lookup"><span data-stu-id="7471a-144">Other Information</span></span>

<span data-ttu-id="7471a-145">O objeto [System. Management. Automation. ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) também pode fornecer informações que descrevem o ambiente no qual o erro ocorreu.</span><span class="sxs-lookup"><span data-stu-id="7471a-145">The [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) object might also provide information that describes the environment in which the error occurred.</span></span> <span data-ttu-id="7471a-146">Essas informações incluem itens como detalhes do erro, informações de invocação e o objeto de destino que estava sendo processado quando o erro ocorreu.</span><span class="sxs-lookup"><span data-stu-id="7471a-146">This information includes items such as error details, invocation information, and the target object that was being processed when the error occurred.</span></span> <span data-ttu-id="7471a-147">Embora essas informações possam ser úteis para o aplicativo host, ela normalmente não é usada para identificar o erro.</span><span class="sxs-lookup"><span data-stu-id="7471a-147">Although this information might be useful to the host application, it is not typically used to identify the error.</span></span> <span data-ttu-id="7471a-148">Essas informações estão disponíveis por meio das seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="7471a-148">This information is available through the following properties:</span></span>

[<span data-ttu-id="7471a-149">System. Management. Automation. ErrorRecord. ErrorDetails</span><span class="sxs-lookup"><span data-stu-id="7471a-149">System.Management.Automation.ErrorRecord.ErrorDetails</span></span>](/dotnet/api/System.Management.Automation.ErrorRecord.ErrorDetails)

[<span data-ttu-id="7471a-150">System. Management. Automation. ErrorRecord. InvocationInfo</span><span class="sxs-lookup"><span data-stu-id="7471a-150">System.Management.Automation.ErrorRecord.InvocationInfo</span></span>](/dotnet/api/System.Management.Automation.ErrorRecord.InvocationInfo)

[<span data-ttu-id="7471a-151">System. Management. Automation. ErrorRecord. TargetObject</span><span class="sxs-lookup"><span data-stu-id="7471a-151">System.Management.Automation.ErrorRecord.TargetObject</span></span>](/dotnet/api/System.Management.Automation.ErrorRecord.TargetObject)

## <a name="see-also"></a><span data-ttu-id="7471a-152">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="7471a-152">See Also</span></span>

[<span data-ttu-id="7471a-153">System. Management. Automation. ErrorRecord</span><span class="sxs-lookup"><span data-stu-id="7471a-153">System.Management.Automation.ErrorRecord</span></span>](/dotnet/api/System.Management.Automation.ErrorRecord)

[<span data-ttu-id="7471a-154">System. Management. Automation. ErrorCategory</span><span class="sxs-lookup"><span data-stu-id="7471a-154">System.Management.Automation.Errorcategory</span></span>](/dotnet/api/System.Management.Automation.ErrorCategory)

[<span data-ttu-id="7471a-155">System. Management. Automation. Errorcategoryinfo</span><span class="sxs-lookup"><span data-stu-id="7471a-155">System.Management.Automation.Errorcategoryinfo</span></span>](/dotnet/api/System.Management.Automation.ErrorCategoryInfo)

[<span data-ttu-id="7471a-156">System. Management. Automation. cmdlet. WriteError</span><span class="sxs-lookup"><span data-stu-id="7471a-156">System.Management.Automation.Cmdlet.WriteError</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.WriteError)

[<span data-ttu-id="7471a-157">System. Management. Automation. cmdlet. ThrowTerminatingError \*</span><span class="sxs-lookup"><span data-stu-id="7471a-157">System.Management.Automation.Cmdlet.Throwterminatingerror\*</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError)

[<span data-ttu-id="7471a-158">Adicionando relatórios de erros não conclusivos ao seu cmdlet</span><span class="sxs-lookup"><span data-stu-id="7471a-158">Adding Non-Terminating Error Reporting to Your Cmdlet</span></span>](./adding-non-terminating-error-reporting-to-your-cmdlet.md)

[<span data-ttu-id="7471a-159">Relatório de erros do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="7471a-159">Windows PowerShell Error Reporting</span></span>](./error-reporting-concepts.md)

<span data-ttu-id="7471a-160">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md) (Escrevendo um Cmdlet do Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="7471a-160">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md)</span></span>