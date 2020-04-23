---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Usando dados de configuração
ms.openlocfilehash: 7d13b19ba932d1a818194a221f145fd1a3832547
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2020
ms.locfileid: "71954183"
---
# <a name="using-configuration-data-in-dsc"></a><span data-ttu-id="561f4-103">Usando dados de configuração em DSC</span><span class="sxs-lookup"><span data-stu-id="561f4-103">Using configuration data in DSC</span></span>

> <span data-ttu-id="561f4-104">Aplica-se a: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="561f4-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="561f4-105">Usando o parâmetro **ConfigurationData** da DSC interna, você pode definir os dados que podem ser usados dentro de uma configuração.</span><span class="sxs-lookup"><span data-stu-id="561f4-105">By using the built-in DSC **ConfigurationData** parameter, you can define data that can be used within a configuration.</span></span>
<span data-ttu-id="561f4-106">Isso permite que você crie uma única configuração que pode ser usada para vários nós ou para ambientes diferentes.</span><span class="sxs-lookup"><span data-stu-id="561f4-106">This allows you to create a single configuration that can be used for multiple nodes or for different environments.</span></span>
<span data-ttu-id="561f4-107">Por exemplo, se estiver desenvolvendo um aplicativo, você pode usar uma configuração para os ambientes de desenvolvimento e produção e usar dados de configuração para especificar dados para cada ambiente.</span><span class="sxs-lookup"><span data-stu-id="561f4-107">For example, if you are developing an application, you can use one configuration for both development and production environments, and use configuration data to specify data for each environment.</span></span>

<span data-ttu-id="561f4-108">Este tópico descreve a estrutura da tabela de hash **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="561f4-108">This topic describes the structure of the **ConfigurationData** hashtable.</span></span>
<span data-ttu-id="561f4-109">Para obter exemplos de como usar dados de configuração, consulte [Separando Dados de Configuração e de Ambiente](separatingEnvData.md).</span><span class="sxs-lookup"><span data-stu-id="561f4-109">For examples of how to use configuration data, see [Separating configuration and environment data](separatingEnvData.md).</span></span>

## <a name="the-configurationdata-common-parameter"></a><span data-ttu-id="561f4-110">O parâmetro comum de ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="561f4-110">The ConfigurationData common parameter</span></span>

<span data-ttu-id="561f4-111">Uma configuração DSC usa um parâmetro comum, **ConfigurationData**, que você especifica ao compilar a configuração.</span><span class="sxs-lookup"><span data-stu-id="561f4-111">A DSC configuration takes a common parameter, **ConfigurationData**, that you specify when you compile the configuration.</span></span>
<span data-ttu-id="561f4-112">Para obter informações de como compilar configurações, consulte [Configurações DSC](configurations.md).</span><span class="sxs-lookup"><span data-stu-id="561f4-112">For information about compiling configurations, see [DSC configurations](configurations.md).</span></span>

<span data-ttu-id="561f4-113">O parâmetro **ConfigurationData** é uma tabela de hash que precisa ter pelo menos uma chave chamada **AllNodes**.</span><span class="sxs-lookup"><span data-stu-id="561f4-113">The **ConfigurationData** parameter is a hashtable that must have at least one key named **AllNodes**.</span></span>
<span data-ttu-id="561f4-114">Ele também pode ter uma ou mais chaves.</span><span class="sxs-lookup"><span data-stu-id="561f4-114">It can also have one or more other keys.</span></span>

> [!NOTE]
> <span data-ttu-id="561f4-115">Os exemplos neste tópico usam uma única chave adicional (que não é a chave nomeada **AllNodes**) denominada `NonNodeData`, mas você pode incluir qualquer número de chaves adicionais e nomeá-las como desejar.</span><span class="sxs-lookup"><span data-stu-id="561f4-115">The examples in this topic use a single additional key (other than the named **AllNodes** key) named `NonNodeData`, but you can include any number of additional keys, and name them whatever you want.</span></span>

```powershell
$MyData =
@{
    AllNodes = @()
    NonNodeData = ""
}
```

