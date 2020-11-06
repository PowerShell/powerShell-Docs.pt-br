---
ms.date: 07/08/2020
keywords: DSC,powershell,configuração,instalação
title: Usando a ferramenta Designer de Recursos
description: A ferramenta Designer de Recursos é um conjunto de cmdlets expostos pelo módulo xDscResourceDesigner que facilitam a criação de recursos de DSC do PowerShell.
ms.openlocfilehash: efe36d045ac3fba3823cb1f812bb5761d238fdf1
ms.sourcegitcommit: 488a940c7c828820b36a6ba56c119f64614afc29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92656487"
---
# <a name="using-the-resource-designer-tool"></a><span data-ttu-id="9c787-104">Usando a ferramenta Designer de Recursos</span><span class="sxs-lookup"><span data-stu-id="9c787-104">Using the Resource Designer tool</span></span>

> <span data-ttu-id="9c787-105">Aplica-se a: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="9c787-105">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="9c787-106">A ferramenta Designer de Recursos é um conjunto de cmdlets expostos pelo módulo **xDscResourceDesigner** que facilitam a criação de recursos de Configuração de Estado Desejado (DSC) do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9c787-106">The Resource Designer tool is a set of cmdlets exposed by the **xDscResourceDesigner** module that make creating Windows PowerShell Desired State Configuration (DSC) resources easier.</span></span> <span data-ttu-id="9c787-107">Os cmdlets nesse recurso ajudam a criar o esquema MOF, o módulo de script e a estrutura de diretórios para seu novo recurso.</span><span class="sxs-lookup"><span data-stu-id="9c787-107">The cmdlets in this resource help create the MOF schema, the script module, and the directory structure for your new resource.</span></span> <span data-ttu-id="9c787-108">Para obter mais informações sobre recursos de DSC, consulte [Criar recursos personalizados de configuração de estado desejado do Windows PowerShell](authoringResource.md).</span><span class="sxs-lookup"><span data-stu-id="9c787-108">For more information about DSC resources, see [Build Custom Windows PowerShell Desired State Configuration Resources](authoringResource.md).</span></span> <span data-ttu-id="9c787-109">Neste artigo, criaremos um recurso de DSC que gerencia os usuários do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9c787-109">In this article, we will create a DSC resource that manages Active Directory users.</span></span> <span data-ttu-id="9c787-110">Use o cmdlet [Install-Module](/powershell/module/PowershellGet/Install-Module) para instalar o módulo **xDscResourceDesigner**.</span><span class="sxs-lookup"><span data-stu-id="9c787-110">Use the [Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet to install the **xDscResourceDesigner** module.</span></span>

## <a name="creating-resource-properties"></a><span data-ttu-id="9c787-111">Criando propriedades de recurso</span><span class="sxs-lookup"><span data-stu-id="9c787-111">Creating resource properties</span></span>

<span data-ttu-id="9c787-112">A primeira coisa que precisamos fazer é decidir sobre as propriedades que serão expostas pelo recuso.</span><span class="sxs-lookup"><span data-stu-id="9c787-112">The first thing we need to do is decide on properties that the resource will expose.</span></span> <span data-ttu-id="9c787-113">Para esse exemplo, definiremos um usuário do Active Directory com as seguintes propriedades.</span><span class="sxs-lookup"><span data-stu-id="9c787-113">For this example, we will define an Active Directory user with the following properties.</span></span>

<span data-ttu-id="9c787-114">Nome do parâmetro Descrição</span><span class="sxs-lookup"><span data-stu-id="9c787-114">Parameter name  Description</span></span>

- <span data-ttu-id="9c787-115">**UserName** : propriedade de chave que identifica um usuário com exclusividade.</span><span class="sxs-lookup"><span data-stu-id="9c787-115">**UserName** : Key property that uniquely identifies a user.</span></span>
- <span data-ttu-id="9c787-116">**Ensure** : especifica se a conta do usuário deve ser do tipo Present ou Absent.</span><span class="sxs-lookup"><span data-stu-id="9c787-116">**Ensure** : Specifies whether the user account should be Present or Absent.</span></span> <span data-ttu-id="9c787-117">Esse parâmetro terá apenas dois valores possíveis.</span><span class="sxs-lookup"><span data-stu-id="9c787-117">This parameter will have only two possible values.</span></span>
- <span data-ttu-id="9c787-118">**DomainCredential** : a senha do domínio para o usuário.</span><span class="sxs-lookup"><span data-stu-id="9c787-118">**DomainCredential** : The domain password for the user.</span></span>
- <span data-ttu-id="9c787-119">**Password** : a senha desejada para o usuário permitir que uma configuração altere a senha do usuário, se necessário.</span><span class="sxs-lookup"><span data-stu-id="9c787-119">**Password** : The desired password for the user to allow a configuration to change the user password if necessary.</span></span>

<span data-ttu-id="9c787-120">Para criar as propriedades, usamos o cmdlet `New-xDscResourceProperty`.</span><span class="sxs-lookup"><span data-stu-id="9c787-120">To create the properties, we use the `New-xDscResourceProperty` cmdlet.</span></span> <span data-ttu-id="9c787-121">Os seguintes comandos do PowerShell criam as propriedades descritas acima.</span><span class="sxs-lookup"><span data-stu-id="9c787-121">The following PowerShell commands create the properties described above.</span></span>

```powershell
$UserName = New-xDscResourceProperty –Name UserName -Type String -Attribute Key
$Ensure = New-xDscResourceProperty –Name Ensure -Type String -Attribute Write –ValidateSet "Present", "Absent"
$DomainCredential = New-xDscResourceProperty –Name DomainCredential -Type PSCredential -Attribute Write
$Password = New-xDscResourceProperty –Name Password -Type PSCredential -Attribute Write
```

## <a name="create-the-resource"></a><span data-ttu-id="9c787-122">Criar o recurso</span><span class="sxs-lookup"><span data-stu-id="9c787-122">Create the resource</span></span>

<span data-ttu-id="9c787-123">Agora que as propriedades do recurso foram criadas, podemos chamar o cmdlet `New-xDscResource` para criar o recurso.</span><span class="sxs-lookup"><span data-stu-id="9c787-123">Now that the resource properties have been created, we can call the `New-xDscResource` cmdlet to create the resource.</span></span> <span data-ttu-id="9c787-124">O cmdlet `New-xDscResource` utiliza a lista de propriedades como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="9c787-124">The `New-xDscResource` cmdlet takes the list of properties as parameters.</span></span> <span data-ttu-id="9c787-125">Também usa o caminho no qual o módulo deve ser criado, o nome do novo recurso e o nome do módulo no qual ele está contido.</span><span class="sxs-lookup"><span data-stu-id="9c787-125">It also takes the path where the module should be created, the name of the new resource, and the name of the module in which it is contained.</span></span> <span data-ttu-id="9c787-126">O comando do PowerShell a seguir cria o recurso.</span><span class="sxs-lookup"><span data-stu-id="9c787-126">The following PowerShell command creates the resource.</span></span>

```powershell
New-xDscResource –Name Demo_ADUser –Property $UserName, $Ensure, $DomainCredential, $Password –Path 'C:\Program Files\WindowsPowerShell\Modules' –ModuleName Demo_DSCModule
```

<span data-ttu-id="9c787-127">O cmdlet `New-xDscResource` cria o esquema MOF, um script de recurso esqueleto, a estrutura de diretório necessária para o novo recurso e um manifesto para o módulo que expõe o novo recurso.</span><span class="sxs-lookup"><span data-stu-id="9c787-127">The `New-xDscResource` cmdlet creates the MOF schema, a skeleton resource script, the required directory structure for your new resource, and a manifest for the module that exposes the new resource.</span></span>

<span data-ttu-id="9c787-128">O arquivo de esquema MOF está em `C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.schema.mof`, e o conteúdo dele é descrito a seguir.</span><span class="sxs-lookup"><span data-stu-id="9c787-128">The MOF schema file is at `C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.schema.mof`, and its contents are as follows.</span></span>

```
[ClassVersion("1.0.0.0"), FriendlyName("Demo_ADUser")]
class Demo_ADUser : OMI_BaseResource
{
  [Key] string UserName;
  [Write, ValueMap{"Present","Absent"}, Values{"Present","Absent"}] string Ensure;
  [Write, EmbeddedInstance("MSFT_Credential")] String DomainCredential;
  [Write, EmbeddedInstance("MSFT_Credential")] String Password;
};
```

<span data-ttu-id="9c787-129">O script de recurso está em `C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.psm1`.</span><span class="sxs-lookup"><span data-stu-id="9c787-129">The resource script is at `C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.psm1`.</span></span>
<span data-ttu-id="9c787-130">Não inclui a lógica real para implementar o recurso, que você mesmo deve adicionar.</span><span class="sxs-lookup"><span data-stu-id="9c787-130">It does not include the actual logic to implement the resource, which you must add yourself.</span></span> <span data-ttu-id="9c787-131">O conteúdo do script esqueleto é o seguinte.</span><span class="sxs-lookup"><span data-stu-id="9c787-131">The contents of the skeleton script are as follows.</span></span>

```powershell
function Get-TargetResource
{
  [CmdletBinding()]
  [OutputType([System.Collections.Hashtable])]
  param
  (
    [parameter(Mandatory = $true)]
    [System.String]
    $UserName
  )

  #Write-Verbose "Use this cmdlet to deliver information about command processing."

  #Write-Debug "Use this cmdlet to write debug information while troubleshooting."

  <#
  $returnValue = @{
  UserName = [System.String]
  Ensure = [System.String]
  DomainAdminCredential = [System.Management.Automation.PSCredential]
  Password = [System.Management.Automation.PSCredential]
  }

  $returnValue
  #>
}

function Set-TargetResource
{
  [CmdletBinding()]
  param
  (
    [parameter(Mandatory = $true)]
    [System.String]
    $UserName,

    [ValidateSet("Present","Absent")]
    [System.String]
    $Ensure,

    [System.Management.Automation.PSCredential]
    $DomainAdminCredential,

    [System.Management.Automation.PSCredential]
    $Password
  )

  #Write-Verbose "Use this cmdlet to deliver information about command processing."

  #Write-Debug "Use this cmdlet to write debug information while troubleshooting."

  #Include this line if the resource requires a system reboot.
  #$global:DSCMachineStatus = 1
}

function Test-TargetResource
{
  [CmdletBinding()]
  [OutputType([System.Boolean])]
  param
  (
    [parameter(Mandatory = $true)]
    [System.String]
    $UserName,

    [ValidateSet("Present","Absent")]
    [System.String]
    $Ensure,

    [System.Management.Automation.PSCredential]
    $DomainAdminCredential,

    [System.Management.Automation.PSCredential]
    $Password
  )

  #Write-Verbose "Use this cmdlet to deliver information about command processing."

  #Write-Debug "Use this cmdlet to write debug information while troubleshooting."

  <#
  $result = [System.Boolean]

  $result
  #>
}

Export-ModuleMember -Function *-TargetResource
```

## <a name="updating-the-resource"></a><span data-ttu-id="9c787-132">Atualizando o recurso</span><span class="sxs-lookup"><span data-stu-id="9c787-132">Updating the resource</span></span>

<span data-ttu-id="9c787-133">Se você precisar adicionar ou modificar a lista de parâmetros do recurso, poderá chamar o cmdlet `Update-xDscResource`.</span><span class="sxs-lookup"><span data-stu-id="9c787-133">If you need to add or modify the parameter list of the resource, you can call the `Update-xDscResource` cmdlet.</span></span> <span data-ttu-id="9c787-134">O cmdlet atualiza o recurso com uma nova lista de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="9c787-134">The cmdlet updates the resource with a new parameter list.</span></span> <span data-ttu-id="9c787-135">Se você já tiver adicionado lógica no script do recurso, ele permanecerá intacto.</span><span class="sxs-lookup"><span data-stu-id="9c787-135">If you have already added logic in your resource script, it is left intact.</span></span>

<span data-ttu-id="9c787-136">Suponha, por exemplo, que você deseja incluir o horário do último logon para o usuário no nosso recurso.</span><span class="sxs-lookup"><span data-stu-id="9c787-136">For example, suppose you want to include the last log in time for the user in our resource.</span></span> <span data-ttu-id="9c787-137">Em vez de reescrever o recurso por completo, é possível chamar `New-xDscResourceProperty` para criar a propriedade e, depois, chamar `Update-xDscResource` e adicionar a nova propriedade à sua lista de propriedades.</span><span class="sxs-lookup"><span data-stu-id="9c787-137">Rather than writing the resource again completely, you can call the `New-xDscResourceProperty` to create the new property, and then call `Update-xDscResource` and add your new property to the properties list.</span></span>

```powershell
$lastLogon = New-xDscResourceProperty –Name LastLogon –Type Hashtable –Attribute Write –Description "For mapping users to their last log on time"
Update-xDscResource –Name 'Demo_ADUser' –Property $UserName, $Ensure, $DomainCredential, $Password, $lastLogon -Force
```

## <a name="testing-a-resource-schema"></a><span data-ttu-id="9c787-138">Testando um esquema de recursos</span><span class="sxs-lookup"><span data-stu-id="9c787-138">Testing a resource schema</span></span>

<span data-ttu-id="9c787-139">A ferramenta Designer de Recursos expõe mais um cmdlet que pode ser usado para testar a validade de um esquema MOF escrito manualmente.</span><span class="sxs-lookup"><span data-stu-id="9c787-139">The Resource Designer tool exposes one more cmdlet that can be used to test the validity of a MOF schema that you have written manually.</span></span> <span data-ttu-id="9c787-140">Chame o cmdlet `Test-xDscSchema`, passando o caminho de um esquema de recursos MOF como parâmetro.</span><span class="sxs-lookup"><span data-stu-id="9c787-140">Call the `Test-xDscSchema` cmdlet, passing the path of a MOF resource schema as a parameter.</span></span> <span data-ttu-id="9c787-141">O cmdlet mostrará os erros no esquema.</span><span class="sxs-lookup"><span data-stu-id="9c787-141">The cmdlet will output any errors in the schema.</span></span>

### <a name="see-also"></a><span data-ttu-id="9c787-142">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="9c787-142">See Also</span></span>

#### <a name="concepts"></a><span data-ttu-id="9c787-143">Conceitos</span><span class="sxs-lookup"><span data-stu-id="9c787-143">Concepts</span></span>

[<span data-ttu-id="9c787-144">Criar recursos personalizados de configuração de estado desejado do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c787-144">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>](authoringResource.md)

#### <a name="other-resources"></a><span data-ttu-id="9c787-145">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="9c787-145">Other Resources</span></span>

<span data-ttu-id="9c787-146">[xDscResourceDesigner Module](https://www.powershellgallery.com/packages/xDscResourceDesigner/1.12.0.0) (Módulo xDscResourceDesigner)</span><span class="sxs-lookup"><span data-stu-id="9c787-146">[xDscResourceDesigner Module](https://www.powershellgallery.com/packages/xDscResourceDesigner/1.12.0.0)</span></span>
