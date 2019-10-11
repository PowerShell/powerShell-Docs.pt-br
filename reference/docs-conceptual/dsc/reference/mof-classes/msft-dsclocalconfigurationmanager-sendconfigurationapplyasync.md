---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Método SendConfigurationApplyAsync
ms.openlocfilehash: c0e6dc9418757ee719e848fa8e7006dd73d91ad8
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71953373"
---
# <a name="sendconfigurationapplyasync-method"></a><span data-ttu-id="09ae3-103">Método SendConfigurationApplyAsync</span><span class="sxs-lookup"><span data-stu-id="09ae3-103">SendConfigurationApplyAsync method</span></span>

<span data-ttu-id="09ae3-104">Envia o documento de configuração de maneira assíncrona para o nó gerenciado e usa o Agente de Configuração para aplicar a configuração.</span><span class="sxs-lookup"><span data-stu-id="09ae3-104">Sends the configuration document asynchronously to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="09ae3-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="09ae3-105">Syntax</span></span>

```mof
uint32 SendConfigurationApplyAsync(
  [in] uint8   ConfigurationData[],
  [in] boolean force,
  [in] string  jobId
);
```

## <a name="parameters"></a><span data-ttu-id="09ae3-106">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="09ae3-106">Parameters</span></span>

<span data-ttu-id="09ae3-107">*ConfigurationData* \[in\] Dados de ambiente da configuração.</span><span class="sxs-lookup"><span data-stu-id="09ae3-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="09ae3-108">*force* \[in\] **true** para forçar a configuração a parar.</span><span class="sxs-lookup"><span data-stu-id="09ae3-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

<span data-ttu-id="09ae3-109">*jobId* \[in\] A ID do trabalho para a qual enviar a configuração.</span><span class="sxs-lookup"><span data-stu-id="09ae3-109">*jobId* \[in\] The ID of the job for which to send the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="09ae3-110">Retornar valor</span><span class="sxs-lookup"><span data-stu-id="09ae3-110">Return value</span></span>

<span data-ttu-id="09ae3-111">Retorna zero em caso de êxito; caso contrário, retorna um código de erro.</span><span class="sxs-lookup"><span data-stu-id="09ae3-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="09ae3-112">Comentários</span><span class="sxs-lookup"><span data-stu-id="09ae3-112">Remarks</span></span>

<span data-ttu-id="09ae3-113">Esse é um método estático.</span><span class="sxs-lookup"><span data-stu-id="09ae3-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="09ae3-114">Requisitos</span><span class="sxs-lookup"><span data-stu-id="09ae3-114">Requirements</span></span>

<span data-ttu-id="09ae3-115">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="09ae3-115">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="09ae3-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="09ae3-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="09ae3-117">Consulte também</span><span class="sxs-lookup"><span data-stu-id="09ae3-117">See also</span></span>

[<span data-ttu-id="09ae3-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="09ae3-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
