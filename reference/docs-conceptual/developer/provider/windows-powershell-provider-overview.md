---
title: Visão geral do provedor do Windows PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 82244fbd-07b9-47f3-805c-3fb90ebbf58a
caps.latest.revision: 13
ms.openlocfilehash: 81f6c8cd75ccea9e711cd8f6d6daa6cca5a499a0
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72366285"
---
# <a name="windows-powershell-provider-overview"></a><span data-ttu-id="41992-102">Visão geral do provedor do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="41992-102">Windows PowerShell Provider Overview</span></span>

<span data-ttu-id="41992-103">Um provedor do Windows PowerShell permite que qualquer armazenamento de dados seja exposto como um sistema de arquivos como se fosse uma unidade montada.</span><span class="sxs-lookup"><span data-stu-id="41992-103">A Windows PowerShell provider allows any data store to be exposed like a file system as if it were a mounted drive.</span></span> <span data-ttu-id="41992-104">Por exemplo, o provedor de registro interno permite que você navegue no registro como você navegaria na unidade `c` do seu computador.</span><span class="sxs-lookup"><span data-stu-id="41992-104">For example, the built-in Registry provider allows you to navigate the registry like you would navigate the `c` drive of your computer.</span></span> <span data-ttu-id="41992-105">Um provedor também pode substituir os cmdlets `Item` (por exemplo, `Get-Item`, `Set-Item`, etc.) de modo que os dados em seu armazenamento de dados possam ser tratados como arquivos e diretórios são tratados ao navegar em um sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="41992-105">A provider can also override the `Item` cmdlets (for example, `Get-Item`, `Set-Item`, etc.) such that the data in your data store can be treated like files and directories are treated when navigating a file system.</span></span> <span data-ttu-id="41992-106">Para obter mais informações sobre provedores e unidades e os provedores internos do Windows PowerShell, consulte [about_Providers](/powershell/module/microsoft.powershell.core/about/about_providers).</span><span class="sxs-lookup"><span data-stu-id="41992-106">For more information about providers and drives, and the built-in providers in  Windows PowerShell, see [about_Providers](/powershell/module/microsoft.powershell.core/about/about_providers).</span></span>

## <a name="providers-and-drives"></a><span data-ttu-id="41992-107">Provedores e unidades</span><span class="sxs-lookup"><span data-stu-id="41992-107">Providers and Drives</span></span>

<span data-ttu-id="41992-108">Um provedor define a lógica que é usada para acessar, navegar e editar um armazenamento de dados, enquanto uma unidade especifica um ponto de entrada específico para um armazenamento de dados (ou uma parte de um armazenamento de dados) que é do tipo definido pelo provedor.</span><span class="sxs-lookup"><span data-stu-id="41992-108">A Provider defines the logic that is used to access, navigate, and edit a data store, while a drive specifies a specific entry point to a data store (or a portion of a data store) that is of the type defined by the provider.</span></span> <span data-ttu-id="41992-109">Por exemplo, o provedor de registro permite que você acesse Hives e chaves em um registro, e as unidades HKLM e HKCU especificam os hives correspondentes no registro.</span><span class="sxs-lookup"><span data-stu-id="41992-109">For example, the Registry provider allows you to access hives and keys in a registry, and the HKLM and HKCU drives specify the corresponding hives within the registry.</span></span> <span data-ttu-id="41992-110">As unidades HKLM e HKCU usam o provedor de registro.</span><span class="sxs-lookup"><span data-stu-id="41992-110">The HKLM and HKCU drives both use the Registry provider.</span></span>

<span data-ttu-id="41992-111">Ao escrever um provedor, você pode especificar unidades-unidades padrão que são criadas automaticamente quando o provedor está disponível.</span><span class="sxs-lookup"><span data-stu-id="41992-111">When you write a provider, you can specify default drives-drives that are created automatically when the provider is available.</span></span> <span data-ttu-id="41992-112">Você também define um método para criar novas unidades que usam esse provedor.</span><span class="sxs-lookup"><span data-stu-id="41992-112">You also define a method to create new drives that use that provider.</span></span>

## <a name="type-of-providers"></a><span data-ttu-id="41992-113">Tipo de provedores</span><span class="sxs-lookup"><span data-stu-id="41992-113">Type of Providers</span></span>

