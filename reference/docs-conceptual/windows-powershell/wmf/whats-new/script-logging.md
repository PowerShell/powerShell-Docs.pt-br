---
ms.date: 06/12/2017
keywords: wmf,powershell,instalação
title: Rastreamento e registro de scripts
ms.openlocfilehash: dd18453c041428d5a6537c413c3ebe324a62dfee
ms.sourcegitcommit: 2aec310ad0c0b048400cb56f6fa64c1e554c812a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2020
ms.locfileid: "83809862"
---
# <a name="script-tracing-and-logging"></a><span data-ttu-id="6e2dd-103">Rastreamento e registro de scripts</span><span class="sxs-lookup"><span data-stu-id="6e2dd-103">Script Tracing and Logging</span></span>

<span data-ttu-id="6e2dd-104">Embora o PowerShell já tenha a configuração **LogPipelineExecutionDetails** da Política de Grupo para registrar em log a chamada de cmdlets, a linguagem de scripts do PowerShell traz vários recursos que talvez você queira registrar em log e auditar.</span><span class="sxs-lookup"><span data-stu-id="6e2dd-104">While PowerShell already has the **LogPipelineExecutionDetails** Group Policy setting to log the invocation of cmdlets, PowerShell's scripting language has several features that you might want to log and audit.</span></span> <span data-ttu-id="6e2dd-105">O novo recurso de Rastreamento de Script Detalhado permite habilitar o acompanhamento e a análise detalhados ao usar scripts do PowerShell em um sistema.</span><span class="sxs-lookup"><span data-stu-id="6e2dd-105">The new Detailed Script Tracing feature provides detailed tracking and analysis of PowerShell script activity on a system.</span></span> <span data-ttu-id="6e2dd-106">Depois de habilitar o rastreamento detalhado de scripts, o PowerShell registra em log todos os blocos de script no log de eventos do ETW, **Microsoft-Windows-PowerShell/Operational**.</span><span class="sxs-lookup"><span data-stu-id="6e2dd-106">After enabling detailed script tracing, PowerShell logs all script blocks to the ETW event log, **Microsoft-Windows-PowerShell/Operational**.</span></span> <span data-ttu-id="6e2dd-107">Se um bloco de script criar outro bloco de script, por exemplo, chamando `Invoke-Expression`, o bloco de script chamado também será registrado em log.</span><span class="sxs-lookup"><span data-stu-id="6e2dd-107">If a script block creates another script block, for example, by calling `Invoke-Expression`, the invoked script block also logged.</span></span>

<span data-ttu-id="6e2dd-108">O registro em log é habilitado pela configuração **Ativar Registro de Bloco de Script do PowerShell** da Política de Grupo em **Modelos Administrativos** -> **Componentes do Windows** -> **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="6e2dd-108">Logging is enabled through the **Turn on PowerShell Script Block Logging** Group Policy setting in **Administrative Templates** -> **Windows Components** -> **Windows PowerShell**.</span></span>

<span data-ttu-id="6e2dd-109">Os eventos são:</span><span class="sxs-lookup"><span data-stu-id="6e2dd-109">The events are:</span></span>

