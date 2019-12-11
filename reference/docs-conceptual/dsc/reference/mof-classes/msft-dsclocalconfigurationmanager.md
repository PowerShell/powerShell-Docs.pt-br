---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Classe MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 09b30edd48384c0e8412e0e6ee926a719249c5b8
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "71953263"
---
# <a name="msft_dsclocalconfigurationmanager-class"></a><span data-ttu-id="359d5-103">Classe MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="359d5-103">MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="359d5-104">O LCM (Gerenciador de Configurações Local) que controla os estados dos arquivos de configuração e usa o Agente de Configuração para aplicar as configurações.</span><span class="sxs-lookup"><span data-stu-id="359d5-104">The Local Configuration Manager (LCM) that controls the states of configuration files and uses Configuration Agent to apply the configurations.</span></span>

<span data-ttu-id="359d5-105">A sintaxe a seguir é simplificada do código MOF (Managed Object Format) e inclui todas as propriedades herdadas.</span><span class="sxs-lookup"><span data-stu-id="359d5-105">The following syntax is simplified from Managed Object Format (MOF) code and includes all of the inherited properties.</span></span>

## <a name="syntax"></a><span data-ttu-id="359d5-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="359d5-106">Syntax</span></span>

```
[ClassVersion("1.0.0"), dynamic, provider("dsccore"), AMENDMENT]
class MSFT_DSCLocalConfigurationManager
{
};
```

## <a name="members"></a><span data-ttu-id="359d5-107">Membros</span><span class="sxs-lookup"><span data-stu-id="359d5-107">Members</span></span>

<span data-ttu-id="359d5-108">A classe **MSFT_DSCLocalConfigurationManager** tem os seguintes membros:</span><span class="sxs-lookup"><span data-stu-id="359d5-108">The **MSFT_DSCLocalConfigurationManager** class has the following members:</span></span>

- <span data-ttu-id="359d5-109">[Métodos][]</span><span class="sxs-lookup"><span data-stu-id="359d5-109">[Methods][]</span></span>

### <a name="methods"></a><span data-ttu-id="359d5-110">Métodos</span><span class="sxs-lookup"><span data-stu-id="359d5-110">Methods</span></span>

<span data-ttu-id="359d5-111">A classe **MSFT_DSCLocalConfigurationManager** tem os métodos a seguir.</span><span class="sxs-lookup"><span data-stu-id="359d5-111">The **MSFT_DSCLocalConfigurationManager** class has these methods.</span></span>