<span data-ttu-id="561f4-116">O valor da chave **AllNodes** é uma matriz.</span><span class="sxs-lookup"><span data-stu-id="561f4-116">The value of the **AllNodes** key is an array.</span></span> <span data-ttu-id="561f4-117">Cada elemento dessa matriz também é uma tabela de hash que deve ter pelo menos uma chave chamada **NodeName**:</span><span class="sxs-lookup"><span data-stu-id="561f4-117">Each element of this array is also a hash table that must have at least one key named **NodeName**:</span></span>

```powershell
$MyData =
@{
    AllNodes =
    @(
        @{
            NodeName = "VM-1"
        },


        @{
            NodeName = "VM-2"
        },


        @{
            NodeName = "VM-3"
        }
    );

    NonNodeData = ""
}
```

<span data-ttu-id="561f4-118">Você também pode adicionar outras chaves para cada tabela de hash:</span><span class="sxs-lookup"><span data-stu-id="561f4-118">You can add other keys to each hash table as well:</span></span>

```powershell
$MyData =
@{
    AllNodes =
    @(
        @{
            NodeName = "VM-1"
            Role     = "WebServer"
        },


        @{
            NodeName = "VM-2"
            Role     = "SQLServer"
        },


        @{
            NodeName = "VM-3"
            Role     = "WebServer"
        }
    );

    NonNodeData = ""
}
```

<span data-ttu-id="561f4-119">Para aplicar uma propriedade para todos os nós, você pode criar um membro da matriz **AllNodes** que possua um **NodeName** de `*`.</span><span class="sxs-lookup"><span data-stu-id="561f4-119">To apply a property to all nodes, you can create a member of the **AllNodes** array that has a **NodeName** of `*`.</span></span>
<span data-ttu-id="561f4-120">Por exemplo, para atribuir uma propriedade `LogPath` a cada nó, você pode fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="561f4-120">For example, to give every node a `LogPath` property, you could do this:</span></span>

```powershell
$MyData =
@{
    AllNodes =
    @(
        @{
            NodeName     = "*"
            LogPath      = "C:\Logs"
        },


        @{
            NodeName     = "VM-1"
            Role         = "WebServer"
            SiteContents = "C:\Site1"
            SiteName     = "Website1"
        },


        @{
            NodeName     = "VM-2"
            Role         = "SQLServer"
        },


        @{
            NodeName     = "VM-3"
            Role         = "WebServer"
            SiteContents = "C:\Site2"
            SiteName     = "Website3"
        }
    );
}
```

<span data-ttu-id="561f4-121">Isso é o equivalente a adicionar uma propriedade com um nome de `LogPath` com um valor de `"C:\Logs"` para cada um dos outros blocos (`VM-1`, `VM-2` e `VM-3`).</span><span class="sxs-lookup"><span data-stu-id="561f4-121">This is the equivalent of adding a property with a name of `LogPath` with a value of `"C:\Logs"` to each of the other blocks (`VM-1`, `VM-2`, and `VM-3`).</span></span>

## <a name="defining-the-configurationdata-hashtable"></a><span data-ttu-id="561f4-122">Definição da tabela de hash de ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="561f4-122">Defining the ConfigurationData hashtable</span></span>

<span data-ttu-id="561f4-123">Você pode definir **ConfigurationData** como uma variável dentro do mesmo arquivo de script que uma configuração (como em nossos exemplos anteriores) ou em um arquivo `.psd1` separado.</span><span class="sxs-lookup"><span data-stu-id="561f4-123">You can define **ConfigurationData** either as a variable within the same script file as a configuration (as in our previous examples) or in a separate `.psd1` file.</span></span>
<span data-ttu-id="561f4-124">Para definir **ConfigurationData** em um arquivo `.psd1`, crie um arquivo que contenha somente a tabela de hash que representa os dados de configuração.</span><span class="sxs-lookup"><span data-stu-id="561f4-124">To define **ConfigurationData** in a `.psd1` file, create a file that contains only the hashtable that represents the configuration data.</span></span>

<span data-ttu-id="561f4-125">Por exemplo, você poderia criar um arquivo chamado `MyData.psd1` com o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="561f4-125">For example, you could create a file named `MyData.psd1` with the following contents:</span></span>