| <span data-ttu-id="6e2dd-110">Canal</span><span class="sxs-lookup"><span data-stu-id="6e2dd-110">Channel</span></span> |                               <span data-ttu-id="6e2dd-111">Operacional</span><span class="sxs-lookup"><span data-stu-id="6e2dd-111">Operational</span></span>                               |
| ------- | ----------------------------------------------------------------------- |
| <span data-ttu-id="6e2dd-112">Nível</span><span class="sxs-lookup"><span data-stu-id="6e2dd-112">Level</span></span>   | <span data-ttu-id="6e2dd-113">Detalhado</span><span class="sxs-lookup"><span data-stu-id="6e2dd-113">Verbose</span></span>                                                                 |
| <span data-ttu-id="6e2dd-114">Opcode</span><span class="sxs-lookup"><span data-stu-id="6e2dd-114">Opcode</span></span>  | <span data-ttu-id="6e2dd-115">Criar</span><span class="sxs-lookup"><span data-stu-id="6e2dd-115">Create</span></span>                                                                  |
| <span data-ttu-id="6e2dd-116">Tarefa</span><span class="sxs-lookup"><span data-stu-id="6e2dd-116">Task</span></span>    | <span data-ttu-id="6e2dd-117">CommandStart</span><span class="sxs-lookup"><span data-stu-id="6e2dd-117">CommandStart</span></span>                                                            |
| <span data-ttu-id="6e2dd-118">Palavra-chave</span><span class="sxs-lookup"><span data-stu-id="6e2dd-118">Keyword</span></span> | <span data-ttu-id="6e2dd-119">Runspace</span><span class="sxs-lookup"><span data-stu-id="6e2dd-119">Runspace</span></span>                                                                |
| <span data-ttu-id="6e2dd-120">EventId</span><span class="sxs-lookup"><span data-stu-id="6e2dd-120">EventId</span></span> | <span data-ttu-id="6e2dd-121">Engine_ScriptBlockCompiled (0x1008 = 4104)</span><span class="sxs-lookup"><span data-stu-id="6e2dd-121">Engine_ScriptBlockCompiled (0x1008 = 4104)</span></span>                              |
| <span data-ttu-id="6e2dd-122">Mensagem</span><span class="sxs-lookup"><span data-stu-id="6e2dd-122">Message</span></span> | <span data-ttu-id="6e2dd-123">Criando texto Scriptblock (%1 de %2):</span><span class="sxs-lookup"><span data-stu-id="6e2dd-123">Creating Scriptblock text (%1 of %2):</span></span> </br> <span data-ttu-id="6e2dd-124">%3</span><span class="sxs-lookup"><span data-stu-id="6e2dd-124">%3</span></span> </br> <span data-ttu-id="6e2dd-125">ID de ScriptBlock: %4</span><span class="sxs-lookup"><span data-stu-id="6e2dd-125">ScriptBlock ID: %4</span></span> |

<span data-ttu-id="6e2dd-126">O texto inserido na mensagem é a extensão do bloco de script compilado.</span><span class="sxs-lookup"><span data-stu-id="6e2dd-126">The text embedded in the message is the extent of the script block compiled.</span></span> <span data-ttu-id="6e2dd-127">A ID é um GUID que é retido durante o ciclo de vida do bloco de script.</span><span class="sxs-lookup"><span data-stu-id="6e2dd-127">The ID is a GUID that is retained for the life of the script block.</span></span>

<span data-ttu-id="6e2dd-128">Ao habilitar o registro detalhado, o recurso escreve marcadores de início e de fim:</span><span class="sxs-lookup"><span data-stu-id="6e2dd-128">When you enable verbose logging, the feature writes begin and end markers:</span></span>

