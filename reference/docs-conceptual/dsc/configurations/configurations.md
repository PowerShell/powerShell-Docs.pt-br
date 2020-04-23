---
ms.date: 12/12/2018
keywords: DSC,powershell,configuração,instalação
title: Configurações DSC
ms.openlocfilehash: d7749ec88f9cca3e29c6b38d61fb73776af7ceb4
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2020
ms.locfileid: "71954493"
---
# <a name="dsc-configurations"></a><span data-ttu-id="152e2-103">Configurações DSC</span><span class="sxs-lookup"><span data-stu-id="152e2-103">DSC Configurations</span></span>

> <span data-ttu-id="152e2-104">Aplica-se a: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="152e2-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="152e2-105">As configurações DSC são scripts do PowerShell que definem um tipo especial de função.</span><span class="sxs-lookup"><span data-stu-id="152e2-105">DSC configurations are PowerShell scripts that define a special type of function.</span></span>
<span data-ttu-id="152e2-106">Para definir uma configuração utilize a palavra-chave do PowerShell **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="152e2-106">To define a configuration, you use the PowerShell keyword **Configuration**.</span></span>

```powershell
Configuration MyDscConfiguration {
    Node "TEST-PC1" {
        WindowsFeature MyFeatureInstance {
            Ensure = 'Present'
            Name = 'RSAT'
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}
MyDscConfiguration
```

<span data-ttu-id="152e2-107">Salve o script como um arquivo `.ps1`.</span><span class="sxs-lookup"><span data-stu-id="152e2-107">Save the script as a `.ps1` file.</span></span>

## <a name="configuration-syntax"></a><span data-ttu-id="152e2-108">Sintaxe da configuração</span><span class="sxs-lookup"><span data-stu-id="152e2-108">Configuration syntax</span></span>

<span data-ttu-id="152e2-109">Um script de configuração é composto por estas partes:</span><span class="sxs-lookup"><span data-stu-id="152e2-109">A configuration script consists of the following parts:</span></span>

- <span data-ttu-id="152e2-110">O bloco **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="152e2-110">The **Configuration** block.</span></span> <span data-ttu-id="152e2-111">É o bloco de script externo.</span><span class="sxs-lookup"><span data-stu-id="152e2-111">This is the outermost script block.</span></span> <span data-ttu-id="152e2-112">Para defini-lo, use a palavra-chave **Configuration** e forneça um nome.</span><span class="sxs-lookup"><span data-stu-id="152e2-112">You define it by using the **Configuration** keyword and providing a name.</span></span> <span data-ttu-id="152e2-113">Nesse caso, o nome da configuração é "MyDscConfiguration".</span><span class="sxs-lookup"><span data-stu-id="152e2-113">In this case, the name of the configuration is "MyDscConfiguration".</span></span>
- <span data-ttu-id="152e2-114">Um ou mais blocos de **Nó**.</span><span class="sxs-lookup"><span data-stu-id="152e2-114">One or more **Node** blocks.</span></span> <span data-ttu-id="152e2-115">Definem os nós (computadores ou máquinas virtuais) que você está configurando.</span><span class="sxs-lookup"><span data-stu-id="152e2-115">These define the nodes (computers or VMs) that you are configuring.</span></span> <span data-ttu-id="152e2-116">Na configuração acima, há um bloco de **Nó** que tem como destino um computador denominado "TEST-PC1".</span><span class="sxs-lookup"><span data-stu-id="152e2-116">In the above configuration, there is one **Node** block that targets a computer named "TEST-PC1".</span></span> <span data-ttu-id="152e2-117">O bloco Nó pode aceitar vários nomes de computador.</span><span class="sxs-lookup"><span data-stu-id="152e2-117">The Node block can accept multiple computer names.</span></span>
- <span data-ttu-id="152e2-118">Um ou mais blocos de recurso.</span><span class="sxs-lookup"><span data-stu-id="152e2-118">One or more resource blocks.</span></span> <span data-ttu-id="152e2-119">É onde a configuração define as propriedades para os recursos que estão sendo configurados.</span><span class="sxs-lookup"><span data-stu-id="152e2-119">This is where the configuration sets the properties for the resources that it is configuring.</span></span> <span data-ttu-id="152e2-120">Nesse caso, há dois blocos de recurso; cada um deles chama o recurso "WindowsFeature".</span><span class="sxs-lookup"><span data-stu-id="152e2-120">In this case, there are two resource blocks, each of which call the "WindowsFeature" resource.</span></span>

