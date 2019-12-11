---
ms.date: 08/27/2018
keywords: powershell, cmdlet
title: Usando variáveis para armazenar objetos
ms.openlocfilehash: 2d20d84e48d3f68cab5c1ffa05d689b46415ebc8
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "67030361"
---
# <a name="using-variables-to-store-objects"></a><span data-ttu-id="2b037-103">Usando variáveis para armazenar objetos</span><span class="sxs-lookup"><span data-stu-id="2b037-103">Using variables to store objects</span></span>

<span data-ttu-id="2b037-104">O PowerShell funciona com objetos.</span><span class="sxs-lookup"><span data-stu-id="2b037-104">PowerShell works with objects.</span></span> <span data-ttu-id="2b037-105">O PowerShell permite que você crie objetos nomeados, conhecidos como variáveis.</span><span class="sxs-lookup"><span data-stu-id="2b037-105">PowerShell lets you create named objects known as variables.</span></span>
<span data-ttu-id="2b037-106">Os nomes de variáveis podem incluir o caractere de sublinhado e quaisquer caracteres alfanuméricos.</span><span class="sxs-lookup"><span data-stu-id="2b037-106">Variable names can include the underscore character and any alphanumeric characters.</span></span> <span data-ttu-id="2b037-107">Quando usada no PowerShell, uma variável é sempre especificada usando o caractere \$ seguido pelo nome da variável.</span><span class="sxs-lookup"><span data-stu-id="2b037-107">When used in PowerShell, a variable is always specified using the \$ character followed by variable name.</span></span>

## <a name="creating-a-variable"></a><span data-ttu-id="2b037-108">Criar uma variável</span><span class="sxs-lookup"><span data-stu-id="2b037-108">Creating a variable</span></span>

<span data-ttu-id="2b037-109">Você pode criar uma variável digitando um nome de variável válido:</span><span class="sxs-lookup"><span data-stu-id="2b037-109">You can create a variable by typing a valid variable name:</span></span>

```
PS> $loc
PS>
```

<span data-ttu-id="2b037-110">Este exemplo não retorna resultados porque `$loc` não tem um valor.</span><span class="sxs-lookup"><span data-stu-id="2b037-110">This example returns no result because `$loc` doesn't have a value.</span></span> <span data-ttu-id="2b037-111">Você pode criar uma variável e atribuir a ela um valor na mesma etapa.</span><span class="sxs-lookup"><span data-stu-id="2b037-111">You can create a variable and assign it a value in the same step.</span></span> <span data-ttu-id="2b037-112">O PowerShell só criará a variável se ela não existir.</span><span class="sxs-lookup"><span data-stu-id="2b037-112">PowerShell only creates the variable if it doesn't exist.</span></span>
<span data-ttu-id="2b037-113">Caso contrário, ele atribuirá o valor especificado à variável existente.</span><span class="sxs-lookup"><span data-stu-id="2b037-113">Otherwise, it assigns the specified value to the existing variable.</span></span> <span data-ttu-id="2b037-114">O exemplo a seguir armazena o local atual na variável `$loc`:</span><span class="sxs-lookup"><span data-stu-id="2b037-114">The following example stores the current location in the variable `$loc`:</span></span>

```powershell
$loc = Get-Location
```

<span data-ttu-id="2b037-115">O PowerShell não exibe qualquer saída quando você digita esse comando.</span><span class="sxs-lookup"><span data-stu-id="2b037-115">PowerShell displays no output when you type this command.</span></span> <span data-ttu-id="2b037-116">O PowerShell envia a saída de "Get-Location" para `$loc`.</span><span class="sxs-lookup"><span data-stu-id="2b037-116">PowerShell sends the output of 'Get-Location' to `$loc`.</span></span> <span data-ttu-id="2b037-117">No PowerShell, os dados que não estão atribuídos ou redirecionados são enviados para a tela.</span><span class="sxs-lookup"><span data-stu-id="2b037-117">In PowerShell, data that isn't assigned or redirected is sent to the screen.</span></span> <span data-ttu-id="2b037-118">A sua localização atual aparece ao digitar `$loc`:</span><span class="sxs-lookup"><span data-stu-id="2b037-118">Typing `$loc` shows your current location:</span></span>

```
PS> $loc

Path
----
C:\temp
```

<span data-ttu-id="2b037-119">Use `Get-Member` para exibir informações sobre o conteúdo das variáveis.</span><span class="sxs-lookup"><span data-stu-id="2b037-119">You can use `Get-Member` to display information about the contents of variables.</span></span> <span data-ttu-id="2b037-120">`Get-Member` mostra que `$loc` é um objeto **PathInfo**, assim como a saída de `Get-Location`:</span><span class="sxs-lookup"><span data-stu-id="2b037-120">`Get-Member` shows you that `$loc` is a **PathInfo** object, just like the output from `Get-Location`:</span></span>

```powershell
PS> $loc | Get-Member -MemberType Property

   TypeName: System.Management.Automation.PathInfo

Name         MemberType Definition
----         ---------- ----------
Drive        Property   System.Management.Automation.PSDriveInfo Drive {get;}
Path         Property   System.String Path {get;}
Provider     Property   System.Management.Automation.ProviderInfo Provider {...
ProviderPath Property   System.String ProviderPath {get;}
```

## <a name="manipulating-variables"></a><span data-ttu-id="2b037-121">Manipular variáveis</span><span class="sxs-lookup"><span data-stu-id="2b037-121">Manipulating variables</span></span>