```powershell
@{
    AllNodes =
    @(
        @{
            NodeName    = 'VM-1'
            FeatureName = 'Web-Server'
        },

        @{
            NodeName    = 'VM-2'
            FeatureName = 'Hyper-V'
        }
    )
}
```

## <a name="compiling-a-configuration-with-configuration-data"></a><span data-ttu-id="561f4-126">Compilando uma configuração com os dados de configuração</span><span class="sxs-lookup"><span data-stu-id="561f4-126">Compiling a configuration with configuration data</span></span>

<span data-ttu-id="561f4-127">Para compilar uma configuração para a qual você definiu os dados de configuração, passe os dados de configuração como o valor do parâmetro **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="561f4-127">To compile a configuration for which you have defined configuration data, you pass the configuration data as the value of the **ConfigurationData** parameter.</span></span>

<span data-ttu-id="561f4-128">Isso criará um arquivo MOF para cada entrada na matriz **AllNodes**.</span><span class="sxs-lookup"><span data-stu-id="561f4-128">This will create a MOF file for each entry in the **AllNodes** array.</span></span>
<span data-ttu-id="561f4-129">Cada arquivo MOF será nomeado com a propriedade `NodeName` da entrada de matriz correspondente.</span><span class="sxs-lookup"><span data-stu-id="561f4-129">Each MOF file will be named with the `NodeName` property of the corresponding array entry.</span></span>

<span data-ttu-id="561f4-130">Por exemplo, se você definir dados de configuração como o arquivo `MyData.psd1` acima, compilar uma configuração criará os arquivos `VM-1.mof` e `VM-2.mof`.</span><span class="sxs-lookup"><span data-stu-id="561f4-130">For example, if you define configuration data as in the `MyData.psd1` file above, compiling a configuration would create both `VM-1.mof` and `VM-2.mof` files.</span></span>

### <a name="compiling-a-configuration-with-configuration-data-using-a-variable"></a><span data-ttu-id="561f4-131">Compilando uma configuração com os dados de configuração usando uma variável</span><span class="sxs-lookup"><span data-stu-id="561f4-131">Compiling a configuration with configuration data using a variable</span></span>

<span data-ttu-id="561f4-132">Para usar dados de configuração que são definidos como uma variável no mesmo arquivo `.ps1` que a configuração, passe o nome da variável como o valor do parâmetro **ConfigurationData** ao compilar a configuração:</span><span class="sxs-lookup"><span data-stu-id="561f4-132">To use configuration data that is defined as a variable in the same `.ps1` file as the configuration, you pass the variable name as the value of the **ConfigurationData** parameter when compiling the configuration:</span></span>

```powershell
MyDscConfiguration -ConfigurationData $MyData
```

### <a name="compiling-a-configuration-with-configuration-data-using-a-data-file"></a><span data-ttu-id="561f4-133">Compilando uma configuração com os dados de configuração usando um arquivo de dados</span><span class="sxs-lookup"><span data-stu-id="561f4-133">Compiling a configuration with configuration data using a data file</span></span>

<span data-ttu-id="561f4-134">Para usar dados de configuração que são definidos em um arquivo .psd1, você passa o caminho e o nome desse arquivo como o valor do parâmetro **ConfigurationData** ao compilar a configuração:</span><span class="sxs-lookup"><span data-stu-id="561f4-134">To use configuration data that is defined in a .psd1 file, you pass the path and name of that file as the value of the **ConfigurationData** parameter when compiling the configuration:</span></span>

```powershell
MyDscConfiguration -ConfigurationData .\MyData.psd1
```

## <a name="using-configurationdata-variables-in-a-configuration"></a><span data-ttu-id="561f4-135">Usando variáveis de ConfigurationData em uma configuração</span><span class="sxs-lookup"><span data-stu-id="561f4-135">Using ConfigurationData variables in a configuration</span></span>

<span data-ttu-id="561f4-136">O DSC fornece as seguintes variáveis especiais que podem ser usadas em um script de configuração:</span><span class="sxs-lookup"><span data-stu-id="561f4-136">DSC provides the following special variables that can be used in a configuration script:</span></span>