<span data-ttu-id="152e2-121">Dentro de um bloco de **configuração**, é possível fazer qualquer coisa que normalmente poderia ser feita em uma função do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="152e2-121">Within a **Configuration** block, you can do anything that you normally could in a PowerShell function.</span></span> <span data-ttu-id="152e2-122">No exemplo anterior, se você não quisesse embutir em código o nome do computador de destino na configuração, poderia adicionar um parâmetro para o nome do nó:</span><span class="sxs-lookup"><span data-stu-id="152e2-122">For example, in the previous example, if you didn't want to hard code the name of the target computer in the configuration, you could add a parameter for the node name:</span></span>

<span data-ttu-id="152e2-123">Neste exemplo, você especifica o nome do nó passando-o como o parâmetro **ComputerName** quando compila a configuração.</span><span class="sxs-lookup"><span data-stu-id="152e2-123">In this example, you specify the name of the node by passing it as the **ComputerName** parameter when you compile the configuration.</span></span> <span data-ttu-id="152e2-124">O nome padrão é "localhost".</span><span class="sxs-lookup"><span data-stu-id="152e2-124">The name defaults to "localhost".</span></span>

```powershell
Configuration MyDscConfiguration
{
    param
    (
        [string[]]$ComputerName='localhost'
    )

    Node $ComputerName
    {
        WindowsFeature MyFeatureInstance
        {
            Ensure = 'Present'
            Name = 'RSAT'
        }

        WindowsFeature My2ndFeatureInstance
        {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}

MyDscConfiguration
```

<span data-ttu-id="152e2-125">O bloco **Nó** também pode aceitar vários nomes de computador.</span><span class="sxs-lookup"><span data-stu-id="152e2-125">The **Node** block can also accept multiple computer names.</span></span> <span data-ttu-id="152e2-126">No exemplo acima, você pode usar o parâmetro `-ComputerName` ou passar uma lista de computadores separados por vírgula diretamente ao bloco **Nó**.</span><span class="sxs-lookup"><span data-stu-id="152e2-126">In the above example, you can either use the `-ComputerName` parameter, or pass a comma-separated list of computers directly to the **Node** block.</span></span>

```powershell
MyDscConfiguration -ComputerName "localhost", "Server01"
```

<span data-ttu-id="152e2-127">Ao especificar uma lista de computadores para o bloco **Nó**, dentro de uma configuração, você precisa usar a notação de matriz.</span><span class="sxs-lookup"><span data-stu-id="152e2-127">When specifying a list of computers to the **Node** block, from within a Configuration, you need to use array-notation.</span></span>

```powershell
Configuration MyDscConfiguration
{
    Node @('localhost', 'Server01')
    {
        WindowsFeature MyFeatureInstance
        {
            Ensure = 'Present'
            Name = 'RSAT'
        }

        WindowsFeature My2ndFeatureInstance
        {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}

MyDscConfiguration
```

## <a name="compiling-the-configuration"></a><span data-ttu-id="152e2-128">Compilando a configuração</span><span class="sxs-lookup"><span data-stu-id="152e2-128">Compiling the configuration</span></span>

<span data-ttu-id="152e2-129">Para poder aplicar uma configuração, você precisa compilá-la em um documento MOF.</span><span class="sxs-lookup"><span data-stu-id="152e2-129">Before you can enact a configuration, you have to compile it into a MOF document.</span></span>
<span data-ttu-id="152e2-130">Faça isso chamando a configuração como você chamaria uma função do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="152e2-130">You do this by calling the configuration like you would call a PowerShell function.</span></span>
<span data-ttu-id="152e2-131">A última linha do exemplo contendo somente o nome da configuração, chama a configuração.</span><span class="sxs-lookup"><span data-stu-id="152e2-131">The last line of the example containing only the name of the configuration, calls the configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="152e2-132">Para chamar uma configuração, a função precisa estar no escopo global (como acontece com qualquer outra função do PowerShell).</span><span class="sxs-lookup"><span data-stu-id="152e2-132">To call a configuration, the function must be in global scope (as with any other PowerShell function).</span></span>
> <span data-ttu-id="152e2-133">Isso pode ser feito por meio de "dot-sourcing" do script ou ao executar o script de configuração usando F5 ou clicando no botão **Executar Script** no ISE.</span><span class="sxs-lookup"><span data-stu-id="152e2-133">You can make this happen either by "dot-sourcing" the script, or by running the configuration script by using F5 or clicking on the **Run Script** button in the ISE.</span></span>
> <span data-ttu-id="152e2-134">Para fazer o dot-source do script, execute o comando `. .\myConfig.ps1`, em que `myConfig.ps1` é o nome do arquivo de script que contém sua configuração.</span><span class="sxs-lookup"><span data-stu-id="152e2-134">To dot-source the script, run the command `. .\myConfig.ps1` where `myConfig.ps1` is the name of the script file that contains your configuration.</span></span>

