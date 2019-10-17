---
title: Registros de erro do Windows PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- error category [PowerShell SDK]
- error identifier [PowerShell SDK]
- error records [PowerShell SDK]
- error category string [PowerShell SDK]
ms.assetid: bdd66fea-eb63-4bb6-9cbe-9a799e5e0db5
caps.latest.revision: 9
ms.openlocfilehash: 5412d88b690a1f5f1ef387416e3bf9da3a32c95d
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72369105"
---
# <a name="windows-powershell-error-records"></a><span data-ttu-id="d96da-102">Registros de erros do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d96da-102">Windows PowerShell Error Records</span></span>

<span data-ttu-id="d96da-103">Os cmdlets devem passar um objeto [System. Management. Automation. ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) que identifica a condição de erro para erros de encerramento e de não finalização.</span><span class="sxs-lookup"><span data-stu-id="d96da-103">Cmdlets must pass an [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) object that identifies the error condition for terminating and non-terminating errors.</span></span>

<span data-ttu-id="d96da-104">O objeto [System. Management. Automation. ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) contém as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="d96da-104">The [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) object contains the following information:</span></span>

- <span data-ttu-id="d96da-105">A exceção que descreve o erro.</span><span class="sxs-lookup"><span data-stu-id="d96da-105">The exception that describes the error.</span></span> <span data-ttu-id="d96da-106">Geralmente, essa é uma exceção que o cmdlet capturou e converteu em um registro de erro.</span><span class="sxs-lookup"><span data-stu-id="d96da-106">Often, this is an exception that the cmdlet caught and converted into an error record.</span></span> <span data-ttu-id="d96da-107">Cada registro de erro deve conter uma exceção.</span><span class="sxs-lookup"><span data-stu-id="d96da-107">Every error record must contain an exception.</span></span>

<span data-ttu-id="d96da-108">Se o cmdlet não capturou uma exceção, ele deve criar uma nova exceção e escolher a classe de exceção que melhor descreve a condição de erro.</span><span class="sxs-lookup"><span data-stu-id="d96da-108">If the cmdlet did not catch an exception, it must create a new exception and choose the exception class that best describes the error condition.</span></span> <span data-ttu-id="d96da-109">No entanto, não é necessário lançar a exceção porque ela pode ser acessada por meio da propriedade [System. Management. Automation. ErrorRecord. Exception](/dotnet/api/System.Management.Automation.ErrorRecord.Exception) do objeto [System. Management. Automation. ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) .</span><span class="sxs-lookup"><span data-stu-id="d96da-109">However, you do not need to throw the exception because it can be accessed through the [System.Management.Automation.ErrorRecord.Exception](/dotnet/api/System.Management.Automation.ErrorRecord.Exception) property of the [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) object.</span></span>

- <span data-ttu-id="d96da-110">Um identificador de erro que fornece um designador de destino que pode ser usado para fins de diagnóstico e por scripts do Windows PowerShell para lidar com condições de erro específicas com manipuladores de erro específicos.</span><span class="sxs-lookup"><span data-stu-id="d96da-110">An error identifier that provides a targeted designator that can be used for diagnostic purposes and by Windows PowerShell scripts to handle specific error conditions with specific error handlers.</span></span> <span data-ttu-id="d96da-111">Cada registro de erro deve conter um identificador de erro (consulte o identificador de erro).</span><span class="sxs-lookup"><span data-stu-id="d96da-111">Every error record must contain an error identifier (see Error Identifier).</span></span>

- <span data-ttu-id="d96da-112">Uma categoria de erro que fornece um designador geral que pode ser usado para fins de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="d96da-112">An error category that provides a general designator that can be used for diagnostic purposes.</span></span> <span data-ttu-id="d96da-113">Cada registro de erro deve especificar uma categoria de erro (consulte a categoria de erro).</span><span class="sxs-lookup"><span data-stu-id="d96da-113">Every error record must specify an error category (see Error Category).</span></span>

