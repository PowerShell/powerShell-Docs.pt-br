---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Método SendMetaConfigurationApply
ms.openlocfilehash: b2e420bafb8ea22aea43800f6e429d3ed785d1e8
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71954873"
---
# <a name="sendmetaconfigurationapply-method"></a><span data-ttu-id="69cd8-103">Método SendMetaConfigurationApply</span><span class="sxs-lookup"><span data-stu-id="69cd8-103">SendMetaConfigurationApply method</span></span>

<span data-ttu-id="69cd8-104">Define as configurações do Gerenciador de Configurações Local usadas para controlar o Agente de Configuração.</span><span class="sxs-lookup"><span data-stu-id="69cd8-104">Sets the Local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

## <a name="syntax"></a><span data-ttu-id="69cd8-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="69cd8-105">Syntax</span></span>

```mof
uint32 SendMetaConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="69cd8-106">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="69cd8-106">Parameters</span></span>

<span data-ttu-id="69cd8-107">*ConfigurationData* \[in\] Dados de ambiente da configuração.</span><span class="sxs-lookup"><span data-stu-id="69cd8-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="69cd8-108">*force* \[in\] **true** para forçar a configuração a parar.</span><span class="sxs-lookup"><span data-stu-id="69cd8-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="69cd8-109">Retornar valor</span><span class="sxs-lookup"><span data-stu-id="69cd8-109">Return value</span></span>

<span data-ttu-id="69cd8-110">Retorna zero em caso de êxito; caso contrário, retorna um código de erro.</span><span class="sxs-lookup"><span data-stu-id="69cd8-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="69cd8-111">Comentários</span><span class="sxs-lookup"><span data-stu-id="69cd8-111">Remarks</span></span>

<span data-ttu-id="69cd8-112">Esse é um método estático.</span><span class="sxs-lookup"><span data-stu-id="69cd8-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="69cd8-113">Requisitos</span><span class="sxs-lookup"><span data-stu-id="69cd8-113">Requirements</span></span>

<span data-ttu-id="69cd8-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="69cd8-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="69cd8-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="69cd8-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="69cd8-116">Consulte também</span><span class="sxs-lookup"><span data-stu-id="69cd8-116">See also</span></span>

[<span data-ttu-id="69cd8-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="69cd8-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
