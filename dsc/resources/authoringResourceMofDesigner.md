---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Usando a ferramenta Designer de Recursos
ms.openlocfilehash: 3fd2f06cf46602ee30dd34f8e7bd77d3c92b808f
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53400202"
---
# <a name="using-the-resource-designer-tool"></a><span data-ttu-id="3b5c4-103">Usando a ferramenta Designer de Recursos</span><span class="sxs-lookup"><span data-stu-id="3b5c4-103">Using the Resource Designer tool</span></span>

> <span data-ttu-id="3b5c4-104">Aplica-se a: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="3b5c4-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="3b5c4-105">A ferramenta Designer de Recursos é um conjunto de cmdlets expostos pelo módulo **xDscResourceDesigner** que facilitam a criação de recursos de Configuração de Estado Desejado (DSC) do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-105">The Resource Designer tool is a set of cmdlets exposed by the **xDscResourceDesigner** module that make creating Windows PowerShell Desired State Configuration (DSC) resources easier.</span></span> <span data-ttu-id="3b5c4-106">Os cmdlets nesse recurso ajudam a criar o esquema MOF, o módulo de script e a estrutura de diretórios para seu novo recurso.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-106">The cmdlets in this resource help create the MOF schema, the script module, and the directory structure for your new resource.</span></span> <span data-ttu-id="3b5c4-107">Para obter mais informações sobre recursos de DSC, consulte [Criar recursos personalizados de configuração de estado desejado do Windows PowerShell](authoringResource.md).</span><span class="sxs-lookup"><span data-stu-id="3b5c4-107">For more information about DSC resources, see [Build Custom Windows PowerShell Desired State Configuration Resources](authoringResource.md).</span></span>
<span data-ttu-id="3b5c4-108">Neste tópico, criaremos um recurso de DSC que gerencia os usuários do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-108">In this topic, we will create a DSC resource that manages Active Directory users.</span></span>
<span data-ttu-id="3b5c4-109">Use o cmdlet [Install-Module](/powershell/module/PowershellGet/Install-Module) para instalar o módulo **xDscResourceDesigner**.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-109">Use the [Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet to install the **xDscResourceDesigner** module.</span></span>

><span data-ttu-id="3b5c4-110">**Observação**: **Install-Module** está incluído na **PowerShellGet** módulo, que está incluído no PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-110">**Note**: **Install-Module** is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="3b5c4-111">É possível baixar o módulo **PowerShellGet** para o PowerShell 3.0 e 4.0 em [Visualização de Módulos do PowerShell do PackageManagement](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span><span class="sxs-lookup"><span data-stu-id="3b5c4-111">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span>

## <a name="creating-resource-properties"></a><span data-ttu-id="3b5c4-112">Criando propriedades de recurso</span><span class="sxs-lookup"><span data-stu-id="3b5c4-112">Creating resource properties</span></span>
<span data-ttu-id="3b5c4-113">A primeira coisa que precisamos fazer é decidir sobre as propriedades que serão expostas pelo recuso.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-113">The first thing we need to do is decide on properties that the resource will expose.</span></span> <span data-ttu-id="3b5c4-114">Para esse exemplo, definiremos um usuário do Active Directory com as seguintes propriedades.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-114">For this example, we will define an Active Directory user with the following properties.</span></span>

<span data-ttu-id="3b5c4-115">Nome do parâmetro Descrição</span><span class="sxs-lookup"><span data-stu-id="3b5c4-115">Parameter name  Description</span></span>
* <span data-ttu-id="3b5c4-116">.**nome**usuário Propriedade de chave que identifica exclusivamente um usuário.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-116">**UserName**: Key property that uniquely identifies a user.</span></span>
* <span data-ttu-id="3b5c4-117">Ensure Especifica se a conta de usuário deve estar presentes ou ausentes.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-117">**Ensure**: Specifies whether the user account should be Present or Absent.</span></span> <span data-ttu-id="3b5c4-118">Esse parâmetro terá apenas dois valores possíveis.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-118">This parameter will have only two possible values.</span></span>
* <span data-ttu-id="3b5c4-119">**DomainCredential**: A senha de domínio para o usuário.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-119">**DomainCredential**: The domain password for the user.</span></span>
* <span data-ttu-id="3b5c4-120">Senha A senha desejada para o usuário Permitir que uma configuração alterar a senha do usuário, se necessário.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-120">**Password**: The desired password for the user to allow a configuration to change the user password if necessary.</span></span>