<span data-ttu-id="41992-114">Há vários tipos de provedores, cada um dos quais fornece um nível diferente de funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="41992-114">There are several types of providers, each of which provides a different level of functionality.</span></span> <span data-ttu-id="41992-115">Um provedor é implementado como uma classe que deriva de um dos descendentes da classe [System. Management. Automation. SessionStateCategory](/dotnet/api/system.management.automation.sessionstatecategory?view=pscore-6.2.0) do **cmdletprovider** .</span><span class="sxs-lookup"><span data-stu-id="41992-115">A provider is implemented as a class that derives from one of the descendants of the [System.Management.Automation.SessionStateCategory](/dotnet/api/system.management.automation.sessionstatecategory?view=pscore-6.2.0) **CmdletProvider** class.</span></span> <span data-ttu-id="41992-116">Para obter informações sobre os diferentes tipos de provedores, consulte [tipos de provedor](./provider-types.md).</span><span class="sxs-lookup"><span data-stu-id="41992-116">For information about the different types of providers, see [Provider types](./provider-types.md).</span></span>

## <a name="provider-cmdlets"></a><span data-ttu-id="41992-117">Cmdlets do provedor</span><span class="sxs-lookup"><span data-stu-id="41992-117">Provider cmdlets</span></span>

<span data-ttu-id="41992-118">Os provedores podem implementar métodos que correspondam aos cmdlets, criando comportamentos personalizados para esses cmdlets quando usados em uma unidade para esse provedor.</span><span class="sxs-lookup"><span data-stu-id="41992-118">Providers can implement methods that correspond to cmdlets, creating custom behaviors for those cmdlets when used in a drive for that provider.</span></span> <span data-ttu-id="41992-119">Dependendo do tipo de provedor, diferentes conjuntos de cmdlets estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="41992-119">Depending on the type of provider, different sets of cmdlets are available.</span></span> <span data-ttu-id="41992-120">Para obter uma lista completa dos cmdlets disponíveis para personalização em provedores, consulte [cmdlets do provedor](./provider-cmdlets.md).</span><span class="sxs-lookup"><span data-stu-id="41992-120">For a complete list of the cmdlets available for customization in providers, see [Provider cmdlets](./provider-cmdlets.md).</span></span>

## <a name="provider-paths"></a><span data-ttu-id="41992-121">Caminhos de provedor</span><span class="sxs-lookup"><span data-stu-id="41992-121">Provider paths</span></span>

<span data-ttu-id="41992-122">Os usuários navegam por unidades de provedor como sistemas de arquivos.</span><span class="sxs-lookup"><span data-stu-id="41992-122">Users navigate provider drives like file systems.</span></span> <span data-ttu-id="41992-123">Por isso, eles esperam que a sintaxe dos caminhos corresponda aos caminhos usados na navegação do sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="41992-123">Because of this, they expect the syntax of paths to correspond to the paths used in file system navigation.</span></span> <span data-ttu-id="41992-124">Quando um usuário executa um cmdlet de provedor, ele especifica um caminho para o item a ser acessado.</span><span class="sxs-lookup"><span data-stu-id="41992-124">When a user runs a provider cmdlet, they specify a path to the item to be accessed.</span></span> <span data-ttu-id="41992-125">O caminho especificado pode ser interpretado de várias maneiras.</span><span class="sxs-lookup"><span data-stu-id="41992-125">The path that is specified can be interpreted in several ways.</span></span> <span data-ttu-id="41992-126">Um provedor deve dar suporte a um ou mais dos seguintes tipos de caminho.</span><span class="sxs-lookup"><span data-stu-id="41992-126">A provider should support one or more of the following path types.</span></span>

### <a name="drive-qualified-paths"></a><span data-ttu-id="41992-127">Caminhos qualificados para a unidade</span><span class="sxs-lookup"><span data-stu-id="41992-127">Drive-qualified paths</span></span>