- <span data-ttu-id="d96da-114">Uma mensagem de erro de substituição opcional e uma ação recomendada (consulte a mensagem de erro de substituição).</span><span class="sxs-lookup"><span data-stu-id="d96da-114">An optional replacement error message and a recommended action (see Replacement Error Message).</span></span>

- <span data-ttu-id="d96da-115">Informações de invocação opcionais sobre o cmdlet que gerou o erro.</span><span class="sxs-lookup"><span data-stu-id="d96da-115">Optional invocation information about the cmdlet that threw the error.</span></span> <span data-ttu-id="d96da-116">Essas informações são especificadas pelo Windows PowerShell (consulte mensagem de invocação).</span><span class="sxs-lookup"><span data-stu-id="d96da-116">This information is specified by Windows PowerShell (see Invocation Message).</span></span>

- <span data-ttu-id="d96da-117">O objeto de destino que estava sendo processado quando o erro ocorreu.</span><span class="sxs-lookup"><span data-stu-id="d96da-117">The target object that was being processed when the error occurred.</span></span> <span data-ttu-id="d96da-118">Esse pode ser o objeto de entrada ou pode ser outro objeto que o seu cmdlet estava processando.</span><span class="sxs-lookup"><span data-stu-id="d96da-118">This might be the input object, or it might be another object that your cmdlet was processing.</span></span> <span data-ttu-id="d96da-119">Por exemplo, para o comando `remove-item -recurse c:\somedirectory`, o erro pode ser uma instância de um objeto FileInfo para "c:\somedirectory\lockedfile".</span><span class="sxs-lookup"><span data-stu-id="d96da-119">For example, for the command `remove-item -recurse c:\somedirectory`, the error might be an instance of a FileInfo object for "c:\somedirectory\lockedfile".</span></span> <span data-ttu-id="d96da-120">As informações do objeto de destino são opcionais.</span><span class="sxs-lookup"><span data-stu-id="d96da-120">The target object information is optional.</span></span>

## <a name="error-identifier"></a><span data-ttu-id="d96da-121">Identificador de erro</span><span class="sxs-lookup"><span data-stu-id="d96da-121">Error Identifier</span></span>

<span data-ttu-id="d96da-122">Ao criar um registro de erro, especifique um identificador que designa a condição de erro dentro do seu cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d96da-122">When you create an error record, specify an identifier that designates the error condition within your cmdlet.</span></span> <span data-ttu-id="d96da-123">O Windows PowerShell combina o identificador de destino com o nome do seu cmdlet para criar um identificador de erro totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="d96da-123">Windows PowerShell combines the targeted identifier with the name of your cmdlet to create a fully qualified error identifier.</span></span> <span data-ttu-id="d96da-124">O identificador de erro totalmente qualificado pode ser acessado por meio da propriedade [System. Management. Automation. ErrorRecord. FullyQualifiedErrorId](/dotnet/api/System.Management.Automation.ErrorRecord.FullyQualifiedErrorId) do objeto [System. Management. Automation. ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) .</span><span class="sxs-lookup"><span data-stu-id="d96da-124">The fully qualified error identifier can be accessed through the [System.Management.Automation.ErrorRecord.FullyQualifiedErrorId](/dotnet/api/System.Management.Automation.ErrorRecord.FullyQualifiedErrorId) property of the [System.Management.Automation.ErrorRecord](/dotnet/api/System.Management.Automation.ErrorRecord) object.</span></span> <span data-ttu-id="d96da-125">O identificador de erro não está disponível por si só.</span><span class="sxs-lookup"><span data-stu-id="d96da-125">The error identifier is not available by itself.</span></span> <span data-ttu-id="d96da-126">Ele está disponível apenas como parte do identificador de erro totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="d96da-126">It is available only as part of the fully qualified error identifier.</span></span>

