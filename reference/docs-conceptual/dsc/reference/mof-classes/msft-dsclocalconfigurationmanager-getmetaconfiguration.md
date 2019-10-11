---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Método GetMetaConfiguration
ms.openlocfilehash: bd280cb8ebd7b0522e4e01cbd24bd9bdcfddf4c2
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71953403"
---
# <a name="getmetaconfiguration-method"></a><span data-ttu-id="df478-103">Método GetMetaConfiguration</span><span class="sxs-lookup"><span data-stu-id="df478-103">GetMetaConfiguration method</span></span>

<span data-ttu-id="df478-104">Obtém as configurações do Gerenciador de Configurações Local usadas para controlar o Agente de Configuração.</span><span class="sxs-lookup"><span data-stu-id="df478-104">Gets the local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

## <a name="syntax"></a><span data-ttu-id="df478-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="df478-105">Syntax</span></span>

```mof
uint32 GetMetaConfiguration(
  [out] MSFT_DSCMetaConfiguration MetaConfiguration
);
```

## <a name="parameters"></a><span data-ttu-id="df478-106">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="df478-106">Parameters</span></span>

<span data-ttu-id="df478-107">*MetaConfiguration* \[out\] No retorno, contém uma instância inserida da classe **MSFT_DSCMetaConfiguration** que define as configurações.</span><span class="sxs-lookup"><span data-stu-id="df478-107">*MetaConfiguration* \[out\] On return, contains an embedded instance of the **MSFT_DSCMetaConfiguration** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="df478-108">Retornar valor</span><span class="sxs-lookup"><span data-stu-id="df478-108">Return value</span></span>

<span data-ttu-id="df478-109">Retorna zero em caso de êxito; caso contrário, retorna um código de erro.</span><span class="sxs-lookup"><span data-stu-id="df478-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="df478-110">Comentários</span><span class="sxs-lookup"><span data-stu-id="df478-110">Remarks</span></span>

<span data-ttu-id="df478-111">Esse é um método estático.</span><span class="sxs-lookup"><span data-stu-id="df478-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="df478-112">Requisitos</span><span class="sxs-lookup"><span data-stu-id="df478-112">Requirements</span></span>

<span data-ttu-id="df478-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="df478-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="df478-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="df478-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="df478-115">Consulte também</span><span class="sxs-lookup"><span data-stu-id="df478-115">See also</span></span>

[<span data-ttu-id="df478-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="df478-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
