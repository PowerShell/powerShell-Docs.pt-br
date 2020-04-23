---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Chamando métodos do recurso DSC diretamente
ms.openlocfilehash: cf237f638593706e5959e2bcc0d851b0e55baf0e
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2020
ms.locfileid: "71954383"
---
# <a name="calling-dsc-resource-methods-directly"></a><span data-ttu-id="21a5d-103">Chamando métodos do recurso DSC diretamente</span><span class="sxs-lookup"><span data-stu-id="21a5d-103">Calling DSC resource methods directly</span></span>

><span data-ttu-id="21a5d-104">Aplica-se a: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="21a5d-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="21a5d-105">Você pode usar o cmdlet [Invoke-DscResource](/powershell/module/PSDesiredStateConfiguration/Invoke-DscResource) para chamar diretamente as funções ou os métodos de um recurso DSC (As funções **Get-TargetResource**, **Set-TargetResource** e **Test-TargetResource** de um recurso baseado em MOF ou os métodos **Get**, **Set** e **Test** de um recurso baseado em classe).</span><span class="sxs-lookup"><span data-stu-id="21a5d-105">You can use the [Invoke-DscResource](/powershell/module/PSDesiredStateConfiguration/Invoke-DscResource) cmdlet to directly call the functions or methods of a DSC resource (The **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** functions of a MOF-based resource, or the **Get**, **Set**, and **Test** methods of a class-based resource).</span></span>
<span data-ttu-id="21a5d-106">Isso pode ser usado por terceiros que querem usar recursos DSC, ou como uma ferramenta útil ao desenvolver recursos.</span><span class="sxs-lookup"><span data-stu-id="21a5d-106">This can be used by third-parties that want to use DSC resources, or as a helpful tool while developing resources.</span></span>

<span data-ttu-id="21a5d-107">Geralmente, esse cmdlet é usado em combinação com uma propriedade de metaconfiguração `refreshMode = 'Disabled'`, mas pode ser usado, independentemente do **refreshMode** para o qual está definido.</span><span class="sxs-lookup"><span data-stu-id="21a5d-107">This cmdlet is typically used in combination with a metaconfiguration property `refreshMode = 'Disabled'`, but it can be used no matter what **refreshMode** is set to.</span></span>

<span data-ttu-id="21a5d-108">Ao chamar o cmdlet **Invoke-DscResource**, você especifica qual método ou função chamar usando o parâmetro **Method**.</span><span class="sxs-lookup"><span data-stu-id="21a5d-108">When calling the **Invoke-DscResource** cmdlet, you specify which method or function to call by using the **Method** parameter.</span></span> <span data-ttu-id="21a5d-109">Especifique as propriedades do recurso passando uma tabela de hash como o valor do parâmetro **Property**.</span><span class="sxs-lookup"><span data-stu-id="21a5d-109">You specify the properties of the resource by passing a hashtable as the value of the **Property** parameter.</span></span>

<span data-ttu-id="21a5d-110">A seguir, exemplos de chamada direta aos métodos do recurso:</span><span class="sxs-lookup"><span data-stu-id="21a5d-110">The following are examples of directly calling resource methods:</span></span>

## <a name="ensure-a-file-is-present"></a><span data-ttu-id="21a5d-111">Certificar-se de que um arquivo está presente</span><span class="sxs-lookup"><span data-stu-id="21a5d-111">Ensure a file is present</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Set -Property @{
                            DestinationPath = "$env:SystemDrive\\DirectAccess.txt";
                            Contents = 'This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="test-that-a-file-is-present"></a><span data-ttu-id="21a5d-112">Testar se um arquivo está presente</span><span class="sxs-lookup"><span data-stu-id="21a5d-112">Test that a file is present</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Test -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="get-the-contents-of-file"></a><span data-ttu-id="21a5d-113">Obter o conteúdo do arquivo</span><span class="sxs-lookup"><span data-stu-id="21a5d-113">Get the contents of file</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Get -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result.ItemValue | fl
```

><span data-ttu-id="21a5d-114">**Observação:** não é permitido chamar diretamente métodos de recurso de composição.</span><span class="sxs-lookup"><span data-stu-id="21a5d-114">**Note:** Directly calling composite resource methods is not supported.</span></span> <span data-ttu-id="21a5d-115">Em vez disso, chame os métodos de recursos subjacentes que compõem o recurso de composição.</span><span class="sxs-lookup"><span data-stu-id="21a5d-115">Instead, call the methods of the underlying resources that make up the composite resource.</span></span>

## <a name="see-also"></a><span data-ttu-id="21a5d-116">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="21a5d-116">See Also</span></span>
- [<span data-ttu-id="21a5d-117">Escrevendo um recurso personalizado de DSC com MOF</span><span class="sxs-lookup"><span data-stu-id="21a5d-117">Writing a custom DSC resource with MOF</span></span>](../resources/authoringResourceMOF.md)
- [<span data-ttu-id="21a5d-118">Escrevendo um recurso personalizado de DSC com classes do PowerShell</span><span class="sxs-lookup"><span data-stu-id="21a5d-118">Writing a custom DSC resource with PowerShell classes</span></span>](../resources/authoringResourceClass.md)
- [<span data-ttu-id="21a5d-119">Depurando os recursos de DSC</span><span class="sxs-lookup"><span data-stu-id="21a5d-119">Debugging DSC resources</span></span>](../troubleshooting/debugResource.md)