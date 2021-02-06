---
external help file: Microsoft.PowerShell.Commands.Utility.dll-Help.xml
Locale: en-US
Module Name: Microsoft.PowerShell.Utility
ms.date: 04/23/2020
online version: https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/wait-event?view=powershell-7.2&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Wait-Event
ms.openlocfilehash: caf2a1c80848d3140e7ad46fdf54dbe71886c633
ms.sourcegitcommit: 95d41698c7a2450eeb70ef2fb6507fe7e6eff3b6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "99597792"
---
# <span data-ttu-id="21207-102">Wait-Event</span><span class="sxs-lookup"><span data-stu-id="21207-102">Wait-Event</span></span>

## <span data-ttu-id="21207-103">SINOPSE</span><span class="sxs-lookup"><span data-stu-id="21207-103">SYNOPSIS</span></span>
<span data-ttu-id="21207-104">Aguarda até que um determinado evento seja gerado antes de continuar a executar.</span><span class="sxs-lookup"><span data-stu-id="21207-104">Waits until a particular event is raised before continuing to run.</span></span>

## <span data-ttu-id="21207-105">SYNTAX</span><span class="sxs-lookup"><span data-stu-id="21207-105">SYNTAX</span></span>

```
Wait-Event [[-SourceIdentifier] <String>] [-Timeout <Int32>] [<CommonParameters>]
```

## <span data-ttu-id="21207-106">DESCRIPTION</span><span class="sxs-lookup"><span data-stu-id="21207-106">DESCRIPTION</span></span>

<span data-ttu-id="21207-107">O `Wait-Event` cmdlet suspende a execução de um script ou função até que um evento específico seja gerado.</span><span class="sxs-lookup"><span data-stu-id="21207-107">The `Wait-Event` cmdlet suspends execution of a script or function until a particular event is raised.</span></span> <span data-ttu-id="21207-108">A execução é retomada quando o evento é detectado.</span><span class="sxs-lookup"><span data-stu-id="21207-108">Execution resumes when the event is detected.</span></span> <span data-ttu-id="21207-109">Para cancelar a espera, pressione <kbd>Ctrl</kbd> + <kbd>C</kbd>.</span><span class="sxs-lookup"><span data-stu-id="21207-109">To cancel the wait, press <kbd>CTRL</kbd>+<kbd>C</kbd>.</span></span>

<span data-ttu-id="21207-110">Esse recurso fornece uma alternativa às sondagens de evento.</span><span class="sxs-lookup"><span data-stu-id="21207-110">This feature provides an alternative to polling for an event.</span></span> <span data-ttu-id="21207-111">Ele também permite que você determine a resposta a um evento de duas maneiras diferentes:</span><span class="sxs-lookup"><span data-stu-id="21207-111">It also allows you to determine the response to an event in two different ways:</span></span>

- <span data-ttu-id="21207-112">usando o parâmetro **Action** da assinatura do evento</span><span class="sxs-lookup"><span data-stu-id="21207-112">using the **Action** parameter of the event subscription</span></span>
- <span data-ttu-id="21207-113">aguardando um evento retornar e, em seguida, responder com uma ação</span><span class="sxs-lookup"><span data-stu-id="21207-113">waiting for an event to return and then respond with an action</span></span>

## <span data-ttu-id="21207-114">EXEMPLOS</span><span class="sxs-lookup"><span data-stu-id="21207-114">EXAMPLES</span></span>

### <span data-ttu-id="21207-115">Exemplo 1: aguardar o próximo evento</span><span class="sxs-lookup"><span data-stu-id="21207-115">Example 1: Wait for the next event</span></span>

<span data-ttu-id="21207-116">Este exemplo aguarda o próximo evento que é gerado.</span><span class="sxs-lookup"><span data-stu-id="21207-116">This example waits for the next event that is raised.</span></span>

```powershell
Wait-Event
```

### <span data-ttu-id="21207-117">Exemplo 2: aguardar um evento com um identificador de origem especificado</span><span class="sxs-lookup"><span data-stu-id="21207-117">Example 2: Wait for an event with a specified source identifier</span></span>

