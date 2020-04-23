---
title: Comunicação remota do WS-Management (WSMan) no PowerShell Core
description: Comunicação remota do WSMan no PowerShell Core
ms.date: 08/06/2018
ms.openlocfilehash: e5f00128bc8ebc1b432cc77a5896a9e09d684109
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2020
ms.locfileid: "62058872"
---
# <a name="ws-management-wsman-remoting-in-powershell-core"></a><span data-ttu-id="89a52-103">Comunicação remota do WS-Management (WSMan) no PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="89a52-103">WS-Management (WSMan) Remoting in PowerShell Core</span></span>

## <a name="instructions-to-create-a-remoting-endpoint"></a><span data-ttu-id="89a52-104">Instruções para criar um ponto de extremidade de comunicação remota</span><span class="sxs-lookup"><span data-stu-id="89a52-104">Instructions to Create a Remoting Endpoint</span></span>

<span data-ttu-id="89a52-105">O pacote do PowerShell Core para Windows inclui um plug-in WinRM (`pwrshplugin.dll`) e um script de instalação (`Install-PowerShellRemoting.ps1`) em `$PSHome`.</span><span class="sxs-lookup"><span data-stu-id="89a52-105">The PowerShell Core package for Windows includes a WinRM plug-in (`pwrshplugin.dll`) and an installation script (`Install-PowerShellRemoting.ps1`) in `$PSHome`.</span></span>
<span data-ttu-id="89a52-106">Esses arquivos permitem que o PowerShell aceite conexões remotas de entrada do PowerShell quando seu ponto de extremidade é especificado.</span><span class="sxs-lookup"><span data-stu-id="89a52-106">These files enable PowerShell to accept incoming PowerShell remote connections when its endpoint is specified.</span></span>

### <a name="motivation"></a><span data-ttu-id="89a52-107">Motivação</span><span class="sxs-lookup"><span data-stu-id="89a52-107">Motivation</span></span>

