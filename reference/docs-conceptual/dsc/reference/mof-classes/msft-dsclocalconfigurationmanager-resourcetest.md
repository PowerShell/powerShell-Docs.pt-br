---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Método ResourceTest
ms.openlocfilehash: ff06fd645a94055e79aa0f8d20f2f06e16483720
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71954943"
---
# <a name="resourcetest-method"></a><span data-ttu-id="29c8e-103">Método ResourceTest</span><span class="sxs-lookup"><span data-stu-id="29c8e-103">ResourceTest method</span></span>

<span data-ttu-id="29c8e-104">Chama diretamente o método **Test** de um recurso de DSC.</span><span class="sxs-lookup"><span data-stu-id="29c8e-104">Directly calls the **Test** method of a DSC resource.</span></span>

## <a name="syntax"></a><span data-ttu-id="29c8e-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="29c8e-105">Syntax</span></span>

```mof
uint32 ResourceTest(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean InDesiredState
);
```

## <a name="parameters"></a><span data-ttu-id="29c8e-106">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="29c8e-106">Parameters</span></span>

<span data-ttu-id="29c8e-107">*ResourceType* \[in\] O nome do recurso a chamar.</span><span class="sxs-lookup"><span data-stu-id="29c8e-107">*ResourceType* \[in\] The name of the resource to call.</span></span>

<span data-ttu-id="29c8e-108">*ModuleName* \[in\] O nome do módulo que contém o recurso a chamar.</span><span class="sxs-lookup"><span data-stu-id="29c8e-108">*ModuleName* \[in\] The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="29c8e-109">*resourceProperty* \[in\] Especifica o nome da propriedade do recurso e o respectivo valor em uma tabela de hash como chave e valor, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="29c8e-109">*resourceProperty* \[in\] Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="29c8e-110">Use o cmdlet [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) para descobrir as propriedades de recurso e seus tipos.</span><span class="sxs-lookup"><span data-stu-id="29c8e-110">Use the [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="29c8e-111">*InDesiredState* \[out\] No retorno, essa propriedade será definida como **true** se o nó de destino estiver no estado desejado.</span><span class="sxs-lookup"><span data-stu-id="29c8e-111">*InDesiredState* \[out\] On return, this property is set to **true** if the target node is in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="29c8e-112">Retornar valor</span><span class="sxs-lookup"><span data-stu-id="29c8e-112">Return value</span></span>

<span data-ttu-id="29c8e-113">Retorna zero em caso de êxito; caso contrário, retorna um código de erro.</span><span class="sxs-lookup"><span data-stu-id="29c8e-113">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="29c8e-114">Comentários</span><span class="sxs-lookup"><span data-stu-id="29c8e-114">Remarks</span></span>

<span data-ttu-id="29c8e-115">Esse é um método estático.</span><span class="sxs-lookup"><span data-stu-id="29c8e-115">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="29c8e-116">Requisitos</span><span class="sxs-lookup"><span data-stu-id="29c8e-116">Requirements</span></span>

<span data-ttu-id="29c8e-117">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="29c8e-117">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="29c8e-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="29c8e-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="29c8e-119">Consulte também</span><span class="sxs-lookup"><span data-stu-id="29c8e-119">See also</span></span>

[<span data-ttu-id="29c8e-120">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="29c8e-120">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
