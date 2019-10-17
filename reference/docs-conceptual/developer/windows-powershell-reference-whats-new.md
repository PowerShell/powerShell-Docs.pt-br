---
title: Referência do Windows PowerShell-novidades
ms.date: 09/13/2016
ms.topic: article
ms.openlocfilehash: 364d081ddf2f87ceeaa47732266a35f4a126246f
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72366085"
---
# <a name="whats-new"></a><span data-ttu-id="58273-102">Novidades</span><span class="sxs-lookup"><span data-stu-id="58273-102">What's New</span></span>

<span data-ttu-id="58273-103">O Windows PowerShell 2,0 fornece os novos recursos a seguir para uso na criação de cmdlets, provedores e aplicativos de host.</span><span class="sxs-lookup"><span data-stu-id="58273-103">Windows PowerShell 2.0 provides the following new features for use when writing cmdlets, providers, and host applications.</span></span>

## <a name="modules"></a><span data-ttu-id="58273-104">Módulos</span><span class="sxs-lookup"><span data-stu-id="58273-104">Modules</span></span>

<span data-ttu-id="58273-105">Agora você pode empacotar e distribuir soluções do Windows PowerShell usando módulos.</span><span class="sxs-lookup"><span data-stu-id="58273-105">You can now package and distribute Windows PowerShell solutions by using modules.</span></span> <span data-ttu-id="58273-106">Os módulos permitem particionar, organizar e abstrair o código do Windows PowerShell em unidades independentes e reutilizáveis.</span><span class="sxs-lookup"><span data-stu-id="58273-106">Modules allow you to partition, organize, and abstract your Windows PowerShell code into self-contained, reusable units.</span></span> <span data-ttu-id="58273-107">Para obter mais informações sobre módulos, consulte escrevendo um módulo do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="58273-107">For more information about modules, see Writing a Windows PowerShell Module.</span></span>

## <a name="the-powershell-class"></a><span data-ttu-id="58273-108">A classe do PowerShell</span><span class="sxs-lookup"><span data-stu-id="58273-108">The PowerShell class</span></span>

<span data-ttu-id="58273-109">A classe PowerShell fornece uma solução mais simples para a criação de aplicativos, conhecidos como aplicativos host, que executam comandos programaticamente.</span><span class="sxs-lookup"><span data-stu-id="58273-109">The PowerShell class provides a simpler solution for creating applications, referred to as host applications, that programmatically run commands.</span></span> <span data-ttu-id="58273-110">Essa classe permite que você crie um pipeline de comandos, especifique o runspace que é usado para executar os comandos e especifique a invocação de comandos de forma síncrona ou assíncrona.</span><span class="sxs-lookup"><span data-stu-id="58273-110">This class allows you to create a pipeline of commands, specify the runspace that is used to run the commands, and specify invoking the commands synchronously or asynchronously.</span></span>

## <a name="the-runspacepool-class"></a><span data-ttu-id="58273-111">A classe RunspacePool</span><span class="sxs-lookup"><span data-stu-id="58273-111">The RunspacePool class</span></span>

<span data-ttu-id="58273-112">Pools de runspace permitem que você crie vários Runspaces usando uma única chamada.</span><span class="sxs-lookup"><span data-stu-id="58273-112">Runspace pools allow you to create multiple runspaces by using a single call.</span></span> <span data-ttu-id="58273-113">O método CreateRunspacePool fornece várias sobrecargas que podem ser usadas para criar Runspaces que têm os mesmos recursos, como o mesmo host, estado de sessão inicial e informações de conexão.</span><span class="sxs-lookup"><span data-stu-id="58273-113">The CreateRunspacePool method provides several overloads that can be used to create runspaces that have the same features, such as the same host, initial session state, and connection information.</span></span>

## <a name="the-initialsessionstate-class"></a><span data-ttu-id="58273-114">A classe InitialSessionState</span><span class="sxs-lookup"><span data-stu-id="58273-114">The InitialSessionState class</span></span>