- <span data-ttu-id="561f4-137">A **$AllNodes** refere-se a toda a coleção de nós definida em **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="561f4-137">**$AllNodes** refers to the entire collection of nodes defined in **ConfigurationData**.</span></span> <span data-ttu-id="561f4-138">Você pode filtrar a coleção **AllNodes** usando **.Where()** e **.ForEach()** .</span><span class="sxs-lookup"><span data-stu-id="561f4-138">You can filter the **AllNodes** collection by using **.Where()** and **.ForEach()**.</span></span>
- <span data-ttu-id="561f4-139">O **ConfigurationData** refere-se à tabela de hash inteira que é passada como parâmetro ao compilar uma configuração.</span><span class="sxs-lookup"><span data-stu-id="561f4-139">**ConfigurationData** refers to the entire hash table that is passed as the parameter when compiling a configuration.</span></span>
- <span data-ttu-id="561f4-140">**MyTypeName** contém o nome da [configuração](configurations.md) na qual a variável é usada.</span><span class="sxs-lookup"><span data-stu-id="561f4-140">**MyTypeName** contains the [configuration](configurations.md) name the variable is used in.</span></span> <span data-ttu-id="561f4-141">Por exemplo, na configuração `MyDscConfiguration`, `$MyTypeName` terá um valor de `MyDscConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="561f4-141">For example, in the configuration `MyDscConfiguration`, the `$MyTypeName` will have a value of `MyDscConfiguration`.</span></span>
- <span data-ttu-id="561f4-142">O **Nó** refere-se a uma entrada específica na coleção **AllNodes** depois que ela é filtrada usando **.Where()** ou **.ForEach()** .</span><span class="sxs-lookup"><span data-stu-id="561f4-142">**Node** refers to a particular entry in the **AllNodes** collection after it is filtered by using **.Where()** or **.ForEach()**.</span></span>
  - <span data-ttu-id="561f4-143">Leia mais sobre esses métodos em [about_arrays](/powershell/module/microsoft.powershell.core/about/about_arrays)</span><span class="sxs-lookup"><span data-stu-id="561f4-143">You can read more about these methods in [about_arrays](/powershell/module/microsoft.powershell.core/about/about_arrays)</span></span>

## <a name="using-non-node-data"></a><span data-ttu-id="561f4-144">Usar dados sem nós</span><span class="sxs-lookup"><span data-stu-id="561f4-144">Using non-node data</span></span>

<span data-ttu-id="561f4-145">Como vimos nos exemplos anteriores, a tabela de hash **ConfigurationData** pode ter uma ou mais chaves além da chave **AllNodes** necessária.</span><span class="sxs-lookup"><span data-stu-id="561f4-145">As we've seen in previous examples, the **ConfigurationData** hashtable can have one or more keys in addition to the required **AllNodes** key.</span></span>
<span data-ttu-id="561f4-146">Nos exemplos deste tópico, usamos apenas um único nó adicional e o nomeamos como `NonNodeData`.</span><span class="sxs-lookup"><span data-stu-id="561f4-146">In the examples in this topic, we have used only a single additional node, and named it `NonNodeData`.</span></span>
<span data-ttu-id="561f4-147">No entanto, você pode definir quantas chaves adicionais quiser e nomeá-las da maneira desejada.</span><span class="sxs-lookup"><span data-stu-id="561f4-147">However, you can define any number of additional keys, and name them anything you want.</span></span>

<span data-ttu-id="561f4-148">Para obter um exemplo de como usar dados que não são do nó, consulte [Separando Dados de Configuração e de Ambiente](separatingEnvData.md).</span><span class="sxs-lookup"><span data-stu-id="561f4-148">For an example of using non-node data, see [Separating configuration and environment data](separatingEnvData.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="561f4-149">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="561f4-149">See Also</span></span>

- [<span data-ttu-id="561f4-150">Opções de credenciais nos dados de configuração</span><span class="sxs-lookup"><span data-stu-id="561f4-150">Credentials Options in Configuration Data</span></span>](configDataCredentials.md)
- [<span data-ttu-id="561f4-151">Configurações DSC</span><span class="sxs-lookup"><span data-stu-id="561f4-151">DSC Configurations</span></span>](configurations.md)