| <span data-ttu-id="6e2dd-129">Canal</span><span class="sxs-lookup"><span data-stu-id="6e2dd-129">Channel</span></span> |                                 <span data-ttu-id="6e2dd-130">Operacional</span><span class="sxs-lookup"><span data-stu-id="6e2dd-130">Operational</span></span>                                |
| ------- | -------------------------------------------------------------------------- |
| <span data-ttu-id="6e2dd-131">Nível</span><span class="sxs-lookup"><span data-stu-id="6e2dd-131">Level</span></span>   | <span data-ttu-id="6e2dd-132">Detalhado</span><span class="sxs-lookup"><span data-stu-id="6e2dd-132">Verbose</span></span>                                                                    |
| <span data-ttu-id="6e2dd-133">Opcode</span><span class="sxs-lookup"><span data-stu-id="6e2dd-133">Opcode</span></span>  | <span data-ttu-id="6e2dd-134">Abrir/Fechar</span><span class="sxs-lookup"><span data-stu-id="6e2dd-134">Open / Close</span></span>                                                               |
| <span data-ttu-id="6e2dd-135">Tarefa</span><span class="sxs-lookup"><span data-stu-id="6e2dd-135">Task</span></span>    | <span data-ttu-id="6e2dd-136">CommandStart/CommandStop</span><span class="sxs-lookup"><span data-stu-id="6e2dd-136">CommandStart / CommandStop</span></span>                                                 |
| <span data-ttu-id="6e2dd-137">Palavra-chave</span><span class="sxs-lookup"><span data-stu-id="6e2dd-137">Keyword</span></span> | <span data-ttu-id="6e2dd-138">Runspace</span><span class="sxs-lookup"><span data-stu-id="6e2dd-138">Runspace</span></span>                                                                   |
| <span data-ttu-id="6e2dd-139">EventId</span><span class="sxs-lookup"><span data-stu-id="6e2dd-139">EventId</span></span> | <span data-ttu-id="6e2dd-140">ScriptBlock\_Invoke\_Start\_Detail (0x1009 = 4105) /</span><span class="sxs-lookup"><span data-stu-id="6e2dd-140">ScriptBlock\_Invoke\_Start\_Detail (0x1009 = 4105) /</span></span> </br> <span data-ttu-id="6e2dd-141">ScriptBlock\_Invoke\_Complete\_Detail (0x100A = 4106)</span><span class="sxs-lookup"><span data-stu-id="6e2dd-141">ScriptBlock\_Invoke\_Complete\_Detail (0x100A = 4106)</span></span> |
| <span data-ttu-id="6e2dd-142">Mensagem</span><span class="sxs-lookup"><span data-stu-id="6e2dd-142">Message</span></span> | <span data-ttu-id="6e2dd-143">Chamada da ID do ScriptBlock: %1 iniciada/concluída</span><span class="sxs-lookup"><span data-stu-id="6e2dd-143">Started / Completed invocation of ScriptBlock ID: %1</span></span> </br> <span data-ttu-id="6e2dd-144">Runspace ID: %2</span><span class="sxs-lookup"><span data-stu-id="6e2dd-144">Runspace ID: %2</span></span> |

<span data-ttu-id="6e2dd-145">A ID é o GUID que representa o bloco de script (que pode ser correlacionado com a ID de evento 0x1008), e a ID do Runspace representa o runspace no qual este bloco de script foi executado.</span><span class="sxs-lookup"><span data-stu-id="6e2dd-145">The ID is the GUID representing the script block (that can be correlated with event ID 0x1008), and the Runspace ID represents the runspace in which this script block was run.</span></span>

<span data-ttu-id="6e2dd-146">Sinais de porcentagem na mensagem de invocação representam propriedades estruturadas do ETW.</span><span class="sxs-lookup"><span data-stu-id="6e2dd-146">Percent signs in the invocation message represent structured ETW properties.</span></span> <span data-ttu-id="6e2dd-147">Embora eles sejam substituídos pelos valores reais no texto da mensagem, uma maneira mais robusta de acessá-los é recuperar a mensagem com o cmdlet Get-WinEvent e depois usar a matriz **Properties** da mensagem.</span><span class="sxs-lookup"><span data-stu-id="6e2dd-147">While they are replaced with the actual values in the message text, a more robust way to access them is to retrieve the message with the Get-WinEvent cmdlet, and then use the **Properties** array of the message.</span></span>

<span data-ttu-id="6e2dd-148">Aqui está um exemplo de como essa funcionalidade pode ajudar a descodificar uma tentativa mal-intencionada de criptografar e ocultar um script:</span><span class="sxs-lookup"><span data-stu-id="6e2dd-148">Here's an example of how this functionality can help unwrap a malicious attempt to encrypt and obfuscate a script:</span></span>

