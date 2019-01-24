---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Método GetConfiguration da classe MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: ae31ac30c152c96707b764ddaf00c924806afcfc
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54047087"
---
# <a name="getconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="3fce0-103">Método GetConfiguration da classe MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="3fce0-103">GetConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="3fce0-104">Envia o documento de configuração para o nó gerenciado e usa o método **Get** do Agente de Configuração para aplicar a configuração.</span><span class="sxs-lookup"><span data-stu-id="3fce0-104">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="3fce0-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="3fce0-105">Syntax</span></span>

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

## <a name="parameters"></a><span data-ttu-id="3fce0-106">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="3fce0-106">Parameters</span></span>

<span data-ttu-id="3fce0-107">*configurationData* \[in\] Especifica os dados de configuração para envio.</span><span class="sxs-lookup"><span data-stu-id="3fce0-107">*configurationData* \[in\] Specifies the configuration data to send.</span></span>

<span data-ttu-id="3fce0-108">*configurations* \[out\] No retorno, contém uma instância inserida das configurações.</span><span class="sxs-lookup"><span data-stu-id="3fce0-108">*configurations* \[out\] On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="3fce0-109">Retornar valor</span><span class="sxs-lookup"><span data-stu-id="3fce0-109">Return value</span></span>

<span data-ttu-id="3fce0-110">Retorna zero em caso de êxito; caso contrário, retorna um código de erro.</span><span class="sxs-lookup"><span data-stu-id="3fce0-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="3fce0-111">Comentários</span><span class="sxs-lookup"><span data-stu-id="3fce0-111">Remarks</span></span>

<span data-ttu-id="3fce0-112">Esse é um método estático.</span><span class="sxs-lookup"><span data-stu-id="3fce0-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="3fce0-113">Requisitos</span><span class="sxs-lookup"><span data-stu-id="3fce0-113">Requirements</span></span>

<span data-ttu-id="3fce0-114">MOF\*\* DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="3fce0-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="3fce0-115">namespace {0} Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="3fce0-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="3fce0-116">Consulte também</span><span class="sxs-lookup"><span data-stu-id="3fce0-116">See also</span></span>

[<span data-ttu-id="3fce0-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="3fce0-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)