<span data-ttu-id="3b5c4-121">Para criar as propriedades, usamos o cmdlet **novo xDscResourceProperty**.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-121">To create the properties, we use the **New-xDscResourceProperty** cmdlet.</span></span> <span data-ttu-id="3b5c4-122">Os seguintes comandos do PowerShell criam as propriedades descritas acima.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-122">The following PowerShell commands create the properties described above.</span></span>

```powershell
$UserName = New-xDscResourceProperty –Name UserName -Type String -Attribute Key
$Ensure = New-xDscResourceProperty –Name Ensure -Type String -Attribute Write –ValidateSet “Present”, “Absent”
$DomainCredential = New-xDscResourceProperty –Name DomainCredential -Type PSCredential -Attribute Write
$Password = New-xDscResourceProperty –Name Password -Type PSCredential -Attribute Write
```

## <a name="create-the-resource"></a><span data-ttu-id="3b5c4-123">Criar o recurso</span><span class="sxs-lookup"><span data-stu-id="3b5c4-123">Create the resource</span></span>

<span data-ttu-id="3b5c4-124">Agora que as propriedades do recurso foram criadas, podemos chamar o cmdlet **New-xDscResource** para criar o recurso.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-124">Now that the resource properties have been created, we can call the **New-xDscResource** cmdlet to create the resource.</span></span> <span data-ttu-id="3b5c4-125">O cmdlet **New-xDscResource** utiliza a lista de propriedades como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-125">The **New-xDscResource** cmdlet takes the list of properties as parameters.</span></span> <span data-ttu-id="3b5c4-126">Também usa o caminho no qual o módulo deve ser criado, o nome do novo recurso e o nome do módulo no qual ele está contido.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-126">It also takes the path where the module should be created, the name of the new resource, and the name of the module in which it is contained.</span></span> <span data-ttu-id="3b5c4-127">O comando do PowerShell a seguir cria o recurso.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-127">The following PowerShell command creates the resource.</span></span>

```powershell
New-xDscResource –Name Demo_ADUser –Property $UserName, $Ensure, $DomainCredential, $Password –Path ‘C:\Program Files\WindowsPowerShell\Modules’ –ModuleName Demo_DSCModule
```

<span data-ttu-id="3b5c4-128">O cmdlet **New-xDscResource** cria o esquema MOF, um script de recurso esqueleto, a estrutura de diretório necessária para o novo recurso e um manifesto para o módulo que expõe o novo recurso.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-128">The **New-xDscResource** cmdlet creates the MOF schema, a skeleton resource script, the required directory structure for your new resource, and a manifest for the module that exposes the new resource.</span></span>

<span data-ttu-id="3b5c4-129">O arquivo do esquema MOF está em **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.schema.mof** e seu conteúdo é o seguinte.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-129">The MOF schema file is at **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.schema.mof**, and its contents are as follows.</span></span>

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

<span data-ttu-id="3b5c4-130">O script do recurso está em **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.psm1**.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-130">The resource script is at **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.psm1**.</span></span> <span data-ttu-id="3b5c4-131">Não inclui a lógica real para implementar o recurso, que você mesmo deve adicionar.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-131">It does not include the actual logic to implement the resource, which you must add yourself.</span></span> <span data-ttu-id="3b5c4-132">O conteúdo do script esqueleto é o seguinte.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-132">The contents of the skeleton script are as follows.</span></span>

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