<span data-ttu-id="58273-115">A classe InitialSessionState permite que você crie uma configuração de estado de sessão que é usada quando um runspace é aberto.</span><span class="sxs-lookup"><span data-stu-id="58273-115">The InitialSessionState class allows you to create a session state configuration that is used when a runspace is opened.</span></span> <span data-ttu-id="58273-116">Você pode criar uma configuração personalizada, uma configuração padrão que inclui os comandos fornecidos pelo mshshort e uma configuração cujos comandos são restritos com base nos recursos da sessão.</span><span class="sxs-lookup"><span data-stu-id="58273-116">You can create a custom configuration, a default configuration that includes the commands provided by mshshort, and a configuration whose commands are restricted based on the capabilities of the session.</span></span>

## <a name="remote-runspaces"></a><span data-ttu-id="58273-117">Runspaces remotos</span><span class="sxs-lookup"><span data-stu-id="58273-117">Remote runspaces</span></span>

<span data-ttu-id="58273-118">Agora você pode criar espaços de execução que podem ser abertos em computadores remotos, permitindo que você execute comandos no computador remoto e colete os resultados localmente.</span><span class="sxs-lookup"><span data-stu-id="58273-118">You can now create runspaces that can be opened on remote computers, allowing you to run commands on the remote machine and collect the results locally.</span></span> <span data-ttu-id="58273-119">Para criar um runspace remoto, você deve especificar informações sobre a conexão remota ao criar o runspace.</span><span class="sxs-lookup"><span data-stu-id="58273-119">To create a remote runspace, you must specify information about the remote connection when creating the runspace.</span></span> <span data-ttu-id="58273-120">Consulte os métodos CreateRunspace e CreateRunspacePool para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="58273-120">See the CreateRunspace and CreateRunspacePool methods for examples.</span></span> <span data-ttu-id="58273-121">As informações de conexão são definidas pela classe RunspaceConnectionInfo.</span><span class="sxs-lookup"><span data-stu-id="58273-121">The connection information is defined by the RunspaceConnectionInfo class.</span></span>

## <a name="private-runspace-elements"></a><span data-ttu-id="58273-122">Elementos de runspace privado</span><span class="sxs-lookup"><span data-stu-id="58273-122">Private runspace elements</span></span>

<span data-ttu-id="58273-123">Agora você pode criar Runspaces cujos elementos são públicos ou privados.</span><span class="sxs-lookup"><span data-stu-id="58273-123">You can now create runspaces whose elements are public or private.</span></span> <span data-ttu-id="58273-124">Isso permite que você crie Runspaces cujos elementos estão disponíveis para o runspace, mas que não estão disponíveis para o usuário.</span><span class="sxs-lookup"><span data-stu-id="58273-124">This allows you to create runspaces whose elements are available to the runspace, but are not available to the user.</span></span> <span data-ttu-id="58273-125">Consulte a classe ConstrainedSessionStateEntry para descobrir quais elementos do runspace podem se tornar particulares.</span><span class="sxs-lookup"><span data-stu-id="58273-125">See the ConstrainedSessionStateEntry class to find out which elements of the runspace can be made private.</span></span>

## <a name="runspace-threading-modes-and-apartment-state"></a><span data-ttu-id="58273-126">Modos de threading de runspace e estado de apartamento</span><span class="sxs-lookup"><span data-stu-id="58273-126">Runspace threading modes and apartment state</span></span>

<span data-ttu-id="58273-127">Agora você pode especificar como os threads são criados e usados ao executar comandos em um runspace.</span><span class="sxs-lookup"><span data-stu-id="58273-127">You can now specify how threads are created and used when running commands in a runspace.</span></span> <span data-ttu-id="58273-128">Consulte as propriedades System. Management. Automation. Runspaces. runspace. ThreadOptions e System. Management. Automation. Runspaces. RunspacePool. ThreadOptions.</span><span class="sxs-lookup"><span data-stu-id="58273-128">See the System.Management.Automation.Runspaces.Runspace.ThreadOptions and System.Management.Automation.Runspaces.RunspacePool.ThreadOptions properties.</span></span>

<span data-ttu-id="58273-129">Agora você pode obter o estado de apartamento dos threads que são usados para executar comandos em um runspace.</span><span class="sxs-lookup"><span data-stu-id="58273-129">You can now get the apartment state of the threads that are used to run commands in a runspace.</span></span> <span data-ttu-id="58273-130">Consulte as propriedades System. Management. Automation. Runspaces. runspace. seja ApartmentState e System. Management. Automation. Runspaces. RunspacePool. seja ApartmentState.</span><span class="sxs-lookup"><span data-stu-id="58273-130">See the System.Management.Automation.Runspaces.Runspace.ApartmentState and System.Management.Automation.Runspaces.RunspacePool.ApartmentState properties.</span></span>