<span data-ttu-id="41992-128">Um caminho qualificado para unidade é uma combinação do nome do item, o contêiner e os sub-recipientes nos quais o item está localizado e a unidade do Windows PowerShell por meio da qual o item é acessado.</span><span class="sxs-lookup"><span data-stu-id="41992-128">A drive-qualified path is a combination of the item name, the container and subcontainers in which the item is located, and the Windows PowerShell drive through which the item is accessed.</span></span> <span data-ttu-id="41992-129">(As unidades são definidas pelo provedor que é usado para acessar o armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="41992-129">(Drives are defined by the provider that is used to access the data store.</span></span> <span data-ttu-id="41992-130">Esse caminho começa com o nome da unidade seguido por dois-pontos (:).</span><span class="sxs-lookup"><span data-stu-id="41992-130">This path starts with the drive name followed by a colon (:).</span></span> <span data-ttu-id="41992-131">Por exemplo: `get-childitem C:`</span><span class="sxs-lookup"><span data-stu-id="41992-131">For example: `get-childitem C:`</span></span>

### <a name="provider-qualified-paths"></a><span data-ttu-id="41992-132">Caminhos qualificados para o provedor</span><span class="sxs-lookup"><span data-stu-id="41992-132">Provider-qualified paths</span></span>

<span data-ttu-id="41992-133">Para permitir que o mecanismo do Windows PowerShell inicialize e desinicialize seu provedor, o provedor deve dar suporte a um caminho qualificado para provedor.</span><span class="sxs-lookup"><span data-stu-id="41992-133">To allow the Windows PowerShell engine to initialize and uninitialize your provider, the provider must support a provider-qualified path.</span></span> <span data-ttu-id="41992-134">Por exemplo, o usuário pode inicializar e cancelar a inicialização do provedor FileSystem porque ele define o seguinte caminho qualificado para provedor: `FileSystem::\\uncshare\abc\bar`.</span><span class="sxs-lookup"><span data-stu-id="41992-134">For example, the user can initialize and uninitialize the FileSystem provider because it defines the following provider-qualified path: `FileSystem::\\uncshare\abc\bar`.</span></span>

### <a name="provider-direct-paths"></a><span data-ttu-id="41992-135">Provedores-caminhos diretos</span><span class="sxs-lookup"><span data-stu-id="41992-135">Provider-direct paths</span></span>

<span data-ttu-id="41992-136">Para permitir o acesso remoto ao seu provedor do Windows PowerShell, ele deve dar suporte a um caminho direto do provedor para passar diretamente para o provedor do Windows PowerShell para o local atual.</span><span class="sxs-lookup"><span data-stu-id="41992-136">To allow remote access to your Windows PowerShell provider, it should support a provider-direct path to pass directly to the Windows PowerShell provider for the current location.</span></span> <span data-ttu-id="41992-137">Por exemplo, o provedor do Windows PowerShell do registro pode usar `\\server\regkeypath` como um caminho direto do provedor.</span><span class="sxs-lookup"><span data-stu-id="41992-137">For example, the registry Windows PowerShell provider can use `\\server\regkeypath` as a provider-direct path.</span></span>

### <a name="provider-internal-paths"></a><span data-ttu-id="41992-138">Provedor-caminhos internos</span><span class="sxs-lookup"><span data-stu-id="41992-138">Provider-internal paths</span></span>

<span data-ttu-id="41992-139">Para permitir que o cmdlet do provedor acesse dados usando interfaces de programação de aplicativo (APIs) não Windows PowerShell, seu provedor do Windows PowerShell deve dar suporte a um caminho interno do provedor.</span><span class="sxs-lookup"><span data-stu-id="41992-139">To allow the provider cmdlet to access data using non-Windows PowerShell application programming interfaces (APIs), your Windows PowerShell provider should support a provider-internal path.</span></span> <span data-ttu-id="41992-140">Esse caminho é indicado após "::" no caminho qualificado do provedor.</span><span class="sxs-lookup"><span data-stu-id="41992-140">This path is indicated after the "::" in the provider-qualified path.</span></span> <span data-ttu-id="41992-141">Por exemplo, o caminho interno do provedor do sistema de arquivos do provedor do Windows PowerShell é `\\uncshare\abc\bar`.</span><span class="sxs-lookup"><span data-stu-id="41992-141">For example, the provider-internal path for the filesystem Windows PowerShell provider is `\\uncshare\abc\bar`.</span></span>

## <a name="overriding-cmdlet-parameters"></a><span data-ttu-id="41992-142">Substituindo parâmetros de cmdlet</span><span class="sxs-lookup"><span data-stu-id="41992-142">Overriding cmdlet parameters</span></span>

<span data-ttu-id="41992-143">O comportamento de alguns cmdlets específicos do provedor pode ser substituído por um provedor.</span><span class="sxs-lookup"><span data-stu-id="41992-143">The behavior of some provider-specific cmdlets can be overridden by a provider.</span></span> <span data-ttu-id="41992-144">Para obter uma lista de parâmetros que podem ser substituídos e como substituí-los em sua classe de provedor, consulte [parâmetros de cmdlet do provedor](./provider-cmdlet-parameters.md)</span><span class="sxs-lookup"><span data-stu-id="41992-144">For a list of parameters that can be overridden, and how to override them in your provider class, see [Provider cmdlet parameters](./provider-cmdlet-parameters.md)</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="41992-145">Parâmetros dinâmicos</span><span class="sxs-lookup"><span data-stu-id="41992-145">Dynamic parameters</span></span>

<span data-ttu-id="41992-146">Os provedores podem definir parâmetros dinâmicos que são adicionados a um cmdlet de provedor quando o usuário especifica um determinado valor para um dos parâmetros estáticos do cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41992-146">Providers can define dynamic parameters that are added to a provider cmdlet when the user specifies a certain value for one of the static parameters of the cmdlet.</span></span> <span data-ttu-id="41992-147">Um provedor faz isso implementando um ou mais métodos de parâmetro dinâmicos.</span><span class="sxs-lookup"><span data-stu-id="41992-147">A provider does this by implementing one or more dynamic parameter methods.</span></span> <span data-ttu-id="41992-148">Para obter uma lista de parâmetros de cmdlet que podem ser usados para adicionar um parâmetro dinâmico e os métodos usados para implementá-los, consulte [parâmetros dinâmicos do cmdlet do provedor](./provider-cmdlet-dynamic-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="41992-148">For a list of cmdlet parameters that can be used to add dynamic parameter, and the methods used to implement them, see [Provider cmdlet dynamic parameters](./provider-cmdlet-dynamic-parameters.md).</span></span>

## <a name="provider-capabilities"></a><span data-ttu-id="41992-149">Recursos do provedor</span><span class="sxs-lookup"><span data-stu-id="41992-149">Provider capabilities</span></span>

<span data-ttu-id="41992-150">A enumeração [System. Management. Automation. Provider. Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) define uma série de recursos aos quais os provedores podem dar suporte.</span><span class="sxs-lookup"><span data-stu-id="41992-150">The [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumeration  defines a number of capabilities that providers can support.</span></span> <span data-ttu-id="41992-151">Isso inclui a capacidade de usar curingas, filtrar itens e transações de suporte.</span><span class="sxs-lookup"><span data-stu-id="41992-151">These include the ability to use wildcards, filter items, and support transactions.</span></span> <span data-ttu-id="41992-152">Para especificar recursos para um provedor, adicione uma lista de valores da enumeração [System. Management. Automation. Provider. Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) , combinada com uma operação lógica `OR`, como a [ System. Management. Automation. Provider. Cmdletproviderattribute. Providercapabilities \*](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute.ProviderCapabilities) Propriedade (o segundo parâmetro do atributo) do atributo [System. Management. Automation. Provider. Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) para seu classe de provedor.</span><span class="sxs-lookup"><span data-stu-id="41992-152">To specify capabilities for a provider, add a list of values of the  [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumeration, combined with a logical `OR` operation, as the [System.Management.Automation.Provider.Cmdletproviderattribute.Providercapabilities\*](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute.ProviderCapabilities) property (the second parameter of the attribute) of the [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) attribute for your provider class.</span></span> <span data-ttu-id="41992-153">Por exemplo, o atributo a seguir especifica que o provedor oferece suporte a [System. Management. Automation. Provider. Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities?view=pscore-6.2.0) **ShouldProcess** e [System. Management. Automation. Provider. Providercapabilities ](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities?view=pscore-6.2.0)Recursos de **Transações** .</span><span class="sxs-lookup"><span data-stu-id="41992-153">For example, the following attribute specifies that the provider supports the [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities?view=pscore-6.2.0) **ShouldProcess** and [System.Management.Automation.Provider.ProviderCapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities?view=pscore-6.2.0) **Transactions** capabilities.</span></span>

```csharp
[CmdletProvider(RegistryProvider.ProviderName, ProviderCapabilities.ShouldProcess | ProviderCapabilities.Transactions)]

```

## <a name="provider-cmdlet-help"></a><span data-ttu-id="41992-154">Ajuda do cmdlet do provedor</span><span class="sxs-lookup"><span data-stu-id="41992-154">Provider cmdlet help</span></span>

<span data-ttu-id="41992-155">Ao escrever um provedor, você pode implementar sua própria ajuda para os cmdlets do provedor aos quais você dá suporte.</span><span class="sxs-lookup"><span data-stu-id="41992-155">When writing a provider, you can implement your own Help for the provider cmdlets that you support.</span></span> <span data-ttu-id="41992-156">Isso inclui um único tópico de ajuda para cada cmdlet de provedor ou várias versões de um tópico da ajuda para casos em que o cmdlet do provedor atua de forma diferente com base no uso de parâmetros dinâmicos.</span><span class="sxs-lookup"><span data-stu-id="41992-156">This includes a single help topic for each provider cmdlet or multiple versions of a help topic for cases where the provider cmdlet acts differently based on the use of dynamic parameters.</span></span> <span data-ttu-id="41992-157">Para dar suporte à ajuda específica do cmdlet do provedor, seu provedor deve implementar a interface [System. Management. Automation. Provider. Icmdletprovidersupportshelp](/dotnet/api/System.Management.Automation.Provider.ICmdletProviderSupportsHelp) .</span><span class="sxs-lookup"><span data-stu-id="41992-157">To support provider cmdlet-specific help, your provider must implement the [System.Management.Automation.Provider.Icmdletprovidersupportshelp](/dotnet/api/System.Management.Automation.Provider.ICmdletProviderSupportsHelp) interface.</span></span>

<span data-ttu-id="41992-158">O mecanismo do Windows PowerShell chama o método [System. Management. Automation. Provider. Icmdletprovidersupportshelp. Gethelpmaml \*](/dotnet/api/System.Management.Automation.Provider.ICmdletProviderSupportsHelp.GetHelpMaml) para exibir o tópico da ajuda para seus cmdlets do provedor.</span><span class="sxs-lookup"><span data-stu-id="41992-158">The Windows PowerShell engine calls the [System.Management.Automation.Provider.Icmdletprovidersupportshelp.Gethelpmaml\*](/dotnet/api/System.Management.Automation.Provider.ICmdletProviderSupportsHelp.GetHelpMaml) method to display the Help topic for your provider cmdlets.</span></span> <span data-ttu-id="41992-159">O mecanismo fornece o nome do cmdlet que o usuário especificou ao executar o cmdlet `Get-Help` e o caminho atual do usuário.</span><span class="sxs-lookup"><span data-stu-id="41992-159">The engine provides the name of the cmdlet that the user specified when running the `Get-Help` cmdlet and the current path of the user.</span></span> <span data-ttu-id="41992-160">O caminho atual será necessário se o provedor implementar versões diferentes do mesmo cmdlet do provedor para unidades diferentes.</span><span class="sxs-lookup"><span data-stu-id="41992-160">The current path is required if your provider implements different versions of the same provider cmdlet for different drives.</span></span> <span data-ttu-id="41992-161">O método deve retornar uma cadeia de caracteres que contém o XML para a ajuda do cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41992-161">The method must return a string that contains the XML for the cmdlet Help.</span></span>

<span data-ttu-id="41992-162">O conteúdo do arquivo de ajuda é escrito usando PSMAML XML.</span><span class="sxs-lookup"><span data-stu-id="41992-162">The content for the Help file is written using PSMAML XML.</span></span> <span data-ttu-id="41992-163">Esse é o mesmo esquema XML usado para gravar o conteúdo da ajuda para cmdlets autônomos.</span><span class="sxs-lookup"><span data-stu-id="41992-163">This is the same XML schema that is used for writing Help content for stand-alone cmdlets.</span></span> <span data-ttu-id="41992-164">Adicione o conteúdo para a ajuda do cmdlet personalizado ao arquivo de ajuda para seu provedor no elemento `CmdletHelpPaths`.</span><span class="sxs-lookup"><span data-stu-id="41992-164">Add the content for your custom cmdlet Help to the Help file for your provider under the `CmdletHelpPaths` element.</span></span> <span data-ttu-id="41992-165">O exemplo a seguir mostra o elemento `command` para um cmdlet de provedor único e mostra como você especifica o nome do cmdlet do provedor que seu provedor.</span><span class="sxs-lookup"><span data-stu-id="41992-165">The following example shows the `command` element for a single provider cmdlet, and it shows how you specify the name of the provider cmdlet that your provider.</span></span> <span data-ttu-id="41992-166">suportar</span><span class="sxs-lookup"><span data-stu-id="41992-166">supports</span></span>

```xml
<CmdletHelpPaths>
  <command:command>
    <command:details>
      <command:name>ProviderCmdletName</command:name>
      <command:verb>Verb</command:verb>
      <command:noun>Noun</command:noun>
    <command:details>
  </command:command>
<CmdletHelpPath>
```

## <a name="see-also"></a><span data-ttu-id="41992-167">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="41992-167">See Also</span></span>

[<span data-ttu-id="41992-168">Funcionalidade do provedor do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="41992-168">Windows PowerShell Provider Functionality</span></span>](./provider-types.md)

[<span data-ttu-id="41992-169">Cmdlets do provedor</span><span class="sxs-lookup"><span data-stu-id="41992-169">Provider Cmdlets</span></span>](./provider-cmdlets.md)

[<span data-ttu-id="41992-170">Escrevendo um provedor do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="41992-170">Writing a Windows PowerShell Provider</span></span>](./writing-a-windows-powershell-provider.md)