<span data-ttu-id="2b037-122">O PowerShell fornece vários comandos para manipular variáveis.</span><span class="sxs-lookup"><span data-stu-id="2b037-122">PowerShell provides several commands to manipulate variables.</span></span> <span data-ttu-id="2b037-123">Você pode ver uma listagem completa em um formato legível digitando:</span><span class="sxs-lookup"><span data-stu-id="2b037-123">You can see a complete listing in a readable form by typing:</span></span>

```powershell
Get-Command -Noun Variable | Format-Table -Property Name,Definition -AutoSize -Wrap
```

<span data-ttu-id="2b037-124">O PowerShell também cria diversas variáveis definidas pelo sistema.</span><span class="sxs-lookup"><span data-stu-id="2b037-124">PowerShell also creates several system-defined variables.</span></span> <span data-ttu-id="2b037-125">Você pode usar o cmdlet `Remove-Variable` para remover as variáveis que não são controladas pelo PowerShell da sessão atual.</span><span class="sxs-lookup"><span data-stu-id="2b037-125">You can use the `Remove-Variable` cmdlet to remove variables, which are not controlled by PowerShell, from the current session.</span></span> <span data-ttu-id="2b037-126">Digite o seguinte comando a seguir para limpar todas as variáveis:</span><span class="sxs-lookup"><span data-stu-id="2b037-126">Type the following command to clear all variables:</span></span>

```powershell
Remove-Variable -Name * -Force -ErrorAction SilentlyContinue
```

<span data-ttu-id="2b037-127">Após a execução do comando anterior, o cmdlet `Get-Variable` mostra as variáveis de sistema do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2b037-127">After running the previous command, the `Get-Variable` cmdlet shows the PowerShell system variables.</span></span>

<span data-ttu-id="2b037-128">O PowerShell também cria uma unidade de variável.</span><span class="sxs-lookup"><span data-stu-id="2b037-128">PowerShell also creates a variable drive.</span></span> <span data-ttu-id="2b037-129">Use o exemplo a seguir para exibir todas as variáveis do PowerShell usando a unidade de variável:</span><span class="sxs-lookup"><span data-stu-id="2b037-129">Use the following example to display all PowerShell variables using the variable drive:</span></span>

```powershell
Get-ChildItem variable:
```

## <a name="using-cmdexe-variables"></a><span data-ttu-id="2b037-130">Usar variáveis do cmd.exe</span><span class="sxs-lookup"><span data-stu-id="2b037-130">Using cmd.exe variables</span></span>

<span data-ttu-id="2b037-131">O PowerShell pode usar as mesmas variáveis de ambiente disponíveis a qualquer processo do Windows, incluindo **cmd.exe**.</span><span class="sxs-lookup"><span data-stu-id="2b037-131">PowerShell can use the same environment variables available to any Windows process, including **cmd.exe**.</span></span> <span data-ttu-id="2b037-132">Essas variáveis são expostas por meio de uma unidade chamada `env:`.</span><span class="sxs-lookup"><span data-stu-id="2b037-132">These variables are exposed through a drive named `env:`.</span></span> <span data-ttu-id="2b037-133">Exiba essas variáveis digitando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="2b037-133">You can view these variables by typing the following command:</span></span>

```powershell
Get-ChildItem env:
```

<span data-ttu-id="2b037-134">Os cmdlets `*-Variable` padrão não são projetados para funcionar com variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="2b037-134">The standard `*-Variable` cmdlets aren't designed to work with environment variables.</span></span> <span data-ttu-id="2b037-135">Variáveis de ambiente são acessadas usando o prefixo de unidade `env:`.</span><span class="sxs-lookup"><span data-stu-id="2b037-135">Environment variables are accessed using the `env:` drive prefix.</span></span> <span data-ttu-id="2b037-136">Por exemplo, a variável **% SystemRoot %** no **cmd.exe** contém nome do diretório raiz do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="2b037-136">For example, the **%SystemRoot%** variable in **cmd.exe** contains the operating system's root directory name.</span></span> <span data-ttu-id="2b037-137">No PowerShell, use `$env:SystemRoot` para acessar o mesmo valor.</span><span class="sxs-lookup"><span data-stu-id="2b037-137">In PowerShell, you use `$env:SystemRoot` to access the same value.</span></span>

```
PS> $env:SystemRoot
C:\WINDOWS
```

<span data-ttu-id="2b037-138">Você também pode criar e modificar variáveis de ambiente do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2b037-138">You can also create and modify environment variables from within PowerShell.</span></span> <span data-ttu-id="2b037-139">As variáveis de ambiente do PowerShell seguem as mesmas regras para variáveis de ambiente usadas em outro lugar no sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="2b037-139">Environment variables in PowerShell follow the same rules for environment variables used elsewhere in the operating system.</span></span> <span data-ttu-id="2b037-140">O exemplo a seguir cria uma nova variável de ambiente:</span><span class="sxs-lookup"><span data-stu-id="2b037-140">The following example creates a new environment variable:</span></span>

```powershell
$env:LIB_PATH='/usr/local/lib'
```

<span data-ttu-id="2b037-141">Embora não seja necessário, é comum usar letras maiúsculas nos nomes de variáveis de ambientes.</span><span class="sxs-lookup"><span data-stu-id="2b037-141">Though not required, it's common for environment variable names to use all uppercase letters.</span></span>