## <a name="transaction-cmdlets"></a><span data-ttu-id="58273-131">Cmdlets de transação</span><span class="sxs-lookup"><span data-stu-id="58273-131">Transaction cmdlets</span></span>

<span data-ttu-id="58273-132">Agora você pode criar cmdlets que podem ser usados em uma transação.</span><span class="sxs-lookup"><span data-stu-id="58273-132">You can now create cmdlets that can be used within a transaction.</span></span> <span data-ttu-id="58273-133">Quando um cmdlet é usado em uma transação, suas ações são temporárias e podem ser aceitas ou rejeitadas pelos cmdlets de transação fornecidos pelo Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="58273-133">When a cmdlet is used in a transaction, its actions are temporary, and they can be accepted or rejected by the transaction cmdlets provided by Windows PowerShell.</span></span>

<span data-ttu-id="58273-134">Para obter mais informações sobre transações, consulte como dar suporte a transações.</span><span class="sxs-lookup"><span data-stu-id="58273-134">For more information about transactions, see How to Support Transactions.</span></span>

## <a name="transaction-provider"></a><span data-ttu-id="58273-135">Provedor de transações</span><span class="sxs-lookup"><span data-stu-id="58273-135">Transaction provider</span></span>

<span data-ttu-id="58273-136">Agora você pode criar provedores que podem ser usados em uma transação.</span><span class="sxs-lookup"><span data-stu-id="58273-136">You can now create providers that can be used within a transaction.</span></span> <span data-ttu-id="58273-137">Semelhante aos cmdlets, quando um provedor é usado em uma transação, suas ações são temporárias e podem ser aceitas ou rejeitadas pelos cmdlets de transação fornecidos pelo Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="58273-137">Similar to cmdlets, when a provider is used in a transaction, its actions are temporary, and they can be accepted or rejected by the transaction cmdlets provided by Windows PowerShell.</span></span>

<span data-ttu-id="58273-138">Para obter mais informações sobre como especificar o suporte para a transação em uma classe de provedor, consulte a propriedade System. Management. Automation. Provider. CmdletProviderAttribute. ProviderCapabilities.</span><span class="sxs-lookup"><span data-stu-id="58273-138">For more information about specifying support for transaction within a provider class, see the System.Management.Automation.Provider.CmdletProviderAttribute.ProviderCapabilities property.</span></span>

## <a name="job-cmdlets"></a><span data-ttu-id="58273-139">Cmdlets de trabalho</span><span class="sxs-lookup"><span data-stu-id="58273-139">Job cmdlets</span></span>

<span data-ttu-id="58273-140">Agora você pode escrever cmdlets que podem executar sua ação como um trabalho.</span><span class="sxs-lookup"><span data-stu-id="58273-140">You can now write cmdlets that can perform their action as a job.</span></span> <span data-ttu-id="58273-141">Esses trabalhos são executados em segundo plano sem interagir com a sessão atual.</span><span class="sxs-lookup"><span data-stu-id="58273-141">These jobs are run in the background without interacting with the current session.</span></span> <span data-ttu-id="58273-142">Para obter mais informações sobre como o Windows PowerShell dá suporte a trabalhos, consulte trabalhos em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="58273-142">For more information about how Windows PowerShell supports jobs, see Background Jobs.</span></span>

## <a name="cmdlet-output-types"></a><span data-ttu-id="58273-143">Tipos de saída de cmdlet</span><span class="sxs-lookup"><span data-stu-id="58273-143">Cmdlet output types</span></span>

<span data-ttu-id="58273-144">Agora você pode especificar os tipos de .NET Framework que são retornados pelos cmdlets declarando o atributo OutputType ao escrever seus cmdlets.</span><span class="sxs-lookup"><span data-stu-id="58273-144">You can now specify the .NET Framework types that are returned by your cmdlets by declaring the OutputType attribute when writing your cmdlets.</span></span> <span data-ttu-id="58273-145">Isso permitirá que outras pessoas determinem quais tipos de objetos são retornados por um cmdlet examinando a Propriedade OutputType do cmdlet.</span><span class="sxs-lookup"><span data-stu-id="58273-145">This will allow others to determine what type of objects are returned by a cmdlet by looking at the OutputType property of the cmdlet.</span></span>