<span data-ttu-id="89a52-108">Uma instalação do PowerShell pode estabelecer sessões de PowerShell para computadores remotos usando `New-PSSession` e `Enter-PSSession`.</span><span class="sxs-lookup"><span data-stu-id="89a52-108">An installation of PowerShell can establish PowerShell sessions to remote computers using `New-PSSession` and `Enter-PSSession`.</span></span>
<span data-ttu-id="89a52-109">Para habilitá-lo a aceitar conexões remotas de entrada do PowerShell, o usuário deve criar um ponto de extremidade de comunicação remota do WinRM.</span><span class="sxs-lookup"><span data-stu-id="89a52-109">To enable it to accept incoming PowerShell remote connections, the user must create a WinRM remoting endpoint.</span></span>
<span data-ttu-id="89a52-110">Esse é um cenário de aceitação explícita em que o usuário executa Install-PowerShellRemoting.ps1 para criar o ponto de extremidade do WinRM.</span><span class="sxs-lookup"><span data-stu-id="89a52-110">This is an explicit opt-in scenario where the user runs Install-PowerShellRemoting.ps1 to create the WinRM endpoint.</span></span>
<span data-ttu-id="89a52-111">O script de instalação é uma solução de curto prazo, até que possamos adicionar funcionalidade adicional a `Enable-PSRemoting` para executar a mesma ação.</span><span class="sxs-lookup"><span data-stu-id="89a52-111">The installation script is a short-term solution until we add additional functionality to `Enable-PSRemoting` to perform the same action.</span></span>
<span data-ttu-id="89a52-112">Para obter mais detalhes, veja o problema [#1193](https://github.com/PowerShell/PowerShell/issues/1193).</span><span class="sxs-lookup"><span data-stu-id="89a52-112">For more details, please see issue [#1193](https://github.com/PowerShell/PowerShell/issues/1193).</span></span>

### <a name="script-actions"></a><span data-ttu-id="89a52-113">Ações de script</span><span class="sxs-lookup"><span data-stu-id="89a52-113">Script Actions</span></span>

<span data-ttu-id="89a52-114">O script</span><span class="sxs-lookup"><span data-stu-id="89a52-114">The script</span></span>

1. <span data-ttu-id="89a52-115">Cria um diretório para o plug-in em `$env:windir\System32\PowerShell`</span><span class="sxs-lookup"><span data-stu-id="89a52-115">Creates a directory for the plug-in within `$env:windir\System32\PowerShell`</span></span>
1. <span data-ttu-id="89a52-116">Copia pwrshplugin.dll para esse local</span><span class="sxs-lookup"><span data-stu-id="89a52-116">Copies pwrshplugin.dll to that location</span></span>
1. <span data-ttu-id="89a52-117">Gera um arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="89a52-117">Generates a configuration file</span></span>
1. <span data-ttu-id="89a52-118">Registra esse plug-in no WinRM</span><span class="sxs-lookup"><span data-stu-id="89a52-118">Registers that plug-in with WinRM</span></span>

### <a name="registration"></a><span data-ttu-id="89a52-119">Registro</span><span class="sxs-lookup"><span data-stu-id="89a52-119">Registration</span></span>

<span data-ttu-id="89a52-120">O script deve ser executado em uma sessão do PowerShell de nível de administrador e é executado em dois modos.</span><span class="sxs-lookup"><span data-stu-id="89a52-120">The script must be executed within an Administrator-level PowerShell session and runs in two modes.</span></span>

#### <a name="executed-by-the-instance-of-powershell-that-it-will-register"></a><span data-ttu-id="89a52-121">Executado pela instância do PowerShell que ele registrará</span><span class="sxs-lookup"><span data-stu-id="89a52-121">Executed by the instance of PowerShell that it will register</span></span>

```powershell
Install-PowerShellRemoting.ps1
```

#### <a name="executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register"></a><span data-ttu-id="89a52-122">Executado por outra instância do PowerShell em nome de instância que ele registrará</span><span class="sxs-lookup"><span data-stu-id="89a52-122">Executed by another instance of PowerShell on behalf of the instance that it will register</span></span>

```powershell
<path to powershell>\Install-PowerShellRemoting.ps1 -PowerShellHome "<absolute path to the instance's $PSHOME>"
```

<span data-ttu-id="89a52-123">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="89a52-123">For Example:</span></span>

```powershell
Set-Location -Path 'C:\Program Files\PowerShell\6.0.0\'
.\Install-PowerShellRemoting.ps1 -PowerShellHome "C:\Program Files\PowerShell\6.0.0\"
```

<span data-ttu-id="89a52-124">**Observação:** o script de registro de comunicação remota reiniciará o WinRM. Dessa forma, todas as sessões PSRP existentes serão encerradas logo depois que o script for executado.</span><span class="sxs-lookup"><span data-stu-id="89a52-124">**NOTE:** The remoting registration script will restart WinRM, so all existing PSRP sessions will terminate immediately after the script is run.</span></span> <span data-ttu-id="89a52-125">Se executar durante uma sessão remota, isso encerrará a conexão.</span><span class="sxs-lookup"><span data-stu-id="89a52-125">If run during a remote session, this will terminate the connection.</span></span>

## <a name="how-to-connect-to-the-new-endpoint"></a><span data-ttu-id="89a52-126">Como se conectar ao novo ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="89a52-126">How to Connect to the New Endpoint</span></span>

<span data-ttu-id="89a52-127">Crie uma sessão do PowerShell para o novo ponto de extremidade do PowerShell, especificando `-ConfigurationName "some endpoint name"`.</span><span class="sxs-lookup"><span data-stu-id="89a52-127">Create a PowerShell session to the new PowerShell endpoint by specifying `-ConfigurationName "some endpoint name"`.</span></span> <span data-ttu-id="89a52-128">Para se conectar à instância do PowerShell do exemplo acima, use:</span><span class="sxs-lookup"><span data-stu-id="89a52-128">To connect to the PowerShell instance from the example above, use either:</span></span>

```powershell
New-PSSession ... -ConfigurationName "powershell.6.0.0"
Enter-PSSession ... -ConfigurationName "powershell.6.0.0"
```

<span data-ttu-id="89a52-129">Observe que as invocações `New-PSSession` e `Enter-PSSession` que não especificam `-ConfigurationName` têm como destino o ponto de extremidade padrão do PowerShell, `microsoft.powershell`.</span><span class="sxs-lookup"><span data-stu-id="89a52-129">Note that `New-PSSession` and `Enter-PSSession` invocations that do not specify `-ConfigurationName` will target the default PowerShell endpoint, `microsoft.powershell`.</span></span>