<span data-ttu-id="21207-118">Este exemplo aguarda o próximo evento que é gerado e que tem um identificador de origem de ProcessStarted.</span><span class="sxs-lookup"><span data-stu-id="21207-118">This example waits for the next event that is raised and that has a source identifier of ProcessStarted.</span></span>

```powershell
Wait-Event -SourceIdentifier "ProcessStarted"
```

### <span data-ttu-id="21207-119">Exemplo 3: aguardar um evento decorrido do temporizador</span><span class="sxs-lookup"><span data-stu-id="21207-119">Example 3: Wait for a timer elapsed event</span></span>

<span data-ttu-id="21207-120">Este exemplo usa o `Wait-Event` cmdlet para aguardar um evento de temporizador em um temporizador definido para 2000 milissegundos.</span><span class="sxs-lookup"><span data-stu-id="21207-120">This example uses the `Wait-Event` cmdlet to wait for a timer event on a timer that is set for 2000 milliseconds.</span></span>

```powershell
$Timer = New-Object Timers.Timer
$objectEventArgs = @{
    InputObject = $Timer
    EventName = 'Elapsed'
    SourceIdentifier = 'Timer.Elapsed'
}
Register-ObjectEvent @objectEventArgs
$Timer.Interval = 2000
$Timer.Autoreset = $False
$Timer.Enabled = $True
Wait-Event Timer.Elapsed
```

```Output
ComputerName     :
RunspaceId       : bb560b14-ff43-48d4-b801-5adc31bbc6fb
EventIdentifier  : 1
Sender           : System.Timers.Timer
SourceEventArgs  : System.Timers.ElapsedEventArgs
SourceArgs       : {System.Timers.Timer, System.Timers.ElapsedEventArgs}
SourceIdentifier : Timer.Elapsed
TimeGenerated    : 4/23/2020 2:30:37 PM
MessageData      :
```

### <span data-ttu-id="21207-121">Exemplo 4: aguardar um evento após um tempo limite especificado</span><span class="sxs-lookup"><span data-stu-id="21207-121">Example 4: Wait for an event after a specified timeout</span></span>

<span data-ttu-id="21207-122">Este exemplo aguarda até 90 segundos para o próximo evento que é gerado e que tem um identificador de origem de **ProcessStarted**.</span><span class="sxs-lookup"><span data-stu-id="21207-122">This example waits up to 90 seconds for the next event that is raised and that has a source identifier of **ProcessStarted**.</span></span> <span data-ttu-id="21207-123">Se o tempo especificado expirar, a espera terminará.</span><span class="sxs-lookup"><span data-stu-id="21207-123">If the specified time expires, the wait ends.</span></span>

```powershell
Wait-Event -SourceIdentifier "ProcessStarted" -Timeout 90
```

## <span data-ttu-id="21207-124">PARAMETERS</span><span class="sxs-lookup"><span data-stu-id="21207-124">PARAMETERS</span></span>

### <span data-ttu-id="21207-125">-SourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="21207-125">-SourceIdentifier</span></span>

<span data-ttu-id="21207-126">Especifica o identificador de origem que esse cmdlet espera por eventos.</span><span class="sxs-lookup"><span data-stu-id="21207-126">Specifies the source identifier that this cmdlet waits for events.</span></span>
<span data-ttu-id="21207-127">Por padrão, o `Wait-Event` aguarda qualquer evento.</span><span class="sxs-lookup"><span data-stu-id="21207-127">By default, `Wait-Event` waits for any event.</span></span>

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### <span data-ttu-id="21207-128">-Tempo limite</span><span class="sxs-lookup"><span data-stu-id="21207-128">-Timeout</span></span>

<span data-ttu-id="21207-129">Especifica o tempo máximo, em segundos, que `Wait-Event` aguarda a ocorrência do evento.</span><span class="sxs-lookup"><span data-stu-id="21207-129">Specifies the maximum time, in seconds, that `Wait-Event` waits for the event to occur.</span></span> <span data-ttu-id="21207-130">O padrão, -1, aguarda indefinidamente.</span><span class="sxs-lookup"><span data-stu-id="21207-130">The default, -1, waits indefinitely.</span></span> <span data-ttu-id="21207-131">O tempo começa quando você envia o `Wait-Event` comando.</span><span class="sxs-lookup"><span data-stu-id="21207-131">The timing starts when you submit the `Wait-Event` command.</span></span>