<span data-ttu-id="d96da-127">Use as diretrizes a seguir para gerar identificadores de erro ao criar registros de erro:</span><span class="sxs-lookup"><span data-stu-id="d96da-127">Use the following guidelines to generate error identifiers when you create error records:</span></span>

- <span data-ttu-id="d96da-128">Crie identificadores de erro específicos para uma condição de erro.</span><span class="sxs-lookup"><span data-stu-id="d96da-128">Make error identifiers specific to an error condition.</span></span> <span data-ttu-id="d96da-129">Direcione os identificadores de erro para fins de diagnóstico e para scripts que manipulam condições de erro específicas com manipuladores de erro específicos.</span><span class="sxs-lookup"><span data-stu-id="d96da-129">Target the error identifiers for diagnostic purposes and for scripts that handle specific error conditions with specific error handlers.</span></span> <span data-ttu-id="d96da-130">Um usuário deve ser capaz de usar o identificador de erro para identificar o erro e sua origem.</span><span class="sxs-lookup"><span data-stu-id="d96da-130">A user should be able to use the error identifier to identify the error and its source.</span></span> <span data-ttu-id="d96da-131">Os identificadores de erro também permitem a emissão de relatórios para condições de erro específicas de exceções existentes para que novas subclasses de exceção não sejam necessárias.</span><span class="sxs-lookup"><span data-stu-id="d96da-131">Error identifiers also enable reporting for specific error conditions from existing exceptions so that new exception subclasses are not required.</span></span>

- <span data-ttu-id="d96da-132">Em geral, atribua diferentes identificadores de erro a diferentes caminhos de código.</span><span class="sxs-lookup"><span data-stu-id="d96da-132">In general, assign different error identifiers to different code paths.</span></span> <span data-ttu-id="d96da-133">Os benefícios do usuário final de identificadores específicos.</span><span class="sxs-lookup"><span data-stu-id="d96da-133">The end-user benefits from specific identifiers.</span></span> <span data-ttu-id="d96da-134">Geralmente, cada caminho de código que chama [System. Management. Automation. cmdlet. WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) ou [System. Management. Automation. cmdlet. ThrowTerminatingError \*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) tem seu próprio identificador.</span><span class="sxs-lookup"><span data-stu-id="d96da-134">Often, each code path that calls [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) or [System.Management.Automation.Cmdlet.Throwterminatingerror\*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) has its own identifier.</span></span> <span data-ttu-id="d96da-135">Como regra, defina um novo identificador ao definir uma nova cadeia de caracteres de modelo para a mensagem de erro e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="d96da-135">As a rule, define a new identifier when you define a new template string for the error message, and vice-versa.</span></span> <span data-ttu-id="d96da-136">Não use a mensagem de erro como um identificador.</span><span class="sxs-lookup"><span data-stu-id="d96da-136">Do not use the error message as an identifier.</span></span>

- <span data-ttu-id="d96da-137">Quando você publica o código usando um identificador de erro específico, você estabelece a semântica de erros com esse identificador para o ciclo de vida completo do suporte ao produto.</span><span class="sxs-lookup"><span data-stu-id="d96da-137">When you publish code using a particular error identifier, you establish the semantics of errors with that identifier for your complete product support lifecycle.</span></span> <span data-ttu-id="d96da-138">Não reutilize-o em um contexto que seja semanticamente diferente do contexto original.</span><span class="sxs-lookup"><span data-stu-id="d96da-138">Do not reuse it in a context that is semantically different from the original context.</span></span> <span data-ttu-id="d96da-139">Se a semântica desse erro for alterada, crie e, em seguida, use um novo identificador.</span><span class="sxs-lookup"><span data-stu-id="d96da-139">If the semantics of this error change, create and then use a new identifier.</span></span>