## <a name="event-support"></a><span data-ttu-id="58273-146">Suporte a eventos</span><span class="sxs-lookup"><span data-stu-id="58273-146">Event support</span></span>

<span data-ttu-id="58273-147">Agora você pode escrever cmdlets que adicionam e consomem eventos.</span><span class="sxs-lookup"><span data-stu-id="58273-147">You can now write cmdlets that add and consume events.</span></span> <span data-ttu-id="58273-148">Consulte a classe PSEvent.</span><span class="sxs-lookup"><span data-stu-id="58273-148">See the PSEvent class.</span></span>

## <a name="proxy-commands"></a><span data-ttu-id="58273-149">Comandos de proxy</span><span class="sxs-lookup"><span data-stu-id="58273-149">Proxy commands</span></span>

<span data-ttu-id="58273-150">Agora você pode escrever comandos de proxy que podem ser usados para executar outro comando.</span><span class="sxs-lookup"><span data-stu-id="58273-150">You can now write proxy commands that can be used to run another command.</span></span> <span data-ttu-id="58273-151">Um comando proxy permite que você controle qual funcionalidade do cmdlet de origem está disponível para o usuário.</span><span class="sxs-lookup"><span data-stu-id="58273-151">A proxy command allows you to control what functionality of the source cmdlet is available to the user.</span></span> <span data-ttu-id="58273-152">Por exemplo, você pode criar um comando de proxy que remove um parâmetro fornecido pelo comando de origem.</span><span class="sxs-lookup"><span data-stu-id="58273-152">For example, you can create a proxy command that removes a parameter that is supplied by the source command.</span></span> <span data-ttu-id="58273-153">Consulte a classe ProxyCommand.</span><span class="sxs-lookup"><span data-stu-id="58273-153">See the ProxyCommand class.</span></span>

## <a name="multiple-choice-prompts"></a><span data-ttu-id="58273-154">Prompts com várias opções</span><span class="sxs-lookup"><span data-stu-id="58273-154">Multiple choice prompts</span></span>

<span data-ttu-id="58273-155">Agora você pode escrever aplicativos que podem fornecer prompts que permitem ao usuário selecionar várias opções.</span><span class="sxs-lookup"><span data-stu-id="58273-155">You can now write applications that can provide prompts that allow the user to select multiple choices.</span></span> <span data-ttu-id="58273-156">Consulte a interface IHostUISupportsMultipleChoiceSelection</span><span class="sxs-lookup"><span data-stu-id="58273-156">See the IHostUISupportsMultipleChoiceSelection interface</span></span>

## <a name="interactive-sessions"></a><span data-ttu-id="58273-157">Sessões interativas</span><span class="sxs-lookup"><span data-stu-id="58273-157">Interactive sessions</span></span>

<span data-ttu-id="58273-158">Agora você pode escrever aplicativos que podem iniciar e parar uma sessão interativa em um computador remoto.</span><span class="sxs-lookup"><span data-stu-id="58273-158">You can now write applications that can start and stop an interactive session on a remote computer.</span></span>
<span data-ttu-id="58273-159">Consulte a interface IHostSupportsInteractiveSession.</span><span class="sxs-lookup"><span data-stu-id="58273-159">See the IHostSupportsInteractiveSession interface.</span></span>

## <a name="custom-cmdlet-help-for-providers"></a><span data-ttu-id="58273-160">Ajuda de cmdlet personalizado para provedores</span><span class="sxs-lookup"><span data-stu-id="58273-160">Custom Cmdlet Help for Providers</span></span>

<span data-ttu-id="58273-161">Agora você pode criar tópicos de ajuda personalizados para os cmdlets do provedor.</span><span class="sxs-lookup"><span data-stu-id="58273-161">You can now create customized Help topics for the provider cmdlets.</span></span> <span data-ttu-id="58273-162">Tópicos de ajuda de cmdlets personalizados podem explicar como o cmdlet funciona no caminho do provedor e recursos especiais de documento, incluindo os parâmetros dinâmicos que o provedor adiciona ao cmdlet.</span><span class="sxs-lookup"><span data-stu-id="58273-162">Custom cmdlet help topics can explain how the cmdlet works in the provider path and document special features, including the dynamic parameters that the provider adds to the cmdlet.</span></span>