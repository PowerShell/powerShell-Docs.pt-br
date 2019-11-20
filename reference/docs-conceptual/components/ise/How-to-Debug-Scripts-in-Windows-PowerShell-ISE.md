---
ms.date: 06/05/2017
keywords: powershell, cmdlet
title: Como depurar scripts no ISE do Windows PowerShell
ms.openlocfilehash: 99d6fbcb805e3fe31f95eafd4daf272cf41fd845
ms.sourcegitcommit: a6e54a305fdeb6482321c77da8066d2f991c93e1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2019
ms.locfileid: "74117420"
---
# <a name="how-to-debug-scripts-in-windows-powershell-ise"></a><span data-ttu-id="ac913-103">Como depurar scripts no ISE do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac913-103">How to Debug Scripts in Windows PowerShell ISE</span></span>

<span data-ttu-id="ac913-104">Este artigo descreve como depurar scripts em um computador local usando os recursos de depuração visual do ISE (Ambiente de Script Integrado) do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac913-104">This article describes how to debug scripts on a local computer by using the Windows PowerShell Integrated Scripting Environment (ISE) visual debugging features.</span></span>

## <a name="how-to-manage-breakpoints"></a><span data-ttu-id="ac913-105">Como gerenciar pontos de interrupção</span><span class="sxs-lookup"><span data-stu-id="ac913-105">How to manage breakpoints</span></span>

<span data-ttu-id="ac913-106">Um ponto de interrupção é um ponto designado em um script em que você deseja pausar a operação para poder examinar o estado atual das variáveis e o ambiente no qual o script está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="ac913-106">A breakpoint is a designated spot in a script where you would like operation to pause so that you can examine the current state of the variables and the environment in which your script is running.</span></span> <span data-ttu-id="ac913-107">Depois de o script ser pausado por um ponto de interrupção, você pode executar comandos no Painel de Console para examinar o estado do script.</span><span class="sxs-lookup"><span data-stu-id="ac913-107">Once your script is paused by a breakpoint, you can run commands in the Console Pane to examine the state of your script.</span></span>  <span data-ttu-id="ac913-108">Você pode gerar variáveis ou executar outros comandos.</span><span class="sxs-lookup"><span data-stu-id="ac913-108">You can output variables or run other commands.</span></span> <span data-ttu-id="ac913-109">Você ainda pode modificar o valor de todas as variáveis que estão visíveis para o contexto do script em execução no momento.</span><span class="sxs-lookup"><span data-stu-id="ac913-109">You can even modify the value of any variables that are visible to the context of the currently running script.</span></span> <span data-ttu-id="ac913-110">Após examinar o que deseja ver, você pode retomar a operação do script.</span><span class="sxs-lookup"><span data-stu-id="ac913-110">After you have examined what you want to see, you can resume operation of the script.</span></span>

<span data-ttu-id="ac913-111">É possível definir três tipos de pontos de interrupção no ambiente de depuração do Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ac913-111">You can set three types of breakpoints in the Windows PowerShell debugging environment:</span></span>

1. <span data-ttu-id="ac913-112">**Ponto de interrupção de linha**.</span><span class="sxs-lookup"><span data-stu-id="ac913-112">**Line breakpoint**.</span></span> <span data-ttu-id="ac913-113">O script faz uma pausa quando a linha designada é atingida durante a operação do script</span><span class="sxs-lookup"><span data-stu-id="ac913-113">The script pauses when the designated line is reached during the operation of the script</span></span>

2. <span data-ttu-id="ac913-114">**Ponto de interrupção de variável.**</span><span class="sxs-lookup"><span data-stu-id="ac913-114">**Variable breakpoint.**</span></span> <span data-ttu-id="ac913-115">O script faz uma pausa sempre que o valor da variável designada é alterado.</span><span class="sxs-lookup"><span data-stu-id="ac913-115">The script pauses whenever the designated variable's value changes.</span></span>

3. <span data-ttu-id="ac913-116">**Ponto de interrupção de comando.**</span><span class="sxs-lookup"><span data-stu-id="ac913-116">**Command breakpoint.**</span></span> <span data-ttu-id="ac913-117">O script faz uma pausa sempre que o comando designado está prestes a ser executado durante a operação do script.</span><span class="sxs-lookup"><span data-stu-id="ac913-117">The script pauses whenever the designated command is about to be run during the operation of the script.</span></span> <span data-ttu-id="ac913-118">Ele pode incluir parâmetros para filtrar ainda mais o ponto de interrupção para somente a operação desejada.</span><span class="sxs-lookup"><span data-stu-id="ac913-118">It can include parameters to further filter the breakpoint to only the operation you want.</span></span> <span data-ttu-id="ac913-119">O comando também pode ser uma função que você criou.</span><span class="sxs-lookup"><span data-stu-id="ac913-119">The command can also be a function you created.</span></span>

