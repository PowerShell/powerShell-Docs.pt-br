---
ms.date: 06/12/2017
keywords: wmf,powershell,instalação
title: Problemas conhecidos no WMF 5.0
ms.openlocfilehash: 1db656884736c742ef78354b7452879e319d4a0a
ms.sourcegitcommit: 2aec310ad0c0b048400cb56f6fa64c1e554c812a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2020
ms.locfileid: "83809082"
---
# <a name="known-issues-in-wmf-50"></a><span data-ttu-id="f1ba3-103">Problemas conhecidos no WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="f1ba3-103">Known Issues in WMF 5.0</span></span>

## <a name="powershell-shortcuts-are-broken-when-used-for-the-first-time"></a><span data-ttu-id="f1ba3-104">Os Atalhos do PowerShell são desfeitos quando usados pela primeira vez</span><span class="sxs-lookup"><span data-stu-id="f1ba3-104">PowerShell Shortcuts are broken when used for the first time</span></span>

<span data-ttu-id="f1ba3-105">**Resolução:** execute uma das seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="f1ba3-105">**Resolution:** Perform one of the following actions:</span></span>

1. <span data-ttu-id="f1ba3-106">Clique com o botão direito do mouse no atalho do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-106">Right click on the PowerShell shortcut.</span></span> <span data-ttu-id="f1ba3-107">Escolha “Windows PowerShell” para iniciar em um modo sem privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-107">Select "Windows PowerShell" to launch in a non-elevated mode.</span></span>
2. <span data-ttu-id="f1ba3-108">Clique com o botão direito do mouse no atalho do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-108">Right click on the PowerShell shortcut.</span></span> <span data-ttu-id="f1ba3-109">Clique com o botão direito do mouse em “Windows PowerShell” e escolha “Executar como Administrador” para iniciar em um modo com privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-109">Right click on "Windows PowerShell" and select "Run As Administrator" to launch in an elevated mode.</span></span>

<span data-ttu-id="f1ba3-110">Depois de executar uma das ações acima, os atalhos do PowerShell funcionarão.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-110">Once you have performed either of the above actions, the PowerShell shortcuts will work.</span></span> <span data-ttu-id="f1ba3-111">Essas ações precisarão ser executadas apenas uma vez.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-111">These actions need to be performed only once.</span></span>

## <a name="powershell-modules-and-dsc-resources-report-errors-about-executionpolicy-on-windows-7"></a><span data-ttu-id="f1ba3-112">Os Módulos PowerShell e os Recursos DSC relatam erros sobre ExecutionPolicy no Windows 7</span><span class="sxs-lookup"><span data-stu-id="f1ba3-112">PowerShell Modules and DSC Resources report errors about ExecutionPolicy on Windows 7</span></span>

<span data-ttu-id="f1ba3-113">No Windows 7, o uso de módulos do PowerShell e recursos de DSC pode fazer com que erros sobre ExecutionPolicy sejam relatados.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-113">On Windows 7, using PowerShell modules and DSC resources may result in errors reported about ExecutionPolicy.</span></span>

