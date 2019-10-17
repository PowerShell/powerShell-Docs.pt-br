---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Método GetConfiguration
ms.openlocfilehash: eabc536cfe69abe1144ff031a6f64c09a772e638
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955043"
---
# <a name="getconfiguration-method"></a><span data-ttu-id="874d4-103">Método GetConfiguration</span><span class="sxs-lookup"><span data-stu-id="874d4-103">GetConfiguration method</span></span>

<span data-ttu-id="874d4-104">Envia o documento de configuração para o nó gerenciado e usa o método **Get** do Agente de Configuração para aplicar a configuração.</span><span class="sxs-lookup"><span data-stu-id="874d4-104">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="874d4-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="874d4-105">Syntax</span></span>

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

## <a name="parameters"></a><span data-ttu-id="874d4-106">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="874d4-106">Parameters</span></span>

<span data-ttu-id="874d4-107">*configurationData* \[in\] Especifica os dados de configuração para envio.</span><span class="sxs-lookup"><span data-stu-id="874d4-107">*configurationData* \[in\] Specifies the configuration data to send.</span></span>

<span data-ttu-id="874d4-108">*configurations* \[out\] No retorno, contém uma instância inserida das configurações.</span><span class="sxs-lookup"><span data-stu-id="874d4-108">*configurations* \[out\] On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="874d4-109">Retornar valor</span><span class="sxs-lookup"><span data-stu-id="874d4-109">Return value</span></span>

<span data-ttu-id="874d4-110">Retorna zero em caso de êxito; caso contrário, retorna um código de erro.</span><span class="sxs-lookup"><span data-stu-id="874d4-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="874d4-111">Comentários</span><span class="sxs-lookup"><span data-stu-id="874d4-111">Remarks</span></span>

<span data-ttu-id="874d4-112">Esse é um método estático.</span><span class="sxs-lookup"><span data-stu-id="874d4-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="874d4-113">Requisitos</span><span class="sxs-lookup"><span data-stu-id="874d4-113">Requirements</span></span>

<span data-ttu-id="874d4-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="874d4-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="874d4-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="874d4-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="874d4-116">Consulte também</span><span class="sxs-lookup"><span data-stu-id="874d4-116">See also</span></span>

[<span data-ttu-id="874d4-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="874d4-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)