- <span data-ttu-id="d96da-140">Em geral, você deve usar um determinado identificador de erro apenas para exceções de um determinado tipo CLR.</span><span class="sxs-lookup"><span data-stu-id="d96da-140">You should generally use a particular error identifier only for exceptions of a particular CLR type.</span></span> <span data-ttu-id="d96da-141">Se o tipo da exceção ou o tipo do objeto de destino for alterado, crie e use um novo identificador.</span><span class="sxs-lookup"><span data-stu-id="d96da-141">If the type of the exception or the type of the target object changes, create and then use a new identifier.</span></span>

- <span data-ttu-id="d96da-142">Escolha o texto para o identificador de erro que corresponde de forma concisa ao erro que você está relatando.</span><span class="sxs-lookup"><span data-stu-id="d96da-142">Choose text for your error identifier that concisely corresponds to the error that you are reporting.</span></span> <span data-ttu-id="d96da-143">Use as convenções padrão de .NET Framework de nomenclatura e de capitalização.</span><span class="sxs-lookup"><span data-stu-id="d96da-143">Use standard .NET Framework naming and capitalization conventions.</span></span> <span data-ttu-id="d96da-144">Não use espaço em branco ou pontuação.</span><span class="sxs-lookup"><span data-stu-id="d96da-144">Do not use white space or punctuation.</span></span> <span data-ttu-id="d96da-145">Não Localize identificadores de erro.</span><span class="sxs-lookup"><span data-stu-id="d96da-145">Do not localize error identifiers.</span></span>

- <span data-ttu-id="d96da-146">Não gere dinamicamente identificadores de erro de forma não reproduzível.</span><span class="sxs-lookup"><span data-stu-id="d96da-146">Do not dynamically generate error identifiers in a non-reproducible way.</span></span> <span data-ttu-id="d96da-147">Por exemplo, não incorpore informações de erro, como uma ID de processo.</span><span class="sxs-lookup"><span data-stu-id="d96da-147">For example, do not incorporate error information such as a process ID.</span></span> <span data-ttu-id="d96da-148">Os identificadores de erro são úteis apenas se corresponderem aos identificadores de erro vistos por outros usuários que estão enfrentando a mesma condição de erro.</span><span class="sxs-lookup"><span data-stu-id="d96da-148">Error identifiers are useful only if they correspond to the error identifiers seen by other users who are experiencing the same error condition.</span></span>

## <a name="error-category"></a><span data-ttu-id="d96da-149">Categoria do erro</span><span class="sxs-lookup"><span data-stu-id="d96da-149">Error Category</span></span>

<span data-ttu-id="d96da-150">Ao criar um registro de erro, especifique a categoria do erro usando uma das constantes definidas pela enumeração [System. Management. Automation. ErrorCategory](/dotnet/api/System.Management.Automation.ErrorCategory?view=pscore-6.2.0) .</span><span class="sxs-lookup"><span data-stu-id="d96da-150">When you create an error record, specify the category of the error using one of the constants defined by the [System.Management.Automation.ErrorCategory](/dotnet/api/System.Management.Automation.ErrorCategory?view=pscore-6.2.0) enumeration.</span></span> <span data-ttu-id="d96da-151">O Windows PowerShell usa a categoria de erro para exibir informações de erro quando os usuários definem a variável `$ErrorView` como `"CategoryView"`.</span><span class="sxs-lookup"><span data-stu-id="d96da-151">Windows PowerShell uses the error category to display error information when users set the `$ErrorView` variable to `"CategoryView"`.</span></span>

<span data-ttu-id="d96da-152">Evite usar a constante [System. Management. Automation. ErrorCategory](/dotnet/api/System.Management.Automation.ErrorCategory?view=pscore-6.2.0) **não especificada** .</span><span class="sxs-lookup"><span data-stu-id="d96da-152">Avoid using the [System.Management.Automation.ErrorCategory](/dotnet/api/System.Management.Automation.ErrorCategory?view=pscore-6.2.0) **NotSpecified** constant.</span></span> <span data-ttu-id="d96da-153">Se você tiver alguma informação sobre o erro ou sobre a operação que causou o erro, escolha a categoria que melhor descreve o erro ou a operação, mesmo que a categoria não seja uma correspondência perfeita.</span><span class="sxs-lookup"><span data-stu-id="d96da-153">If you have any information about the error or about the operation that caused the error, choose the category that best describes the error or the operation, even if the category is not a perfect match.</span></span>