<span data-ttu-id="f1ba3-114">**Resolução:** defina ExecutionPolicy como **RemoteSigned** executando o seguinte comando em uma sessão do PowerShell com privilégios elevados (Executar como Administrador):</span><span class="sxs-lookup"><span data-stu-id="f1ba3-114">**Resolution:** Set the ExecutionPolicy to **RemoteSigned** by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```

## <a name="connecting-to-an-old-remote-exchange-endpoint-causes-a-crash"></a><span data-ttu-id="f1ba3-115">Conectar-se a um ponto de extremidade remoto antigo do Exchange causa uma falha</span><span class="sxs-lookup"><span data-stu-id="f1ba3-115">Connecting to an old remote Exchange endpoint causes a crash</span></span>

<span data-ttu-id="f1ba3-116">O ponto de extremidade antigo do Exchange redireciona para um novo ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-116">The old Exchange endpoint redirects to a new endpoint.</span></span> <span data-ttu-id="f1ba3-117">Há um bug na lógica de redirecionamento que resulta em uma falha.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-117">There is a bug in the redirection logic that results in a crash.</span></span>

<span data-ttu-id="f1ba3-118">**Resolução:** conecte-se diretamente ao novo ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-118">**Resolution:** Connect directly to the new endpoint.</span></span>

## <a name="software-inventory-logging-feature-is-erroneously-stopped-after-wmf-50-installation-on-windows-server-2012-r2"></a><span data-ttu-id="f1ba3-119">O recurso de Log de Inventário de Software é interrompido incorretamente após a instalação do WMF 5.0 no Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="f1ba3-119">Software Inventory Logging feature is erroneously stopped after WMF 5.0 installation on Windows Server 2012 R2</span></span>

<span data-ttu-id="f1ba3-120">Ao instalar o WMF 5.0 em um Windows Server 2012 R2 que já está executando o SIL, o recurso de Log de Inventário de Software será interrompido incorretamente após a instalação.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-120">When installing WMF 5.0 on a Windows Server 2012 R2 that is already running SIL, the Software Inventory Logging feature is erroneously stopped after installation.</span></span>

<span data-ttu-id="f1ba3-121">**Resolução:** execute o cmdlet `Start-SilLogging` uma vez após a instalação do WMF, pois o processo de instalação interromperá incorretamente o recurso de Log de Inventário de Software.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-121">**Resolution:** Run the `Start-SilLogging` cmdlet once after the WMF installation, as the installation process will errantly stop the Software Inventory Logging feature.</span></span>

## <a name="get-childitem-does-not-work-if--literalpath-and--recurse-are-used-together"></a><span data-ttu-id="f1ba3-122">`Get-ChildItem` não funcionará se -LiteralPath e -Recurse forem usados juntos</span><span class="sxs-lookup"><span data-stu-id="f1ba3-122">`Get-ChildItem` does not work if -LiteralPath and -Recurse are used together</span></span>

<span data-ttu-id="f1ba3-123">Caso um nome de diretório contenha um caractere curinga inválido, `Get-ChildItem` não produzirá os resultados esperados quando -LiteralPath e -Recurse são usados juntos.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-123">If a directory name contains an invalid wildcard character, then `Get-ChildItem` will not produce expected results when both -LiteralPath and -Recurse are used together.</span></span>

<span data-ttu-id="f1ba3-124">**Resolução:** a solução alternativa não ideal, mas atual, é implementar a recursão no script em vez de depender do cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-124">**Resolution:** Not ideal, but current workaround is to implement recursion in the script rather than rely on the cmdlet.</span></span>

## <a name="sysprep-fails-after-wmf-50-installation"></a><span data-ttu-id="f1ba3-125">Falha de sysprep após instalação do WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="f1ba3-125">Sysprep fails after WMF 5.0 installation</span></span>

<span data-ttu-id="f1ba3-126">Há duas soluções para este problema, dependendo da versão do Windows Server que você está executando.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-126">There are two workarounds for this issue depending on the version of Windows Server you are running.</span></span>

<span data-ttu-id="f1ba3-127">**Resolução:**</span><span class="sxs-lookup"><span data-stu-id="f1ba3-127">**Resolution:**</span></span>

- <span data-ttu-id="f1ba3-128">Para sistemas executando o **Windows Server 2008 R2**</span><span class="sxs-lookup"><span data-stu-id="f1ba3-128">For systems running **Windows Server 2008 R2**</span></span>
  1. <span data-ttu-id="f1ba3-129">Abrir o PowerShell como um administrador</span><span class="sxs-lookup"><span data-stu-id="f1ba3-129">Open PowerShell as an administrator</span></span>
  2. <span data-ttu-id="f1ba3-130">Executar o seguinte comando</span><span class="sxs-lookup"><span data-stu-id="f1ba3-130">Run the following command</span></span>

     ```powershell
     Set-SilLogging -TargetUri https://BlankTarget -CertificateThumbprint 0123456789
     ```

  3. <span data-ttu-id="f1ba3-131">Execute o comando e ignore o erro, uma vez que são esperados.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-131">Run the command and ignore the error, as they are expected.</span></span>

     ```powershell
     Publish-SilData
     ```

  4. <span data-ttu-id="f1ba3-132">Exclua os arquivos no diretório \Windows\System32\Logfiles\SIL\\</span><span class="sxs-lookup"><span data-stu-id="f1ba3-132">Delete the files in  \Windows\System32\Logfiles\SIL\ directory</span></span>

     ```powershell
     Remove-Item -Recurse $env:SystemRoot\System32\Logfiles\SIL\
     ```

  5. <span data-ttu-id="f1ba3-133">Instale todas as atualizações importantes do Windows disponíveis e comece a operação de Sysprep normalmente.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-133">Install all available important Windows Updates, and begin Sysyprep operation normally.</span></span>

- <span data-ttu-id="f1ba3-134">Para sistemas executando o **Windows Server 2012**</span><span class="sxs-lookup"><span data-stu-id="f1ba3-134">For systems running **Windows Server 2012**</span></span>
  1. <span data-ttu-id="f1ba3-135">Depois de instalar o WMF 5.0 no servidor a ser Sysprep, faça logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-135">After installing WMF 5.0 on the server to be Sysprep'd, login as administrator.</span></span>
  2. <span data-ttu-id="f1ba3-136">Copie Generize.xml do diretório `\Windows\System32\Sysprep\ActionFiles\` para um local fora do diretório do Windows, `C:\` por exemplo.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-136">Copy Generize.xml from directory `\Windows\System32\Sysprep\ActionFiles\` to a location outside of the Windows directory, `C:\` for example.</span></span>
  3. <span data-ttu-id="f1ba3-137">Abra sua cópia Generalize.xml com bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-137">Open your Generalize.xml copy with notepad.</span></span>
  4. <span data-ttu-id="f1ba3-138">Localize e remova o texto que segue, uma instância de cada precisa de ser excluída (estarão perto do fim do documento).</span><span class="sxs-lookup"><span data-stu-id="f1ba3-138">Find and remove the following text, one instance of each needs to be deleted (they will be near the end of the document).</span></span>

     ```xml
     <sysprepOrder order="0x3200"></sysprepOrder>
     <sysprepOrder order="0x3300"></sysprepOrder>
     ```

  5. <span data-ttu-id="f1ba3-139">Salve a cópia editada de Generalize.xml e feche o arquivo.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-139">Save the edited copy of Generalize.xml and close the file.</span></span>
  6. <span data-ttu-id="f1ba3-140">Abra um prompt de comando como administrador</span><span class="sxs-lookup"><span data-stu-id="f1ba3-140">Open a command prompt as administrator</span></span>
  7. <span data-ttu-id="f1ba3-141">Execute o seguinte comando para se apropriar do arquivo Generalize.xml na pasta system32:</span><span class="sxs-lookup"><span data-stu-id="f1ba3-141">Run the following command to take ownership of the Generalize.xml file in system32 folder:</span></span>

     ```powershell
     Takeown /f C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml
     ```

  8. <span data-ttu-id="f1ba3-142">Execute o seguinte comando para definir a permissão adequada no arquivo:</span><span class="sxs-lookup"><span data-stu-id="f1ba3-142">Run the following command to set appropriate permission on the file:</span></span>

     ```powershell
     Cacls C:\Windows\System32\ Sysprep\ActionFiles\Generalize.xml /G `<AdministratorUserName>`:F
     ```

     - <span data-ttu-id="f1ba3-143">Responda Sim ao pedido de confirmação.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-143">Answer Yes at the prompt for confirmation.</span></span>
     - <span data-ttu-id="f1ba3-144">Observe que `<AdministratorUserName>` deve ser substituído pelo nome de usuário administrador do computador.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-144">Note that `<AdministratorUserName>` should be replaced by the username who is administrator on the machine.</span></span> <span data-ttu-id="f1ba3-145">Por exemplo, "Administrador".</span><span class="sxs-lookup"><span data-stu-id="f1ba3-145">For example, "Administrator".</span></span>

  9. <span data-ttu-id="f1ba3-146">Copie o arquivo editado e salvo no diretório de Sysprep usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="f1ba3-146">Copy the file you edited and saved over to the Sysprep directory using the following command:</span></span>

     ```powershell
     xcopy C:\Generalize.xml C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml
     ```

     - <span data-ttu-id="f1ba3-147">Responda Sim para substituir (observe que se não houver nenhum pedido para substituir, verifique com atenção o caminho inserido).</span><span class="sxs-lookup"><span data-stu-id="f1ba3-147">Answer Yes to overwrite (note that if there is no prompt to overwrite, double check the path entered).</span></span>
     - <span data-ttu-id="f1ba3-148">Assume que sua cópia editada de Generalize.xml foi copiado no C:\.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-148">Assumes your edited copy of Generalize.xml was copied to C:\ .</span></span>

  10. <span data-ttu-id="f1ba3-149">Generalize.xml é atualizado com a solução alternativa.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-149">Generalize.xml is now updated with the workaround.</span></span> <span data-ttu-id="f1ba3-150">Executar o Sysprep com a opção Generalizar habilitada.</span><span class="sxs-lookup"><span data-stu-id="f1ba3-150">Please run Sysprep with the generalize option enabled.</span></span>