<span data-ttu-id="152e2-135">Quando você chama a configuração, ela:</span><span class="sxs-lookup"><span data-stu-id="152e2-135">When you call the configuration, it:</span></span>

- <span data-ttu-id="152e2-136">Resolve todas as variáveis</span><span class="sxs-lookup"><span data-stu-id="152e2-136">Resolves all variables</span></span>
- <span data-ttu-id="152e2-137">Uma pasta no diretório atual com o mesmo nome que a configuração.</span><span class="sxs-lookup"><span data-stu-id="152e2-137">Creates a folder in the current directory with the same name as the configuration.</span></span>
- <span data-ttu-id="152e2-138">Um arquivo chamado _NodeName_.mof no novo diretório, em que _NodeName_ é o nome do nó de destino da configuração.</span><span class="sxs-lookup"><span data-stu-id="152e2-138">Creates a file named _NodeName_.mof in the new directory, where _NodeName_ is the name of the target node of the configuration.</span></span>
  <span data-ttu-id="152e2-139">Se houver mais de um nó, será criado um arquivo MOF para cada nó.</span><span class="sxs-lookup"><span data-stu-id="152e2-139">If there is more than one node, a MOF file will be created for each node.</span></span>

> [!NOTE]
> <span data-ttu-id="152e2-140">O arquivo MOF contém todas as informações de configuração para o nó de destino.</span><span class="sxs-lookup"><span data-stu-id="152e2-140">The MOF file contains all of the configuration information for the target node.</span></span> <span data-ttu-id="152e2-141">Por isso, é importante mantê-lo seguro.</span><span class="sxs-lookup"><span data-stu-id="152e2-141">Because of this, it's important to keep it secure.</span></span>
> <span data-ttu-id="152e2-142">Para obter mais informações, consulte [Protegendo o arquivo MOF](../pull-server/secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="152e2-142">For more information, see [Securing the MOF file](../pull-server/secureMOF.md).</span></span>

<span data-ttu-id="152e2-143">A compilação da primeira configuração acima resulta na seguinte estrutura de pastas:</span><span class="sxs-lookup"><span data-stu-id="152e2-143">Compiling the first configuration above results in the following folder structure:</span></span>

```powershell
. .\MyDscConfiguration.ps1
MyDscConfiguration
```

```
    Directory: C:\users\default\Documents\DSC Configurations\MyDscConfiguration
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       10/23/2015   4:32 PM           2842 localhost.mof
```

<span data-ttu-id="152e2-144">Se a configuração utilizar um parâmetro, como no segundo exemplo, ele precisará ser fornecido no tempo de compilação.</span><span class="sxs-lookup"><span data-stu-id="152e2-144">If the configuration takes a parameter, as in the second example, that has to be provided at compile time.</span></span> <span data-ttu-id="152e2-145">A aparência deveria ser esta:</span><span class="sxs-lookup"><span data-stu-id="152e2-145">Here's how that would look:</span></span>

```powershell
. .\MyDscConfiguration.ps1
MyDscConfiguration -ComputerName 'MyTestNode'
```

```
    Directory: C:\users\default\Documents\DSC Configurations\MyDscConfiguration
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       10/23/2015   4:32 PM           2842 MyTestNode.mof
```

## <a name="using-new-resources-in-your-configuration"></a><span data-ttu-id="152e2-146">Uso de novos recursos na sua configuração</span><span class="sxs-lookup"><span data-stu-id="152e2-146">Using new resources in Your configuration</span></span>

<span data-ttu-id="152e2-147">Se você executou os exemplos anteriores, talvez tenha notado que foi informado que estava usando um recurso sem importá-lo explicitamente.</span><span class="sxs-lookup"><span data-stu-id="152e2-147">If you ran the previous examples, you might have noticed that you were warned that you were using a resource without explicitly importing it.</span></span>
<span data-ttu-id="152e2-148">Atualmente, a DSC vem com 12 recursos como parte do módulo PSDesiredStateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="152e2-148">Today, DSC ships with 12 resources as part of the PSDesiredStateConfiguration module.</span></span>

<span data-ttu-id="152e2-149">O cmdlet [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) pode ser usado para determinar quais recursos estão instalados no sistema e disponíveis para uso pelo LCM.</span><span class="sxs-lookup"><span data-stu-id="152e2-149">The cmdlet, [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), can be used to determine what resources are installed on the system and available for use by the LCM.</span></span>
<span data-ttu-id="152e2-150">Depois que esses módulos forem colocados em `$env:PSModulePath` e reconhecidos adequadamente pelo [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), ainda precisam ser carregados na sua configuração.</span><span class="sxs-lookup"><span data-stu-id="152e2-150">Once these modules have been placed in `$env:PSModulePath` and are properly recognized by [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), they still need to be loaded within your configuration.</span></span>

<span data-ttu-id="152e2-151">**Import-DscResource** é uma palavra-chave dinâmica que pode ser reconhecida apenas dentro de um bloco **Configuração**, não se trata de um cmdlet.</span><span class="sxs-lookup"><span data-stu-id="152e2-151">**Import-DscResource** is a dynamic keyword that can only be recognized within a **Configuration** block, it is not a cmdlet.</span></span>
<span data-ttu-id="152e2-152">O **Import-DscResource** dá suporte a dois parâmetros:</span><span class="sxs-lookup"><span data-stu-id="152e2-152">**Import-DscResource** supports two parameters:</span></span>

- <span data-ttu-id="152e2-153">**ModuleName** é a forma recomendada de usar o **Import-DscResource**.</span><span class="sxs-lookup"><span data-stu-id="152e2-153">**ModuleName** is the recommended way of using **Import-DscResource**.</span></span> <span data-ttu-id="152e2-154">Aceita o nome do módulo que contém os recursos que serão importados (assim como uma matriz de cadeia de caracteres de nomes de módulos).</span><span class="sxs-lookup"><span data-stu-id="152e2-154">It accepts the name of the module that contains the resources to be imported (as well as a string array of module names).</span></span>
- <span data-ttu-id="152e2-155">**Name** é o nome do recurso que será importado.</span><span class="sxs-lookup"><span data-stu-id="152e2-155">**Name** is the name of the resource to import.</span></span> <span data-ttu-id="152e2-156">Não é o nome amigável gerado como "Name" pelo [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), mas o nome de classe usado na hora de definir o esquema de recurso (gerado como **ResourceType** pelo [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource)).</span><span class="sxs-lookup"><span data-stu-id="152e2-156">This is not the friendly name returned as "Name" by [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), but the class name used when defining the resource schema (returned as **ResourceType** by [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource)).</span></span>

<span data-ttu-id="152e2-157">Para saber mais sobre como usar `Import-DSCResource`, confira [Usando Import-DSCResource](import-dscresource.md)</span><span class="sxs-lookup"><span data-stu-id="152e2-157">For more information on using `Import-DSCResource`, see [Using Import-DSCResource](import-dscresource.md)</span></span>

## <a name="powershell-v4-and-v5-differences"></a><span data-ttu-id="152e2-158">Diferenças entre o PowerShell v4 e v5</span><span class="sxs-lookup"><span data-stu-id="152e2-158">PowerShell v4 and v5 differences</span></span>

<span data-ttu-id="152e2-159">Há diferenças quanto ao local em que os recursos DSC precisam ser armazenados no PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="152e2-159">There are differences in where DSC resources need to be stored in PowerShell 4.0.</span></span> <span data-ttu-id="152e2-160">Para saber mais, confira [Local do recurso](import-dscresource.md#resource-location).</span><span class="sxs-lookup"><span data-stu-id="152e2-160">For more information, see [Resource location](import-dscresource.md#resource-location).</span></span>

## <a name="see-also"></a><span data-ttu-id="152e2-161">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="152e2-161">See Also</span></span>

- [<span data-ttu-id="152e2-162">Visão geral da Desired State Configuration do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="152e2-162">Windows PowerShell Desired State Configuration Overview</span></span>](../overview/overview.md)
- [<span data-ttu-id="152e2-163">Recursos de DSC</span><span class="sxs-lookup"><span data-stu-id="152e2-163">DSC Resources</span></span>](../resources/resources.md)
- [<span data-ttu-id="152e2-164">Configurando o Gerenciador de Configurações Local</span><span class="sxs-lookup"><span data-stu-id="152e2-164">Configuring The Local Configuration Manager</span></span>](../managing-nodes/metaConfig.md)
