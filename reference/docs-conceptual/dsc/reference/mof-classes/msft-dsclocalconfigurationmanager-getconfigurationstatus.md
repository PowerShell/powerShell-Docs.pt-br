---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Método GetConfigurationStatus
ms.openlocfilehash: 83b30ba2612d962fcf2fa658d07d18fb2d91ccc7
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955013"
---
# <a name="getconfigurationstatus-method"></a><span data-ttu-id="e6e41-103">Método GetConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="e6e41-103">GetConfigurationStatus method</span></span>

<span data-ttu-id="e6e41-104">Obtém o histórico do status de configuração.</span><span class="sxs-lookup"><span data-stu-id="e6e41-104">Get the configuration status history.</span></span>

## <a name="syntax"></a><span data-ttu-id="e6e41-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="e6e41-105">Syntax</span></span>

```mof
uint32 GetConfigurationStatus(
  [in]  boolean                     All,
  [out] MSFT_DSCConfigurationStatus configurationStatus[]
);
```

## <a name="parameters"></a><span data-ttu-id="e6e41-106">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="e6e41-106">Parameters</span></span>

<span data-ttu-id="e6e41-107">*All* \[in\] **true** caso esse método deva retornar informações sobre todos as configurações executadas no computador, inclusive a configuração de aplicativo e a verificação de consistência.</span><span class="sxs-lookup"><span data-stu-id="e6e41-107">*All* \[in\] **true** if this method should return information about all the configuration runs on the machine, including the configuration application and the consistency check.</span></span>

<span data-ttu-id="e6e41-108">*configurationStatus* \[out\] No retorno, contém uma instância inserida da classe **MSFT_DSCConfigurationStatus** que define as configurações.</span><span class="sxs-lookup"><span data-stu-id="e6e41-108">*configurationStatus* \[out\] On return, contains an embedded instance of the **MSFT_DSCConfigurationStatus** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="e6e41-109">Retornar valor</span><span class="sxs-lookup"><span data-stu-id="e6e41-109">Return value</span></span>

<span data-ttu-id="e6e41-110">Retorna zero em caso de êxito; caso contrário, retorna um código de erro.</span><span class="sxs-lookup"><span data-stu-id="e6e41-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="e6e41-111">Comentários</span><span class="sxs-lookup"><span data-stu-id="e6e41-111">Remarks</span></span>

<span data-ttu-id="e6e41-112">Esse é um método estático.</span><span class="sxs-lookup"><span data-stu-id="e6e41-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="e6e41-113">Requisitos</span><span class="sxs-lookup"><span data-stu-id="e6e41-113">Requirements</span></span>

<span data-ttu-id="e6e41-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="e6e41-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="e6e41-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="e6e41-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="e6e41-116">Consulte também</span><span class="sxs-lookup"><span data-stu-id="e6e41-116">See also</span></span>

[<span data-ttu-id="e6e41-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="e6e41-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)