<span data-ttu-id="d96da-154">As informações exibidas pelo Windows PowerShell são chamadas de cadeia de caracteres de exibição de categoria e são criadas a partir das propriedades da classe [System. Management. Automation. Errorcategoryinfo](/dotnet/api/System.Management.Automation.ErrorCategoryInfo) .</span><span class="sxs-lookup"><span data-stu-id="d96da-154">The information displayed by Windows PowerShell is referred to as the category-view string and is built from the properties of the [System.Management.Automation.Errorcategoryinfo](/dotnet/api/System.Management.Automation.ErrorCategoryInfo) class.</span></span> <span data-ttu-id="d96da-155">(Essa classe é acessada por meio da propriedade [System. Management. Automation. ErrorRecord. CategoryInfo](/dotnet/api/System.Management.Automation.ErrorRecord.CategoryInfo) de erro.)</span><span class="sxs-lookup"><span data-stu-id="d96da-155">(This class is accessed through the error [System.Management.Automation.ErrorRecord.CategoryInfo](/dotnet/api/System.Management.Automation.ErrorRecord.CategoryInfo) property.)</span></span>

```
{Category}: ({TargetName}:{TargetType}):[{Activity}], {Reason}
```

<span data-ttu-id="d96da-156">A lista a seguir descreve as informações exibidas:</span><span class="sxs-lookup"><span data-stu-id="d96da-156">The following list describes the information displayed:</span></span>

- <span data-ttu-id="d96da-157">Categoria: uma constante [System. Management. Automation. ErrorCategory](/dotnet/api/System.Management.Automation.ErrorCategory?view=pscore-6.2.0) definida pelo Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d96da-157">Category: A Windows PowerShell-defined [System.Management.Automation.ErrorCategory](/dotnet/api/System.Management.Automation.ErrorCategory?view=pscore-6.2.0) constant.</span></span>

- <span data-ttu-id="d96da-158">TargetName: por padrão, o nome do objeto que o cmdlet estava processando quando o erro ocorreu.</span><span class="sxs-lookup"><span data-stu-id="d96da-158">TargetName: By default, the name of the object the cmdlet was processing when the error occurred.</span></span> <span data-ttu-id="d96da-159">Ou outra cadeia de caracteres definida pelo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d96da-159">Or, another cmdlet-defined string.</span></span>

- <span data-ttu-id="d96da-160">TargetType: por padrão, o tipo do objeto de destino.</span><span class="sxs-lookup"><span data-stu-id="d96da-160">TargetType: By default, the type of the target object.</span></span> <span data-ttu-id="d96da-161">Ou outra cadeia de caracteres definida pelo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d96da-161">Or, another cmdlet-defined string.</span></span>

- <span data-ttu-id="d96da-162">Atividade: por padrão, o nome do cmdlet que criou o registro de erro.</span><span class="sxs-lookup"><span data-stu-id="d96da-162">Activity: By default, the name of the cmdlet that created the error record.</span></span> <span data-ttu-id="d96da-163">Ou qualquer outra cadeia de caracteres definida pelo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d96da-163">Or, some other cmdlet-defined string.</span></span>

- <span data-ttu-id="d96da-164">Motivo: por padrão, o tipo de exceção.</span><span class="sxs-lookup"><span data-stu-id="d96da-164">Reason: By default, the exception type.</span></span> <span data-ttu-id="d96da-165">Ou outra cadeia de caracteres definida pelo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d96da-165">Or, another cmdlet-defined string.</span></span>

