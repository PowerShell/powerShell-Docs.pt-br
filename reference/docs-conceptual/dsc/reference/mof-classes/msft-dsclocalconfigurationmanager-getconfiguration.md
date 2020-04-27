---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Método GetConfiguration
ms.openlocfilehash: eabc536cfe69abe1144ff031a6f64c09a772e638
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2020
ms.locfileid: "71955043"
---
# <a name="getconfiguration-method"></a><span data-ttu-id="d8493-103">Método GetConfiguration</span><span class="sxs-lookup"><span data-stu-id="d8493-103">GetConfiguration method</span></span>

<span data-ttu-id="d8493-104">Envia o documento de configuração para o nó gerenciado e usa o método **Get** do Agente de Configuração para aplicar a configuração.</span><span class="sxs-lookup"><span data-stu-id="d8493-104">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="d8493-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="d8493-105">Syntax</span></span>

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

## <a name="parameters"></a><span data-ttu-id="d8493-106">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="d8493-106">Parameters</span></span>

<span data-ttu-id="d8493-107">*configurationData* \[in\] Especifica os dados de configuração para envio.</span><span class="sxs-lookup"><span data-stu-id="d8493-107">*configurationData* \[in\] Specifies the configuration data to send.</span></span>

<span data-ttu-id="d8493-108">*configurations* \[out\] No retorno, contém uma instância inserida das configurações.</span><span class="sxs-lookup"><span data-stu-id="d8493-108">*configurations* \[out\] On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="d8493-109">Valor retornado</span><span class="sxs-lookup"><span data-stu-id="d8493-109">Return value</span></span>

<span data-ttu-id="d8493-110">Retorna zero em caso de êxito; caso contrário, retorna um código de erro.</span><span class="sxs-lookup"><span data-stu-id="d8493-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="d8493-111">Comentários</span><span class="sxs-lookup"><span data-stu-id="d8493-111">Remarks</span></span>

<span data-ttu-id="d8493-112">Esse é um método estático.</span><span class="sxs-lookup"><span data-stu-id="d8493-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="d8493-113">Requisitos</span><span class="sxs-lookup"><span data-stu-id="d8493-113">Requirements</span></span>

<span data-ttu-id="d8493-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="d8493-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="d8493-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="d8493-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="d8493-116">Confira também</span><span class="sxs-lookup"><span data-stu-id="d8493-116">See also</span></span>

[<span data-ttu-id="d8493-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="d8493-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