## <a name="updating-the-resource"></a><span data-ttu-id="3b5c4-133">Atualizando o recurso</span><span class="sxs-lookup"><span data-stu-id="3b5c4-133">Updating the resource</span></span>

<span data-ttu-id="3b5c4-134">Se você precisar adicionar ou modificar a lista de parâmetros do recurso, poderá chamar o cmdlet **Update-xDscResource**.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-134">If you need to add or modify the parameter list of the resource, you can call the **Update-xDscResource** cmdlet.</span></span> <span data-ttu-id="3b5c4-135">O cmdlet atualiza o recurso com uma nova lista de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-135">The cmdlet updates the resource with a new parameter list.</span></span> <span data-ttu-id="3b5c4-136">Se você já tiver adicionado lógica no script do recurso, ele permanecerá intacto.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-136">If you have already added logic in your resource script, it is left intact.</span></span>

<span data-ttu-id="3b5c4-137">Suponha, por exemplo, que você deseja incluir o horário do último logon para o usuário no nosso recurso.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-137">For example, suppose you want to include the last log in time for the user in our resource.</span></span> <span data-ttu-id="3b5c4-138">Em vez de reescrever o recurso por completo, é possível chamar **New-xDscResourceProperty** para criar a nova propriedade e, depois, chamar **Update-xDscResource** e adicionar a nova propriedade à sua lista de propriedades.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-138">Rather than writing the resource again completely, you can call the **New-xDscResourceProperty** to create the new property, and then call **Update-xDscResource** and add your new property to the properties list.</span></span>

```powershell
$lastLogon = New-xDscResourceProperty –Name LastLogon –Type Hashtable –Attribute Write –Description “For mapping users to their last log on time”
Update-xDscResource –Name ‘Demo_ADUser’ –Property $UserName, $Ensure, $DomainCredential, $Password, $lastLogon -Force
```

## <a name="testing-a-resource-schema"></a><span data-ttu-id="3b5c4-139">Testando um esquema de recursos</span><span class="sxs-lookup"><span data-stu-id="3b5c4-139">Testing a resource schema</span></span>

<span data-ttu-id="3b5c4-140">A ferramenta Designer de Recursos expõe mais um cmdlet que pode ser usado para testar a validade de um esquema MOF escrito manualmente.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-140">The Resource Designer tool exposes one more cmdlet that can be used to test the validity of a MOF schema that you have written manually.</span></span> <span data-ttu-id="3b5c4-141">Chame o cmdlet **Test-xDscSchema**, passando o caminho de um esquema de recursos MOF como parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-141">Call the **Test-xDscSchema** cmdlet, passing the path of a MOF resource schema as a parameter.</span></span> <span data-ttu-id="3b5c4-142">O cmdlet mostrará os erros no esquema.</span><span class="sxs-lookup"><span data-stu-id="3b5c4-142">The cmdlet will output any errors in the schema.</span></span>

### <a name="see-also"></a><span data-ttu-id="3b5c4-143">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="3b5c4-143">See Also</span></span>

#### <a name="concepts"></a><span data-ttu-id="3b5c4-144">Conceitos</span><span class="sxs-lookup"><span data-stu-id="3b5c4-144">Concepts</span></span>
[<span data-ttu-id="3b5c4-145">Criar recursos personalizados de configuração de estado desejado do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b5c4-145">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>](authoringResource.md)

#### <a name="other-resources"></a><span data-ttu-id="3b5c4-146">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="3b5c4-146">Other Resources</span></span>
<span data-ttu-id="3b5c4-147">[xDscResourceDesigner Module](https://www.powershellgallery.com/packages/xDscResourceDesigner/1.12.0.0) (Módulo xDscResourceDesigner)</span><span class="sxs-lookup"><span data-stu-id="3b5c4-147">[xDscResourceDesigner Module](https://www.powershellgallery.com/packages/xDscResourceDesigner/1.12.0.0)</span></span>