<span data-ttu-id="ac913-120">Desses, no ambiente de depuração do ISE do Windows PowerShell, somente os pontos de interrupção de linha podem ser definidos usando o menu ou os atalhos de teclado.</span><span class="sxs-lookup"><span data-stu-id="ac913-120">Of these, in the Windows PowerShell ISE debugging environment, only line breakpoints can be set by using the menu or the keyboard shortcuts.</span></span> <span data-ttu-id="ac913-121">Os outros dois tipos de pontos de interrupção podem ser definidos, mas são definidos no Painel de Console usando o cmdlet [Set-PSBreakpoint](https://technet.microsoft.com/library/88d2d9ad-17dc-44ae-99aa-f841125b9dc8).</span><span class="sxs-lookup"><span data-stu-id="ac913-121">The other two types of breakpoints can be set, but they are set from the Console Pane by using the [Set-PSBreakpoint](https://technet.microsoft.com/library/88d2d9ad-17dc-44ae-99aa-f841125b9dc8) cmdlet.</span></span> <span data-ttu-id="ac913-122">Esta seção descreve como executar tarefas de depuração no ISE do Windows PowerShell usando os menus quando disponíveis e como executar uma variedade maior de comandos no Painel de Console usando scripts.</span><span class="sxs-lookup"><span data-stu-id="ac913-122">This section describes how you can perform debugging tasks in Windows PowerShell ISE by using the menus where available, and perform a wider range of commands from the Console Pane by using scripting.</span></span>

### <a name="to-set-a-breakpoint"></a><span data-ttu-id="ac913-123">Para definir um ponto de interrupção</span><span class="sxs-lookup"><span data-stu-id="ac913-123">To set a breakpoint</span></span>

<span data-ttu-id="ac913-124">Um ponto de interrupção pode ser definido em um script somente depois de ele ser salvo.</span><span class="sxs-lookup"><span data-stu-id="ac913-124">A breakpoint can be set in a script only after it has been saved.</span></span> <span data-ttu-id="ac913-125">Clique com o botão direito do mouse na linha em que você quer definir um ponto de interrupção e clique em **Alternar Ponto de Interrupção**.</span><span class="sxs-lookup"><span data-stu-id="ac913-125">Right-click the line where you want to set a line breakpoint, and then click **Toggle Breakpoint**.</span></span> <span data-ttu-id="ac913-126">Ou então clique com o botão direito do mouse na linha na qual você deseja definir um ponto de interrupção e pressione **F9** ou, no menu **Depurar**, clique em **Alternar Ponto de Interrupção**.</span><span class="sxs-lookup"><span data-stu-id="ac913-126">Or, click the line where you want to set a line breakpoint, and press **F9** or, on the **Debug** menu, click **Toggle Breakpoint**.</span></span>

<span data-ttu-id="ac913-127">O script a seguir é um exemplo de como é possível definir um ponto de interrupção de variável no Painel de Console usando o cmdlet [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420).</span><span class="sxs-lookup"><span data-stu-id="ac913-127">The following script is an example of how you can set a variable breakpoint from the Console Pane by using the [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420) cmdlet.</span></span>

```powershell
# This command sets a breakpoint on the Server variable in the Sample.ps1 script.
Set-PSBreakpoint -Script sample.ps1 -Variable Server
```

### <a name="list-all-breakpoints"></a><span data-ttu-id="ac913-128">Listar todos os pontos de interrupção</span><span class="sxs-lookup"><span data-stu-id="ac913-128">List all breakpoints</span></span>

<span data-ttu-id="ac913-129">Exibe todos os pontos de interrupção na sessão atual do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac913-129">Displays all breakpoints in the current Windows PowerShell session.</span></span>

<span data-ttu-id="ac913-130">No menu **Depurar**, clique em **Listar Pontos de Interrupção**.</span><span class="sxs-lookup"><span data-stu-id="ac913-130">On the **Debug** menu, click **List Breakpoints**.</span></span> <span data-ttu-id="ac913-131">O script a seguir é um exemplo de como é possível listar todos os pontos de interrupção no Painel de Console usando o cmdlet [Get-PSBreakpoint](https://technet.microsoft.com/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6).</span><span class="sxs-lookup"><span data-stu-id="ac913-131">The following script is an example of how you can list all breakpoints from the Console Pane by using the [Get-PSBreakpoint](https://technet.microsoft.com/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6) cmdlet.</span></span>

```powershell
# This command lists all breakpoints in the current session.
Get-PSBreakpoint
```

### <a name="remove-a-breakpoint"></a><span data-ttu-id="ac913-132">Remover um ponto de interrupção</span><span class="sxs-lookup"><span data-stu-id="ac913-132">Remove a breakpoint</span></span>

<span data-ttu-id="ac913-133">Remover um ponto de interrupção o excluirá.</span><span class="sxs-lookup"><span data-stu-id="ac913-133">Removing a breakpoint deletes it.</span></span>

<span data-ttu-id="ac913-134">Se você achar que talvez possa querer usá-lo novamente mais tarde, considere [Desabilitar um ponto de interrupção](#disable-a-breakpoint) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="ac913-134">If you think you might want to use it again later, consider [Disable a Breakpoint](#disable-a-breakpoint) it instead.</span></span>
<span data-ttu-id="ac913-135">Clique com o botão direito do mouse na linha de onde você quer remover um ponto de interrupção e clique em **Alternar Ponto de Interrupção**.</span><span class="sxs-lookup"><span data-stu-id="ac913-135">Right-click the line where you want to remove a breakpoint, and then click **Toggle Breakpoint**.</span></span>
<span data-ttu-id="ac913-136">Ou então, clique na linha na qual você deseja remover um ponto de interrupção e, no menu **Depurar**, clique em **Alternar Ponto de Interrupção**.</span><span class="sxs-lookup"><span data-stu-id="ac913-136">Or, click the line where you want to remove a breakpoint, and on the **Debug** menu, click **Toggle Breakpoint**.</span></span>
<span data-ttu-id="ac913-137">O script a seguir é um exemplo de como remover um ponto de interrupção com uma ID especificada do Painel de Console usando o cmdlet [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6).</span><span class="sxs-lookup"><span data-stu-id="ac913-137">The following script is an example of how to remove a breakpoint with a specified ID from the Console Pane by using the [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) cmdlet.</span></span>

```powershell
# This command deletes the breakpoint with breakpoint ID 2.
Remove-PSBreakpoint -Id 2
```

### <a name="remove-all-breakpoints"></a><span data-ttu-id="ac913-138">Remover Todos os Pontos de Interrupção</span><span class="sxs-lookup"><span data-stu-id="ac913-138">Remove All Breakpoints</span></span>

<span data-ttu-id="ac913-139">Para remover todos os pontos de interrupção definidos na sessão atual, no menu **Depurar**, clique em **Remover Todos os Pontos de Interrupção**.</span><span class="sxs-lookup"><span data-stu-id="ac913-139">To remove all breakpoints defined in the current session, on the **Debug** menu, click **Remove All Breakpoints**.</span></span>

<span data-ttu-id="ac913-140">O script a seguir é um exemplo de como remover todos os pontos de interrupção no Painel de Console usando o cmdlet [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6).</span><span class="sxs-lookup"><span data-stu-id="ac913-140">The following script is an example of how to remove all breakpoints from the Console Pane by using the [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) cmdlet.</span></span>

```powershell
# This command deletes all of the breakpoints in the current session.
Get-PSBreakpoint | Remove-PSBreakpoint
```

### <a name="disable-a-breakpoint"></a><span data-ttu-id="ac913-141">Desabilitar um ponto de interrupção</span><span class="sxs-lookup"><span data-stu-id="ac913-141">Disable a Breakpoint</span></span>

<span data-ttu-id="ac913-142">Desabilitar um ponto de interrupção não o remove; ele é desativado até ele ser habilitado.</span><span class="sxs-lookup"><span data-stu-id="ac913-142">Disabling a breakpoint does not remove it; it turns it off until it is enabled.</span></span>  <span data-ttu-id="ac913-143">Para desabilitar um ponto de interrupção de linha específico, clique com o botão direito do mouse na linha na qual você quer desabilitar um ponto de interrupção e clique em **Desabilitar Ponto de Interrupção**.</span><span class="sxs-lookup"><span data-stu-id="ac913-143">To disable a specific line breakpoint, right-click the line where you want to disable a breakpoint, and then click **Disable Breakpoint**.</span></span> <span data-ttu-id="ac913-144">Ou então, clique na linha na qual você deseja desabilitar um ponto de interrupção e pressione **F9** ou, no menu **Depurar**, clique em **Desabilitar Ponto de Interrupção**.</span><span class="sxs-lookup"><span data-stu-id="ac913-144">Or, click the line where you want to disable a breakpoint, and press **F9** or, on the **Debug** menu, click **Disable Breakpoint**.</span></span> <span data-ttu-id="ac913-145">O script a seguir é um exemplo de como é possível remover um ponto de interrupção com uma ID especificada do Painel de Console usando o cmdlet [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8).</span><span class="sxs-lookup"><span data-stu-id="ac913-145">The following script is an example of how you can remove a breakpoint with a specified ID from the Console Pane by using the [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) cmdlet.</span></span>

```powershell
# This command disables the breakpoint with breakpoint ID 0.
Disable-PSBreakpoint -Id 0
```

### <a name="disable-all-breakpoints"></a><span data-ttu-id="ac913-146">Desabilitar Todos os Pontos de Interrupção</span><span class="sxs-lookup"><span data-stu-id="ac913-146">Disable All Breakpoints</span></span>

<span data-ttu-id="ac913-147">Desabilitar um ponto de interrupção não o remove; ele é desativado até ele ser habilitado.</span><span class="sxs-lookup"><span data-stu-id="ac913-147">Disabling a breakpoint does not remove it; it turns it off until it is enabled.</span></span>  <span data-ttu-id="ac913-148">Para desabilitar todos os pontos de interrupção na sessão atual, no menu **Depurar**, clique em **Desabilitar Todos os Pontos de Interrupção**.</span><span class="sxs-lookup"><span data-stu-id="ac913-148">To disable all breakpoints in the current session, on the **Debug** menu, click **Disable all Breakpoints**.</span></span> <span data-ttu-id="ac913-149">O script a seguir é um exemplo de como é possível desabilitar todos os pontos de interrupção no Painel de Console usando o cmdlet [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8).</span><span class="sxs-lookup"><span data-stu-id="ac913-149">The following script is an example of how you can disable all breakpoints from the Console Pane by using the [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) cmdlet.</span></span>

```powershell
# This command disables all breakpoints in the current session.
# You can abbreviate this command as: "gbp | dbp".
Get-PSBreakpoint | Disable-PSBreakpoint
```

### <a name="enable-a-breakpoint"></a><span data-ttu-id="ac913-150">Habilitar um ponto de interrupção</span><span class="sxs-lookup"><span data-stu-id="ac913-150">Enable a Breakpoint</span></span>

<span data-ttu-id="ac913-151">Para habilitar um ponto de interrupção específico, clique com o botão direito do mouse na linha na qual você quer habilitar um ponto de interrupção e clique em **Habilitar Ponto de Interrupção**.</span><span class="sxs-lookup"><span data-stu-id="ac913-151">To enable a specific breakpoint, right-click the line where you want to enable a breakpoint, and then click **Enable Breakpoint**.</span></span> <span data-ttu-id="ac913-152">Ou então, clique na linha na qual você deseja habilitar um ponto de interrupção e pressione **F9** ou, no menu **Depurar**, clique em **Habilitar Ponto de Interrupção**.</span><span class="sxs-lookup"><span data-stu-id="ac913-152">Or, click the line where you want to enable a breakpoint, and then press **F9** or, on the **Debug** menu, click **Enable Breakpoint**.</span></span> <span data-ttu-id="ac913-153">O script a seguir é um exemplo de como é possível habilitar pontos de interrupção específicos no Painel de Console usando o cmdlet [Enable-PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0).</span><span class="sxs-lookup"><span data-stu-id="ac913-153">The following script is an example of how you can enable specific breakpoints from the Console Pane by using the [Enable-PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) cmdlet.</span></span>

```powershell
# This command enables breakpoints with breakpoint IDs 0, 1, and 5.
Enable-PSBreakpoint -Id 0, 1, 5
```

### <a name="enable-all-breakpoints"></a><span data-ttu-id="ac913-154">Habilitar Todos os Pontos de Interrupção</span><span class="sxs-lookup"><span data-stu-id="ac913-154">Enable All Breakpoints</span></span>

<span data-ttu-id="ac913-155">Para habilitar todos os pontos de interrupção definidos na sessão atual, no menu **Depurar**, clique em **Habilitar Todos os Pontos de Interrupção**.</span><span class="sxs-lookup"><span data-stu-id="ac913-155">To enable all breakpoints defined in the current session, on the **Debug** menu, click **Enable all Breakpoints**.</span></span> <span data-ttu-id="ac913-156">O script a seguir é um exemplo de como é possível habilitar todos os pontos de interrupção no Painel de Console usando o cmdlet [Enable-PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0).</span><span class="sxs-lookup"><span data-stu-id="ac913-156">The following script is an example of how you can enable all breakpoints from the Console Pane by using the [Enable-PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) cmdlet.</span></span>

```powershell
# This command enables all breakpoints in the current session.
# You can abbreviate the command by using their aliases: "gbp | ebp".
Get-PSBreakpoint | Enable-PSBreakpoint
```

## <a name="how-to-manage-a-debugging-session"></a><span data-ttu-id="ac913-157">Como gerenciar uma sessão de depuração</span><span class="sxs-lookup"><span data-stu-id="ac913-157">How to manage a debugging session</span></span>

<span data-ttu-id="ac913-158">Antes de iniciar a depuração, você deve definir um ou mais pontos de interrupção.</span><span class="sxs-lookup"><span data-stu-id="ac913-158">Before you start debugging, you must set one or more breakpoints.</span></span> <span data-ttu-id="ac913-159">Não é possível definir um ponto de interrupção, a menos que o script que você deseja depurar esteja salvo.</span><span class="sxs-lookup"><span data-stu-id="ac913-159">You cannot set a breakpoint unless the script that you want to debug is saved.</span></span> <span data-ttu-id="ac913-160">Para obter instruções sobre como definir um ponto de interrupção, consulte [Como gerenciar pontos de interrupção](#how-to-manage-breakpoints) ou [Set-PSBreakpoint](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/set-psbreakpoint).</span><span class="sxs-lookup"><span data-stu-id="ac913-160">For directions on of how to set a breakpoint, see [How to manage breakpoints](#how-to-manage-breakpoints) or [Set-PSBreakpoint](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/set-psbreakpoint).</span></span> <span data-ttu-id="ac913-161">Depois de iniciar a depuração, não é possível editar um script até interromper a depuração.</span><span class="sxs-lookup"><span data-stu-id="ac913-161">After you start debugging, you cannot edit a script until you stop debugging.</span></span> <span data-ttu-id="ac913-162">Um script que tem um ou mais pontos de interrupção definido é salvo automaticamente antes de ser executado.</span><span class="sxs-lookup"><span data-stu-id="ac913-162">A script that has one or more breakpoints set is automatically saved before it is run.</span></span>

### <a name="to-start-debugging"></a><span data-ttu-id="ac913-163">Para iniciar a depuração</span><span class="sxs-lookup"><span data-stu-id="ac913-163">To start debugging</span></span>

<span data-ttu-id="ac913-164">Pressione **F5** ou, na barra de ferramentas, clique no ícone **Executar Script** ou, no menu **Depurar**, clique em **Executar/Continuar**.</span><span class="sxs-lookup"><span data-stu-id="ac913-164">Press **F5** or, on the toolbar, click the **Run Script** icon, or on the **Debug** menu click **Run/Continue**.</span></span> <span data-ttu-id="ac913-165">O script é executado até encontrar o primeiro ponto de interrupção.</span><span class="sxs-lookup"><span data-stu-id="ac913-165">The script runs until it encounters the first breakpoint.</span></span> <span data-ttu-id="ac913-166">Ele pausa a operação neste ponto e realça a linha na qual ele pausa.</span><span class="sxs-lookup"><span data-stu-id="ac913-166">It pauses operation there and highlights the line on which it paused.</span></span>

### <a name="to-continue-debugging"></a><span data-ttu-id="ac913-167">Para continuar a depuração</span><span class="sxs-lookup"><span data-stu-id="ac913-167">To continue debugging</span></span>

<span data-ttu-id="ac913-168">Pressione **F5** ou, na barra de ferramentas, clique no ícone **Executar Script** ou, no menu **Depurar**, clique em **Executar/Continuar** ou então, no Painel Console, digite **C** e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ac913-168">Press **F5** or, on the toolbar, click the **Run Script** icon, or on the **Debug** menu, click **Run/Continue** or, in the Console Pane, type **C** and then press **ENTER**.</span></span> <span data-ttu-id="ac913-169">Isso fará com que o script continue em execução até o próximo ponto de interrupção ou até o fim do script se outros pontos de interrupção não forem encontrados.</span><span class="sxs-lookup"><span data-stu-id="ac913-169">This causes the script to continue running to the next breakpoint or to the end of the script if no further breakpoints are encountered.</span></span>

### <a name="to-view-the-call-stack"></a><span data-ttu-id="ac913-170">Para exibir a pilha de chamadas</span><span class="sxs-lookup"><span data-stu-id="ac913-170">To view the call stack</span></span>

<span data-ttu-id="ac913-171">A pilha de chamadas exibe a execução local no script atual.</span><span class="sxs-lookup"><span data-stu-id="ac913-171">The call stack displays the current run location in the script.</span></span> <span data-ttu-id="ac913-172">Se o script for executado em uma função que foi chamada por uma função diferente, isso será representado na exibição por linhas adicionais na saída.</span><span class="sxs-lookup"><span data-stu-id="ac913-172">If the script is running in a function that was called by a different function, then that is represented in the display by additional rows in the output.</span></span> <span data-ttu-id="ac913-173">A linha inferior exibe o script original e a linha em que uma função foi chamada.</span><span class="sxs-lookup"><span data-stu-id="ac913-173">The bottom-most row displays the original script and the line in it in which a function was called.</span></span> <span data-ttu-id="ac913-174">A próxima linha mostra essa função e a linha em que outra função pode ter sido chamada.</span><span class="sxs-lookup"><span data-stu-id="ac913-174">The next line up shows that function and the line in it in which another function might have been called.</span></span>  <span data-ttu-id="ac913-175">A linha superior mostra o contexto atual da linha atual em que o ponto de interrupção foi definido.</span><span class="sxs-lookup"><span data-stu-id="ac913-175">The top-most row shows the current context of the current line on which the breakpoint is set.</span></span>

<span data-ttu-id="ac913-176">Enquanto está em pausa, para ver a pilha de chamadas atual, pressione **Ctrl+Shift+D** ou, no menu **Depurar**, clique em **Exibir a Pilha de Chamadas** ou, no Painel Console, digite **K** e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ac913-176">While paused, to see the current call stack, press **CTRL+SHIFT+D** or, on the **Debug** menu, click **Display Call Stack** or, in the Console Pane, type **K** and then press **ENTER**.</span></span>

### <a name="to-stop-debugging"></a><span data-ttu-id="ac913-177">Para interromper a depuração</span><span class="sxs-lookup"><span data-stu-id="ac913-177">To stop debugging</span></span>

<span data-ttu-id="ac913-178">Pressione **Shift+F5** ou, no menu **Depurar**, clique em **Parar Depurador** ou então, no Painel Console, digite **Q** e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ac913-178">Press **SHIFT-F5** or, on the **Debug** menu, click **Stop Debugger**, or, in the Console Pane, type **Q** and then press **ENTER**.</span></span>

## <a name="how-to-step-over-step-into-and-step-out-while-debugging"></a><span data-ttu-id="ac913-179">Como contornar, intervir e sair durante a depuração</span><span class="sxs-lookup"><span data-stu-id="ac913-179">How to step over, step into, and step out while debugging</span></span>

<span data-ttu-id="ac913-180">Passo a passo é o processo de executar uma instrução de cada vez.</span><span class="sxs-lookup"><span data-stu-id="ac913-180">Stepping is the process of running one statement at a time.</span></span> <span data-ttu-id="ac913-181">Você pode parar em uma linha de código e examinar os valores de variáveis e o estado do sistema.</span><span class="sxs-lookup"><span data-stu-id="ac913-181">You can stop on a line of code, and examine the values of variables and the state of the system.</span></span> <span data-ttu-id="ac913-182">A tabela a seguir descreve as tarefas comuns de depuração como contornar, intervir e sair.</span><span class="sxs-lookup"><span data-stu-id="ac913-182">The following table describes common debugging tasks such as stepping over, stepping into, and stepping out.</span></span>

| <span data-ttu-id="ac913-183">Tarefa de Depuração</span><span class="sxs-lookup"><span data-stu-id="ac913-183">Debugging Task</span></span> | <span data-ttu-id="ac913-184">Descrição</span><span class="sxs-lookup"><span data-stu-id="ac913-184">Description</span></span> | <span data-ttu-id="ac913-185">Como fazer isso no ISE do PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac913-185">How to accomplish it in PowerShell ISE</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ac913-186">**Intervir**</span><span class="sxs-lookup"><span data-stu-id="ac913-186">**Step Into**</span></span> | <span data-ttu-id="ac913-187">Executa a instrução atual e para na próxima instrução.</span><span class="sxs-lookup"><span data-stu-id="ac913-187">Executes the current statement and then stops at the next statement.</span></span> <span data-ttu-id="ac913-188">Se a instrução atual for uma função ou uma chamada de script, o depurador intervirá nessa função ou script, caso contrário, ele parará na próxima instrução.</span><span class="sxs-lookup"><span data-stu-id="ac913-188">If the current statement is a function or script call, then the debugger steps into that function or script, otherwise it stops at the next statement.</span></span> | <span data-ttu-id="ac913-189">Pressione **F11** ou, no menu **Depurar**, clique em **Intervir** ou então, no Painel de Console, digite **S** e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ac913-189">Press **F11** or, on the **Debug** menu, click **Step Into**, or in the Console Pane, type **S** and press **ENTER**.</span></span> |
| <span data-ttu-id="ac913-190">**Contornar**</span><span class="sxs-lookup"><span data-stu-id="ac913-190">**Step Over**</span></span> | <span data-ttu-id="ac913-191">Executa a instrução atual e para na próxima instrução.</span><span class="sxs-lookup"><span data-stu-id="ac913-191">Executes the current statement and then stops at the next statement.</span></span> <span data-ttu-id="ac913-192">Se a instrução atual for uma função ou uma chamada de script, o depurador executará a função ou o script completos e parará na próxima instrução após a chamada de função.</span><span class="sxs-lookup"><span data-stu-id="ac913-192">If the current statement is a function or script call, then the debugger executes the whole function or script, and it stops at the next statement after the function call.</span></span> | <span data-ttu-id="ac913-193">Pressione **F10** ou, no menu **Depurar**, clique em **Contornar** ou então, no Painel de Console, digite **V** e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ac913-193">Press **F10** or, on the **Debug** menu, click **Step Over**, or in the Console Pane, type **V** and press **ENTER**.</span></span> |
| <span data-ttu-id="ac913-194">**Sair**</span><span class="sxs-lookup"><span data-stu-id="ac913-194">**Step Out**</span></span> | <span data-ttu-id="ac913-195">Sairá da função atual e subirá um nível se a função for aninhada.</span><span class="sxs-lookup"><span data-stu-id="ac913-195">Steps out of the current function and up one level if the function is nested.</span></span> <span data-ttu-id="ac913-196">Se estiver no corpo principal, o script será executado ao final ou no próximo ponto de interrupção.</span><span class="sxs-lookup"><span data-stu-id="ac913-196">If in the main body, the script is executed to the end, or to the next breakpoint.</span></span> <span data-ttu-id="ac913-197">As instruções ignoradas são executadas, mas não percorridas.</span><span class="sxs-lookup"><span data-stu-id="ac913-197">The skipped statements are executed, but not stepped through.</span></span> | <span data-ttu-id="ac913-198">Pressione **Shift+F11** ou, no menu **Depurar**, clique em **Sair** ou então, no Painel Console, digite **O** e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ac913-198">Press **SHIFT+F11**, or on the **Debug** menu, click **Step Out**, or in the Console Pane, type **O** and press **ENTER**.</span></span> |
| <span data-ttu-id="ac913-199">**Continuar**</span><span class="sxs-lookup"><span data-stu-id="ac913-199">**Continue**</span></span> | <span data-ttu-id="ac913-200">Continua a execução até o final ou até o próximo ponto de interrupção.</span><span class="sxs-lookup"><span data-stu-id="ac913-200">Continues execution to the end, or to the next breakpoint.</span></span> <span data-ttu-id="ac913-201">As funções e invocações ignoradas são executadas, mas não são percorridas.</span><span class="sxs-lookup"><span data-stu-id="ac913-201">The skipped functions and invocations are executed, but not stepped through.</span></span> | <span data-ttu-id="ac913-202">Pressione **F5** ou, no menu **Depurar**, clique em **Executar/Continuar** ou então, no Painel Console, digite **C** e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ac913-202">Press **F5** or, on the **Debug** menu, click **Run/Continue**, or in the Console Pane, type **C** and press **ENTER**.</span></span> |

## <a name="how-to-display-the-values-of-variables-while-debugging"></a><span data-ttu-id="ac913-203">Como exibir os valores de variáveis durante a depuração</span><span class="sxs-lookup"><span data-stu-id="ac913-203">How to display the values of variables while debugging</span></span>

<span data-ttu-id="ac913-204">Você pode exibir os valores atuais das variáveis no script ao percorrer o código.</span><span class="sxs-lookup"><span data-stu-id="ac913-204">You can display the current values of variables in the script as you step through the code.</span></span>

### <a name="to-display-the-values-of-standard-variables"></a><span data-ttu-id="ac913-205">Para exibir os valores das variáveis padrão</span><span class="sxs-lookup"><span data-stu-id="ac913-205">To display the values of standard variables</span></span>

<span data-ttu-id="ac913-206">Use um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="ac913-206">Use one of the following methods:</span></span>

- <span data-ttu-id="ac913-207">No Painel de Script, passe o mouse sobre a variável para exibir seu valor como uma dica de ferramenta.</span><span class="sxs-lookup"><span data-stu-id="ac913-207">In the Script Pane, hover over the variable to display its value as a tool tip.</span></span>

- <span data-ttu-id="ac913-208">No Painel de Console, digite o nome da variável e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ac913-208">In the Console Pane, type the variable name and press **ENTER**.</span></span>

<span data-ttu-id="ac913-209">Todos os painéis no ISE estão sempre no mesmo escopo.</span><span class="sxs-lookup"><span data-stu-id="ac913-209">All panes in ISE are always in the same scope.</span></span> <span data-ttu-id="ac913-210">Portanto, enquanto você estiver depurando um script, os comandos que você digitar no Painel de Console são executados no escopo do script.</span><span class="sxs-lookup"><span data-stu-id="ac913-210">Therefore, while you are debugging a script, the commands that you type in the Console Pane run in script scope.</span></span> <span data-ttu-id="ac913-211">Isso permite usar o Painel de Console para encontrar os valores das variáveis e chamar funções definidas apenas no script.</span><span class="sxs-lookup"><span data-stu-id="ac913-211">This allows you to use the Console Pane to find the values of variables and call functions that are defined only in the script.</span></span>

### <a name="to-display-the-values-of-automatic-variables"></a><span data-ttu-id="ac913-212">Para exibir os valores de variáveis automáticas</span><span class="sxs-lookup"><span data-stu-id="ac913-212">To display the values of automatic variables</span></span>

<span data-ttu-id="ac913-213">Você pode usar o método anterior para exibir o valor de quase todas as variáveis enquanto está depurando um script.</span><span class="sxs-lookup"><span data-stu-id="ac913-213">You can use the preceding method to display the value of almost all variables while you are debugging a script.</span></span> <span data-ttu-id="ac913-214">No entanto, esses métodos não funcionam para as seguintes variáveis automáticas.</span><span class="sxs-lookup"><span data-stu-id="ac913-214">However, these methods do not work for the following automatic variables.</span></span>

- <span data-ttu-id="ac913-215">$_</span><span class="sxs-lookup"><span data-stu-id="ac913-215">$_</span></span>

- <span data-ttu-id="ac913-216">$Input</span><span class="sxs-lookup"><span data-stu-id="ac913-216">$Input</span></span>

- <span data-ttu-id="ac913-217">$MyInvocation</span><span class="sxs-lookup"><span data-stu-id="ac913-217">$MyInvocation</span></span>

- <span data-ttu-id="ac913-218">$PSBoundParameters</span><span class="sxs-lookup"><span data-stu-id="ac913-218">$PSBoundParameters</span></span>

- <span data-ttu-id="ac913-219">$Args</span><span class="sxs-lookup"><span data-stu-id="ac913-219">$Args</span></span>

<span data-ttu-id="ac913-220">Se você tentar exibir o valor de qualquer uma dessas variáveis, obterá o valor dessa variável para em um pipeline interno usado pelo depurador, não o valor da variável no script.</span><span class="sxs-lookup"><span data-stu-id="ac913-220">If you try to display the value of any of these variables, you get the value of that variable for in an internal pipeline the debugger uses, not the value of the variable in the script.</span></span> <span data-ttu-id="ac913-221">É possível contornar isso para algumas variáveis ($_, $Input, $MyInvocation, $PSBoundParameters e $Args) usando o seguinte método:</span><span class="sxs-lookup"><span data-stu-id="ac913-221">You can work around this for a few variables ($_, $Input, $MyInvocation, $PSBoundParameters, and $Args) by using the following method:</span></span>

1. <span data-ttu-id="ac913-222">No script, atribua o valor da variável automática a uma nova variável.</span><span class="sxs-lookup"><span data-stu-id="ac913-222">In the script, assign the value of the automatic variable to a new variable.</span></span>

2. <span data-ttu-id="ac913-223">Exiba o valor da nova variável passando o mouse sobre a nova variável no Painel de Script ou digitando a nova variável no Painel de Console.</span><span class="sxs-lookup"><span data-stu-id="ac913-223">Display the value of the new variable, either by hovering over the new variable in the Script Pane, or by typing the new variable in the Console Pane.</span></span>

<span data-ttu-id="ac913-224">Por exemplo, para exibir o valor da variável $MyInvocation, no script, atribua o valor a uma nova variável, como $scriptname, e passe o mouse sobre ou digite a variável $scriptname para exibir seu valor.</span><span class="sxs-lookup"><span data-stu-id="ac913-224">For example, to display the value of the $MyInvocation variable, in the script, assign the value to a new variable, such as $scriptname, and then hover over or type the $scriptname variable to display its value.</span></span>

```powershell
# In C:\ps-test\MyScript.ps1
$scriptname = $MyInvocation.MyCommand.Path
```

```output
# In the Console Pane:
PS> .\MyScript.ps1
PS> $scriptname
C:\ps-test\MyScript.ps1
```

## <a name="see-also"></a><span data-ttu-id="ac913-225">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="ac913-225">See Also</span></span>

- [<span data-ttu-id="ac913-226">Explorando o ISE do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac913-226">Exploring the Windows PowerShell ISE</span></span>](exploring-the-windows-powershell-ise.md)