```powershell
## Malware
function SuperDecrypt
{
    param($script)
    $bytes = [Convert]::FromBase64String($script)

    ## XOR "encryption"
    $xorKey = 0x42
    for($counter = 0; $counter -lt $bytes.Length; $counter++)
    {
        $bytes[$counter] = $bytes[$counter] -bxor $xorKey
    }
    [System.Text.Encoding]::Unicode.GetString($bytes)
}

$decrypted = SuperDecrypt "FUIwQitCNkInQm9CCkItQjFCNkJiQmVCEkI1QixCJkJlQg=="
Invoke-Expression $decrypted
```

<span data-ttu-id="6e2dd-149">A execução disso gera as seguintes entradas de log:</span><span class="sxs-lookup"><span data-stu-id="6e2dd-149">Running this generates the following log entries:</span></span>

```Output
Compiling Scriptblock text (1 of 1):
function SuperDecrypt
{
    param($script)
    $bytes = [Convert]::FromBase64String($script)
    ## XOR "encryption"
    $xorKey = 0x42
    for($counter = 0; $counter -lt $bytes.Length; $counter++)
    {
        $bytes[$counter] = $bytes[$counter] -bxor $xorKey
    }
    [System.Text.Encoding]::Unicode.GetString($bytes)

}
ScriptBlock ID: ad8ae740-1f33-42aa-8dfc-1314411877e3

Compiling Scriptblock text (1 of 1):
$decrypted = SuperDecrypt "FUIwQitCNkInQm9CCkItQjFCNkJiQmVCEkI1QixCJkJlQg=="
ScriptBlock ID: ba11c155-d34c-4004-88e3-6502ecb50f52

Compiling Scriptblock text (1 of 1):
Invoke-Expression $decrypted
ScriptBlock ID: 856c01ca-85d7-4989-b47f-e6a09ee4eeb3

Compiling Scriptblock text (1 of 1):
Write-Host 'Pwnd'
ScriptBlock ID: 5e618414-4e77-48e3-8f65-9a863f54b4c8
```

Caso o tamanho do bloco de script exceda a capacidade de um único evento, o PowerShell dividirá o script em várias partes. <span data-ttu-id="6e2dd-151">Aqui está o código de exemplo para recombinar um script desde suas mensagens de log:</span><span class="sxs-lookup"><span data-stu-id="6e2dd-151">Here is sample code to recombine a script from its log messages:</span></span>

```powershell
$created = Get-WinEvent -FilterHashtable @{ ProviderName="Microsoft-Windows-PowerShell"; Id = 4104 } |
  Where-Object { $_.<...> }
$sortedScripts = $created | sort { $_.Properties[0].Value }
$mergedScript = -join ($sortedScripts | % { $_.Properties[2].Value })
```

<span data-ttu-id="6e2dd-152">Assim como acontece com todos os sistemas de registro em log que têm um buffer de retenção limitado, uma forma de atacar essa infraestrutura seria inundar o log com eventos diferentes para ocultar a evidência anterior.</span><span class="sxs-lookup"><span data-stu-id="6e2dd-152">As with all logging systems that have a limited retention buffer, one way to attack this infrastructure is to flood the log with spurious events to hide earlier evidence.</span></span> <span data-ttu-id="6e2dd-153">Para se proteger contra esse ataque, verifique se você tem alguma forma de coletar logs de eventos configurada (Encaminhamento de Eventos do Windows).</span><span class="sxs-lookup"><span data-stu-id="6e2dd-153">To protect yourself from this attack, ensure that you have some form of event log collection set up Windows Event Forwarding.</span></span> <span data-ttu-id="6e2dd-154">Saiba mais em [Identificar o adversário com o monitoramento de logs de eventos do Windows](https://apps.nsa.gov/iaarchive/library/reports/spotting-the-adversary-with-windows-event-log-monitoring.cfm).</span><span class="sxs-lookup"><span data-stu-id="6e2dd-154">For more information, see [Spotting the Adversary with Windows Event Log Monitoring](https://apps.nsa.gov/iaarchive/library/reports/spotting-the-adversary-with-windows-event-log-monitoring.cfm).</span></span>