## <a name="replacement-error-message"></a><span data-ttu-id="d96da-166">Mensagem de erro de substituição</span><span class="sxs-lookup"><span data-stu-id="d96da-166">Replacement Error Message</span></span>

<span data-ttu-id="d96da-167">Quando você desenvolve um registro de erro para um cmdlet, a mensagem de erro padrão do erro é proveniente do texto de mensagem padrão na propriedade [System. Exception. Message](/dotnet/api/System.Exception.Message) .</span><span class="sxs-lookup"><span data-stu-id="d96da-167">When you develop an error record for a cmdlet, the default error message for the error comes from the default message text in the [System.Exception.Message](/dotnet/api/System.Exception.Message) property.</span></span> <span data-ttu-id="d96da-168">Esta é uma propriedade somente leitura cujo texto de mensagem é destinado apenas para fins de depuração (de acordo com as diretrizes de .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="d96da-168">This is a read-only property whose message text is intended only for debugging purposes (according to the .NET Framework guidelines).</span></span> <span data-ttu-id="d96da-169">Recomendamos que você crie uma mensagem de erro que substitua ou aumente o texto da mensagem padrão.</span><span class="sxs-lookup"><span data-stu-id="d96da-169">We recommend that you create an error message that replaces or augments the default message text.</span></span> <span data-ttu-id="d96da-170">Torne a mensagem mais amigável e mais específica para o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d96da-170">Make the message more user-friendly and more specific to the cmdlet.</span></span>

<span data-ttu-id="d96da-171">A mensagem de substituição é fornecida por um objeto [System. Management. Automation. ErrorDetails](/dotnet/api/System.Management.Automation.ErrorDetails) .</span><span class="sxs-lookup"><span data-stu-id="d96da-171">The replacement message is provided by an [System.Management.Automation.ErrorDetails](/dotnet/api/System.Management.Automation.ErrorDetails) object.</span></span> <span data-ttu-id="d96da-172">Use um dos construtores a seguir deste objeto porque eles fornecem informações de localização adicionais que podem ser usadas pelo Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d96da-172">Use one of the following constructors of this object because they provide additional localization information that can be used by Windows PowerShell.</span></span>

- <span data-ttu-id="d96da-173">[ErrorDetails (cmdlet, Cadeia de caracteres, Cadeia de caracteres, objeto [])](/dotnet/api/system.management.automation.errordetails.-ctor?view=pscore-6.2.0#System_Management_Automation_ErrorDetails__ctor_System_Management_Automation_Cmdlet_System_String_System_String_System_Object___): Use esse construtor se a cadeia de caracteres do modelo for uma cadeia de caracteres de recurso no mesmo assembly no qual o cmdlet é implementado ou se você quiser carregar a cadeia de caracteres do modelo por meio de uma substituição do [ Método System. Management. Automation. cmdlet. GetResourceString](/dotnet/api/System.Management.Automation.Cmdlet.GetResourceString) .</span><span class="sxs-lookup"><span data-stu-id="d96da-173">[ErrorDetails(Cmdlet, String, String, Object[])](/dotnet/api/system.management.automation.errordetails.-ctor?view=pscore-6.2.0#System_Management_Automation_ErrorDetails__ctor_System_Management_Automation_Cmdlet_System_String_System_String_System_Object___): Use this constructor if your template string is a resource string in the same assembly in which the cmdlet is implemented or if you want to load the template string through an override of the  [System.Management.Automation.Cmdlet.GetResourceString](/dotnet/api/System.Management.Automation.Cmdlet.GetResourceString) method.</span></span>

- <span data-ttu-id="d96da-174">[ErrorDetails (assembly, String, String, Object [])](/dotnet/api/system.management.automation.errordetails.-ctor?view=pscore-6.2.0#System_Management_Automation_ErrorDetails__ctor_System_Reflection_Assembly_System_String_System_String_System_Object___): Use este construtor se a cadeia de caracteres do modelo estiver em outro assembly e você não carregá-lo por meio de uma substituição de [System. Management. Automation. cmdlet. GetResourceString](/dotnet/api/System.Management.Automation.Cmdlet.GetResourceString).</span><span class="sxs-lookup"><span data-stu-id="d96da-174">[ErrorDetails(Assembly, String, String, Object[])](/dotnet/api/system.management.automation.errordetails.-ctor?view=pscore-6.2.0#System_Management_Automation_ErrorDetails__ctor_System_Reflection_Assembly_System_String_System_String_System_Object___): Use this constructor if the template string is in another assembly and you do not load it through an override of [System.Management.Automation.Cmdlet.GetResourceString](/dotnet/api/System.Management.Automation.Cmdlet.GetResourceString).</span></span>

<span data-ttu-id="d96da-175">A mensagem de substituição deve estar em conformidade com as diretrizes de design de .NET Framework para gravar mensagens de exceção com uma pequena diferença.</span><span class="sxs-lookup"><span data-stu-id="d96da-175">The replacement message should conform to the .NET Framework design guidelines for writing exception messages with a small difference.</span></span> <span data-ttu-id="d96da-176">O estado das diretrizes que as mensagens de exceção devem ser gravadas para os desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="d96da-176">The guidelines state that exception messages should be written for developers.</span></span> <span data-ttu-id="d96da-177">Essas mensagens de substituição devem ser gravadas para o usuário do cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d96da-177">These replacement messages should be written for the cmdlet user.</span></span>

<span data-ttu-id="d96da-178">A mensagem de erro de substituição deve ser adicionada antes dos métodos [System. Management. Automation. cmdlet. WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) ou [System. Management. Automation. cmdlet. ThrowTerminatingError \*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) serem chamados.</span><span class="sxs-lookup"><span data-stu-id="d96da-178">The replacement error message must be added before the [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) or [System.Management.Automation.Cmdlet.Throwterminatingerror\*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) methods are called.</span></span> <span data-ttu-id="d96da-179">Para adicionar uma mensagem de substituição, defina a propriedade [System. Management. Automation. ErrorRecord. ErrorDetails](/dotnet/api/System.Management.Automation.ErrorRecord.ErrorDetails) do registro de erros.</span><span class="sxs-lookup"><span data-stu-id="d96da-179">To add a replacement message, set the [System.Management.Automation.ErrorRecord.ErrorDetails](/dotnet/api/System.Management.Automation.ErrorRecord.ErrorDetails) property of the error record.</span></span> <span data-ttu-id="d96da-180">Quando essa propriedade é definida, o Windows PowerShell exibe a propriedade [System. Management. Automation. ErrorDetails. Message \*](/dotnet/api/System.Management.Automation.ErrorDetails.Message) em vez do texto da mensagem padrão.</span><span class="sxs-lookup"><span data-stu-id="d96da-180">When this property is set, Windows PowerShell displays the [System.Management.Automation.ErrorDetails.Message\*](/dotnet/api/System.Management.Automation.ErrorDetails.Message) property instead of the default message text.</span></span>

## <a name="recommended-action-information"></a><span data-ttu-id="d96da-181">Informações de ação recomendadas</span><span class="sxs-lookup"><span data-stu-id="d96da-181">Recommended Action Information</span></span>

<span data-ttu-id="d96da-182">O objeto [System. Management. Automation. ErrorDetails](/dotnet/api/System.Management.Automation.ErrorDetails) também pode fornecer informações sobre quais ações são recomendadas quando o erro ocorre.</span><span class="sxs-lookup"><span data-stu-id="d96da-182">The [System.Management.Automation.ErrorDetails](/dotnet/api/System.Management.Automation.ErrorDetails) object can also provide information about what actions are recommended when the error occurs.</span></span>

## <a name="invocation-information"></a><span data-ttu-id="d96da-183">Informações de invocação</span><span class="sxs-lookup"><span data-stu-id="d96da-183">Invocation information</span></span>

<span data-ttu-id="d96da-184">Quando um cmdlet usa [System. Management. Automation. cmdlet. WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) ou [System. Management. Automation. cmdlet. ThrowTerminatingError \*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) para relatar um registro de erro, o Windows PowerShell adiciona automaticamente informações que descrevem o comando que foi invocado quando o erro ocorreu.</span><span class="sxs-lookup"><span data-stu-id="d96da-184">When a cmdlet uses [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) or [System.Management.Automation.Cmdlet.Throwterminatingerror\*](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError) to report an error record, Windows PowerShell automatically adds information that describes the command that was invoked when the error occurred.</span></span> <span data-ttu-id="d96da-185">Essas informações são fornecidas por um objeto [System. Management. Automation. InvocationInfo](/dotnet/api/System.Management.Automation.InvocationInfo) que contém o nome do cmdlet que foi invocado pelo comando, o próprio comando e as informações sobre o pipeline ou script.</span><span class="sxs-lookup"><span data-stu-id="d96da-185">This information is provided by a [System.Management.Automation.Invocationinfo](/dotnet/api/System.Management.Automation.InvocationInfo) object that contains the name of the cmdlet that was invoked by the command, the command itself, and information about the pipeline or script.</span></span> <span data-ttu-id="d96da-186">Esta propriedade é somente leitura.</span><span class="sxs-lookup"><span data-stu-id="d96da-186">This property is read-only.</span></span>

## <a name="see-also"></a><span data-ttu-id="d96da-187">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="d96da-187">See Also</span></span>

[<span data-ttu-id="d96da-188">System. Management. Automation. cmdlet. WriteError</span><span class="sxs-lookup"><span data-stu-id="d96da-188">System.Management.Automation.Cmdlet.WriteError</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.WriteError)

[<span data-ttu-id="d96da-189">System. Management. Automation. cmdlet. ThrowTerminatingError \*</span><span class="sxs-lookup"><span data-stu-id="d96da-189">System.Management.Automation.Cmdlet.Throwterminatingerror\*</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.ThrowTerminatingError)

[<span data-ttu-id="d96da-190">System. Management. Automation. ErrorCategory</span><span class="sxs-lookup"><span data-stu-id="d96da-190">System.Management.Automation.ErrorCategory</span></span>](/dotnet/api/System.Management.Automation.ErrorCategory?view=pscore-6.2.0)

[<span data-ttu-id="d96da-191">System. Management. Automation. Errorcategoryinfo</span><span class="sxs-lookup"><span data-stu-id="d96da-191">System.Management.Automation.Errorcategoryinfo</span></span>](/dotnet/api/System.Management.Automation.ErrorCategoryInfo)

[<span data-ttu-id="d96da-192">System. Management. Automation. ErrorRecord</span><span class="sxs-lookup"><span data-stu-id="d96da-192">System.Management.Automation.ErrorRecord</span></span>](/dotnet/api/System.Management.Automation.ErrorRecord)

[<span data-ttu-id="d96da-193">System. Management. Automation. ErrorDetails</span><span class="sxs-lookup"><span data-stu-id="d96da-193">System.Management.Automation.ErrorDetails</span></span>](/dotnet/api/System.Management.Automation.ErrorDetails)

[<span data-ttu-id="d96da-194">System. Management. Automation. InvocationInfo</span><span class="sxs-lookup"><span data-stu-id="d96da-194">System.Management.Automation.Invocationinfo</span></span>](/dotnet/api/System.Management.Automation.InvocationInfo)

[<span data-ttu-id="d96da-195">Relatório de erros do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d96da-195">Windows PowerShell Error Reporting</span></span>](./error-reporting-concepts.md)

<span data-ttu-id="d96da-196">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md) (Escrevendo um Cmdlet do Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="d96da-196">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md)</span></span>