<span data-ttu-id="21207-132">Se o tempo especificado for ultrapassado, a espera terminará e o prompt de comando retornará, ainda que o evento não tenha sido ativado.</span><span class="sxs-lookup"><span data-stu-id="21207-132">If the specified time is exceeded, the wait ends and the command prompt returns, even if the event has not been raised.</span></span> <span data-ttu-id="21207-133">Nenhuma mensagem de erro é exibida.</span><span class="sxs-lookup"><span data-stu-id="21207-133">No error message is displayed.</span></span>

```yaml
Type: System.Int32
Parameter Sets: (All)
Aliases: TimeoutSec

Required: False
Position: Named
Default value: -1
Accept pipeline input: False
Accept wildcard characters: False
```

### <span data-ttu-id="21207-134">CommonParameters</span><span class="sxs-lookup"><span data-stu-id="21207-134">CommonParameters</span></span>

<span data-ttu-id="21207-135">Este cmdlet oferece suporte aos parâmetros comuns: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction e -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="21207-135">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span> <span data-ttu-id="21207-136">Para obter mais informações, confira [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="21207-136">For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).</span></span>

## <span data-ttu-id="21207-137">ENTRADAS</span><span class="sxs-lookup"><span data-stu-id="21207-137">INPUTS</span></span>

### <span data-ttu-id="21207-138">System.String</span><span class="sxs-lookup"><span data-stu-id="21207-138">System.String</span></span>

## <span data-ttu-id="21207-139">SAÍDAS</span><span class="sxs-lookup"><span data-stu-id="21207-139">OUTPUTS</span></span>

### <span data-ttu-id="21207-140">System. Management. Automation. PSEventArgs</span><span class="sxs-lookup"><span data-stu-id="21207-140">System.Management.Automation.PSEventArgs</span></span>

## <span data-ttu-id="21207-141">OBSERVAÇÕES</span><span class="sxs-lookup"><span data-stu-id="21207-141">NOTES</span></span>

<span data-ttu-id="21207-142">Eventos, assinaturas de evento e a fila de eventos existem apenas na sessão atual.</span><span class="sxs-lookup"><span data-stu-id="21207-142">Events, event subscriptions, and the event queue exist only in the current session.</span></span> <span data-ttu-id="21207-143">Se você fechar a sessão atual, a fila de eventos será descartada e a inscrição do evento será cancelada.</span><span class="sxs-lookup"><span data-stu-id="21207-143">If you close the current session, the event queue is discarded and the event subscription is canceled.</span></span>

## <span data-ttu-id="21207-144">LINKS RELACIONADOS</span><span class="sxs-lookup"><span data-stu-id="21207-144">RELATED LINKS</span></span>

[<span data-ttu-id="21207-145">Get-Event</span><span class="sxs-lookup"><span data-stu-id="21207-145">Get-Event</span></span>](Get-Event.md)

[<span data-ttu-id="21207-146">Get-EventSubscriber</span><span class="sxs-lookup"><span data-stu-id="21207-146">Get-EventSubscriber</span></span>](Get-EventSubscriber.md)

[<span data-ttu-id="21207-147">New-Event</span><span class="sxs-lookup"><span data-stu-id="21207-147">New-Event</span></span>](New-Event.md)

[<span data-ttu-id="21207-148">Register-EngineEvent</span><span class="sxs-lookup"><span data-stu-id="21207-148">Register-EngineEvent</span></span>](Register-EngineEvent.md)

[<span data-ttu-id="21207-149">Register-ObjectEvent</span><span class="sxs-lookup"><span data-stu-id="21207-149">Register-ObjectEvent</span></span>](Register-ObjectEvent.md)

[<span data-ttu-id="21207-150">Remove-Event</span><span class="sxs-lookup"><span data-stu-id="21207-150">Remove-Event</span></span>](Remove-Event.md)

[<span data-ttu-id="21207-151">Unregister-Event</span><span class="sxs-lookup"><span data-stu-id="21207-151">Unregister-Event</span></span>](Unregister-Event.md)

[<span data-ttu-id="21207-152">Wait-Event</span><span class="sxs-lookup"><span data-stu-id="21207-152">Wait-Event</span></span>](Wait-Event.md)