|<span data-ttu-id="359d5-112">Método</span><span class="sxs-lookup"><span data-stu-id="359d5-112">Method</span></span> |<span data-ttu-id="359d5-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="359d5-113">Description</span></span> |
|:--- |:---|
| [<span data-ttu-id="359d5-114">ApplyConfiguration</span><span class="sxs-lookup"><span data-stu-id="359d5-114">ApplyConfiguration</span></span>](msft-dsclocalconfigurationmanager-applyconfiguration.md)| <span data-ttu-id="359d5-115">Usa o Agente de Configuração para aplicar a configuração pendente.</span><span class="sxs-lookup"><span data-stu-id="359d5-115">Uses the Configuration Agent to apply the configuration that is pending.</span></span>|
| [<span data-ttu-id="359d5-116">DisableDebugConfiguration</span><span class="sxs-lookup"><span data-stu-id="359d5-116">DisableDebugConfiguration</span></span>](msft-dsclocalconfigurationmanager-disabledebugconfiguration.md)| <span data-ttu-id="359d5-117">Desabilita a depuração do recurso DSC.</span><span class="sxs-lookup"><span data-stu-id="359d5-117">Disables DSC resource debugging.</span></span>|
| [<span data-ttu-id="359d5-118">EnableDebugConfiguration</span><span class="sxs-lookup"><span data-stu-id="359d5-118">EnableDebugConfiguration</span></span>](msft-dsclocalconfigurationmanager-enabledebugconfiguration.md)| <span data-ttu-id="359d5-119">Habilita a depuração do recurso DSC.</span><span class="sxs-lookup"><span data-stu-id="359d5-119">Enables DSC resource debugging.</span></span>|
| [<span data-ttu-id="359d5-120">GetConfiguration</span><span class="sxs-lookup"><span data-stu-id="359d5-120">GetConfiguration</span></span>](msft-dsclocalconfigurationmanager-getconfiguration.md)| <span data-ttu-id="359d5-121">Envia o documento de configuração para o nó gerenciado e usa o método **Get** do Agente de Configuração para aplicar a configuração.</span><span class="sxs-lookup"><span data-stu-id="359d5-121">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>|
| [<span data-ttu-id="359d5-122">GetConfigurationResultOutput</span><span class="sxs-lookup"><span data-stu-id="359d5-122">GetConfigurationResultOutput</span></span>](msft-dsclocalconfigurationmanager-getconfigurationresultoutput.md)| <span data-ttu-id="359d5-123">Obtém a saída do Agente de Configuração relacionada a um trabalho específico.</span><span class="sxs-lookup"><span data-stu-id="359d5-123">Gets the Configuration Agent output relating to a specific job.</span></span>|
| [<span data-ttu-id="359d5-124">GetConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="359d5-124">GetConfigurationStatus</span></span>](msft-dsclocalconfigurationmanager-getconfigurationstatus.md)| <span data-ttu-id="359d5-125">Obtém o histórico do status de configuração.</span><span class="sxs-lookup"><span data-stu-id="359d5-125">Get the configuration status history.</span></span>|
| [<span data-ttu-id="359d5-126">GetMetaConfiguration</span><span class="sxs-lookup"><span data-stu-id="359d5-126">GetMetaConfiguration</span></span>](msft-dsclocalconfigurationmanager-getmetaconfiguration.md)| <span data-ttu-id="359d5-127">Obtém as configurações LCM que são usadas para controlar o Agente de Configuração.</span><span class="sxs-lookup"><span data-stu-id="359d5-127">Gets the LCM settings that are used to control Configuration Agent.</span></span>|
| [<span data-ttu-id="359d5-128">PerformRequiredConfigurationChecks</span><span class="sxs-lookup"><span data-stu-id="359d5-128">PerformRequiredConfigurationChecks</span></span>](msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks.md)| <span data-ttu-id="359d5-129">Inicia a verificação de consistência.</span><span class="sxs-lookup"><span data-stu-id="359d5-129">Starts the consistency check.</span></span>|
| [<span data-ttu-id="359d5-130">RemoveConfiguration</span><span class="sxs-lookup"><span data-stu-id="359d5-130">RemoveConfiguration</span></span>](msft-dsclocalconfigurationmanager-removeconfiguration.md)| <span data-ttu-id="359d5-131">Remove os arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="359d5-131">Removes the configuration files.</span></span>|
| [<span data-ttu-id="359d5-132">ResourceGet</span><span class="sxs-lookup"><span data-stu-id="359d5-132">ResourceGet</span></span>](msft-dsclocalconfigurationmanager-resourceget.md)| <span data-ttu-id="359d5-133">Chama diretamente o método **Get** de um recurso de DSC.</span><span class="sxs-lookup"><span data-stu-id="359d5-133">Directly calls the **Get** method of a DSC resource.</span></span>|
| [<span data-ttu-id="359d5-134">ResourceSet</span><span class="sxs-lookup"><span data-stu-id="359d5-134">ResourceSet</span></span>](msft-dsclocalconfigurationmanager-resourceset.md)| <span data-ttu-id="359d5-135">Chama diretamente o método **Set** de um recurso de DSC.</span><span class="sxs-lookup"><span data-stu-id="359d5-135">Directly calls the **Set** method of a DSC resource.</span></span>|
| [<span data-ttu-id="359d5-136">ResourceTest</span><span class="sxs-lookup"><span data-stu-id="359d5-136">ResourceTest</span></span>](msft-dsclocalconfigurationmanager-resourcetest.md)| <span data-ttu-id="359d5-137">Chama diretamente o método **Test** de um recurso de DSC.</span><span class="sxs-lookup"><span data-stu-id="359d5-137">Directly calls the **Test** method of a DSC resource.</span></span>|
| [<span data-ttu-id="359d5-138">Reversão</span><span class="sxs-lookup"><span data-stu-id="359d5-138">RollBack</span></span>](msft-dsclocalconfigurationmanager-rollback.md)| <span data-ttu-id="359d5-139">Reverte a uma configuração anterior.</span><span class="sxs-lookup"><span data-stu-id="359d5-139">Rolls back to a previous configuration.</span></span>|
| [<span data-ttu-id="359d5-140">SendConfiguration</span><span class="sxs-lookup"><span data-stu-id="359d5-140">SendConfiguration</span></span>](msft-dsclocalconfigurationmanager-sendconfiguration.md)| <span data-ttu-id="359d5-141">Envia o documento de configuração para o nó gerenciado e o salva como alteração pendente.</span><span class="sxs-lookup"><span data-stu-id="359d5-141">Sends the configuration document to the managed node and saves it as a pending change.</span></span>|
| [<span data-ttu-id="359d5-142">SendConfigurationApply</span><span class="sxs-lookup"><span data-stu-id="359d5-142">SendConfigurationApply</span></span>](msft-dsclocalconfigurationmanager-sendconfigurationapply.md)| <span data-ttu-id="359d5-143">Envia o documento de configuração para o nó gerenciado e usa o Agente de Configuração para aplicar a configuração.</span><span class="sxs-lookup"><span data-stu-id="359d5-143">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>|
| [<span data-ttu-id="359d5-144">SendConfigurationApplyAsync</span><span class="sxs-lookup"><span data-stu-id="359d5-144">SendConfigurationApplyAsync</span></span>](msft-dsclocalconfigurationmanager-sendconfigurationapplyasync.md)| <span data-ttu-id="359d5-145">Envia o documento de configuração para o nó gerenciado e começa a usar o Agente de Configuração para aplicar a configuração.</span><span class="sxs-lookup"><span data-stu-id="359d5-145">Send the configuration document to the managed node and start using the Configuration Agent to apply the configuration.</span></span> <span data-ttu-id="359d5-146">Use GetConfigurationResultOutput para recuperar a saída do resultado.</span><span class="sxs-lookup"><span data-stu-id="359d5-146">Use GetConfigurationResultOutput to retrieve result output.</span></span>|
| [<span data-ttu-id="359d5-147">SendMetaConfigurationApply</span><span class="sxs-lookup"><span data-stu-id="359d5-147">SendMetaConfigurationApply</span></span>](msft-dsclocalconfigurationmanager-sendmetaconfigurationapply.md)| <span data-ttu-id="359d5-148">Obtém as configurações de LCM que são usadas para controlar o Agente de Configuração.</span><span class="sxs-lookup"><span data-stu-id="359d5-148">Sets the LCM settings that are used to control the Configuration Agent.</span></span>|
| [<span data-ttu-id="359d5-149">StopConfiguration</span><span class="sxs-lookup"><span data-stu-id="359d5-149">StopConfiguration</span></span>](msft-dsclocalconfigurationmanager-stopconfiguration.md)| <span data-ttu-id="359d5-150">Interrompe a configuração em andamento.</span><span class="sxs-lookup"><span data-stu-id="359d5-150">Stops the configuration that is in progress.</span></span>|
| [<span data-ttu-id="359d5-151">TestConfiguration</span><span class="sxs-lookup"><span data-stu-id="359d5-151">TestConfiguration</span></span>](msft-dsclocalconfigurationmanager-testconfiguration.md)| <span data-ttu-id="359d5-152">Envia o documento de configuração para o nó gerenciado e verifica a configuração atual de acordo com o documento.</span><span class="sxs-lookup"><span data-stu-id="359d5-152">Sends the configuration document to the managed node and verifies the current configuration against the document.</span></span>|

## <a name="requirements"></a><span data-ttu-id="359d5-153">Requisitos</span><span class="sxs-lookup"><span data-stu-id="359d5-153">Requirements</span></span>

<span data-ttu-id="359d5-154">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="359d5-154">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="359d5-155">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="359d5-155">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>
