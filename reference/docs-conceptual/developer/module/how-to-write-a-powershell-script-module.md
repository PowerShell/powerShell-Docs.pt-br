---
title: Como escrever um módulo de script do PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ed7645ea-5e52-4a45-81a7-aa3c2d605cde
caps.latest.revision: 16
ms.openlocfilehash: b2a929a1724f77f0516ad24cfd90f6d6053ed19e
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72360685"
---
# <a name="how-to-write-a-powershell-script-module"></a><span data-ttu-id="be2de-102">Como escrever um módulo de script do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="be2de-102">How to Write a PowerShell Script Module</span></span>

<span data-ttu-id="be2de-103">Um módulo de script é essencialmente qualquer script do PowerShell válido salvo em uma extensão. psm1.</span><span class="sxs-lookup"><span data-stu-id="be2de-103">A script module is essentially any valid PowerShell script saved in a .psm1 extension.</span></span> <span data-ttu-id="be2de-104">Essa extensão permite que o mecanismo do PowerShell use várias regras e cmdlets em seu arquivo.</span><span class="sxs-lookup"><span data-stu-id="be2de-104">This extension allows the PowerShell engine to use a number of rules and cmdlets on your file.</span></span> <span data-ttu-id="be2de-105">A maioria desses recursos está lá para ajudá-lo a instalar seu código em outros sistemas, bem como gerenciar o escopo.</span><span class="sxs-lookup"><span data-stu-id="be2de-105">Most of these capabilities are there to help you install your code on other systems, as well as manage scoping.</span></span> <span data-ttu-id="be2de-106">Você também pode usar um arquivo de manifesto de módulo, que pode descrever as instalações e soluções ainda mais complexas.</span><span class="sxs-lookup"><span data-stu-id="be2de-106">You can also use a module manifest file, which can describe even more complex installations and solutions.</span></span>

## <a name="writing-a-powershell-script-module"></a><span data-ttu-id="be2de-107">Gravando um módulo de script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="be2de-107">Writing a PowerShell Script Module</span></span>

<span data-ttu-id="be2de-108">Você cria um módulo de script salvando um script do PowerShell válido em um arquivo. psm1 e salvando esse arquivo em um diretório localizado onde o PowerShell pode encontrá-lo.</span><span class="sxs-lookup"><span data-stu-id="be2de-108">You create a script module by saving a valid PowerShell script to a .psm1 file, and then saving that file in a directory located where PowerShell can find it.</span></span> <span data-ttu-id="be2de-109">Nessa pasta, você também pode inserir todos os recursos necessários para executar o script, bem como um arquivo de manifesto que descreva ao PowerShell como o módulo funciona.</span><span class="sxs-lookup"><span data-stu-id="be2de-109">In that folder you can also place any resources you need to run your script, as well as a manifest file that describes to PowerShell how your module works.</span></span>

#### <a name="to-create-a-basic-powershell-module"></a><span data-ttu-id="be2de-110">Para criar um módulo do PowerShell básico</span><span class="sxs-lookup"><span data-stu-id="be2de-110">To create a basic PowerShell Module</span></span>

1. <span data-ttu-id="be2de-111">Pegue um script do PowerShell existente e salve o script com uma extensão. psm1.</span><span class="sxs-lookup"><span data-stu-id="be2de-111">Take an existing PowerShell script, and save the script with a .psm1 extension.</span></span>

   <span data-ttu-id="be2de-112">Salvar um script com a extensão. psm1 significa que você pode usar os cmdlets do módulo, como [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module), nele.</span><span class="sxs-lookup"><span data-stu-id="be2de-112">Saving a script with the .psm1 extension means that you can use the module cmdlets, such as [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module), on it.</span></span> <span data-ttu-id="be2de-113">Esses cmdlets existem principalmente para que você possa facilmente importar e exportar seu código para os sistemas de outros usuários.</span><span class="sxs-lookup"><span data-stu-id="be2de-113">These cmdlets exist primarily so that you can easily import and export your code onto other user's systems.</span></span> <span data-ttu-id="be2de-114">(A solução alternativa seria carregar seu código em outros sistemas e, em seguida, colocar o código-fonte em uma memória ativa, o que não é uma solução particularmente escalonável.) Para obter mais informações, consulte a seção **cmdlets e variáveis de módulo** em [módulos do Windows PowerShell](./understanding-a-windows-powershell-module.md) Observe que, por padrão, todas as funções em seu script podem ser acessadas por usuários que importam o arquivo. psm1, mas as propriedades não são.</span><span class="sxs-lookup"><span data-stu-id="be2de-114">(The alternate solution would be to load up your code on other systems and then dot-source it into active memory, which isn't a particularly scalable solution.) For more information see the **Module Cmdlets and Variables** section in [Windows PowerShell Modules](./understanding-a-windows-powershell-module.md) Note that, by default, all functions in your script are accessible to users who import your .psm1 file, but properties are not.</span></span>

   <span data-ttu-id="be2de-115">Um exemplo de script do PowerShell, intitulado `Show-Calendar`, está disponível no final deste tópico.</span><span class="sxs-lookup"><span data-stu-id="be2de-115">An example PowerShell script, entitled `Show-Calendar`, is available at the end of this topic.</span></span>

   ```powershell
   function Show-Calendar {
   param(
       [DateTime] $start = [DateTime]::Today,
       [DateTime] $end = $start,
       $firstDayOfWeek,
       [int[]] $highlightDay,
       [string[]] $highlightDate = [DateTime]::Today.ToString()
       )

       #actual code for the function goes here see the end of the topic for the complete code sample
   }
   ```

2. <span data-ttu-id="be2de-116">Para controlar o acesso do usuário a determinadas funções ou propriedades, chame [Export-ModuleMember](/powershell/module/Microsoft.PowerShell.Core/Export-ModuleMember) no final do script.</span><span class="sxs-lookup"><span data-stu-id="be2de-116">To control user access to certain functions or properties, call [Export-ModuleMember](/powershell/module/Microsoft.PowerShell.Core/Export-ModuleMember) at the end of your script.</span></span>

   <span data-ttu-id="be2de-117">O código de exemplo na parte inferior da página tem apenas uma função, que por padrão seria exposta.</span><span class="sxs-lookup"><span data-stu-id="be2de-117">The example code at the bottom of the page has only one function, which by default would be exposed.</span></span> <span data-ttu-id="be2de-118">No entanto, é recomendável que você chame explicitamente quais funções deseja expor, conforme descrito no código a seguir:</span><span class="sxs-lookup"><span data-stu-id="be2de-118">However, it is recommended that you explicitly call out which functions you wish to expose, as described in the following code:</span></span>

   ```powershell
   function Show-Calendar {
         }
   Export-ModuleMember -Function Show-Calendar
   ```

   <span data-ttu-id="be2de-119">Você também pode restringir o que é importado usando um manifesto de módulo.</span><span class="sxs-lookup"><span data-stu-id="be2de-119">You can also restrict what is imported using a module manifest.</span></span> <span data-ttu-id="be2de-120">Para obter mais informações, consulte [importando um módulo do PowerShell](./importing-a-powershell-module.md) e [como escrever um manifesto de módulo do PowerShell](./how-to-write-a-powershell-module-manifest.md).</span><span class="sxs-lookup"><span data-stu-id="be2de-120">For more information, see [Importing a PowerShell Module](./importing-a-powershell-module.md) and [How to Write a PowerShell Module Manifest](./how-to-write-a-powershell-module-manifest.md).</span></span>

3. <span data-ttu-id="be2de-121">Se você tiver módulos que seu próprio módulo precisa ter carregado, você poderá usá-los com uma chamada para `Import-Module`, na parte superior do seu próprio módulo.</span><span class="sxs-lookup"><span data-stu-id="be2de-121">If you have modules that your own module needs to have loaded, you can use them with a call to `Import-Module`, at the top of your own module.</span></span>

   <span data-ttu-id="be2de-122">`Import-Module` é um cmdlet que importa um módulo de destino para um sistema.</span><span class="sxs-lookup"><span data-stu-id="be2de-122">`Import-Module` is a cmdlet that imports a targeted module onto a system.</span></span> <span data-ttu-id="be2de-123">Como tal, ele também é usado posteriormente no procedimento para instalar seu próprio módulo também.</span><span class="sxs-lookup"><span data-stu-id="be2de-123">As such, it is also used at a later point in the procedure to install your own module as well.</span></span> <span data-ttu-id="be2de-124">O código de exemplo na parte inferior desta página não usa nenhum módulo de importação.</span><span class="sxs-lookup"><span data-stu-id="be2de-124">The sample code at the bottom of this page does not use any import modules.</span></span> <span data-ttu-id="be2de-125">No entanto, se ele fosse listado na parte superior do arquivo, conforme descrito no código a seguir:</span><span class="sxs-lookup"><span data-stu-id="be2de-125">If it did, however, they would be listed at the top of the file, as described in the following code:</span></span>

   ```powershell
   Import-Module GenericModule
   ```

4. <span data-ttu-id="be2de-126">Para descrever seu módulo para o sistema de ajuda do PowerShell, você pode usar comentários de ajuda padrão dentro do arquivo ou criar um arquivo de ajuda adicional.</span><span class="sxs-lookup"><span data-stu-id="be2de-126">To describe your module to the PowerShell Help system, you can either use standard help comments inside the file, or create an additional Help file.</span></span>

   <span data-ttu-id="be2de-127">O exemplo de código na parte inferior deste tópico inclui as informações de ajuda nos comentários.</span><span class="sxs-lookup"><span data-stu-id="be2de-127">The code sample at the bottom of this topic includes the help information in the comments.</span></span> <span data-ttu-id="be2de-128">Você também pode gravar arquivos XML expandidos que contêm conteúdo de ajuda adicional.</span><span class="sxs-lookup"><span data-stu-id="be2de-128">You could also write expanded XML files that contain additional help content.</span></span> <span data-ttu-id="be2de-129">Para obter mais informações, consulte [escrevendo ajuda para módulos do Windows PowerShell](./writing-help-for-windows-powershell-modules.md).</span><span class="sxs-lookup"><span data-stu-id="be2de-129">For more information, see [Writing Help for Windows PowerShell Modules](./writing-help-for-windows-powershell-modules.md).</span></span>

5. <span data-ttu-id="be2de-130">Se você tiver módulos adicionais, arquivos XML ou outro conteúdo que deseja empacotar com seu módulo, poderá fazer isso com um manifesto de módulo.</span><span class="sxs-lookup"><span data-stu-id="be2de-130">If you have additional modules, XML files, or other content you want to package up with your module, you can do so with a module manifest.</span></span>

   <span data-ttu-id="be2de-131">Um manifesto de módulo é um arquivo que contém os nomes de outros módulos, layouts de diretório, números de versão, dados de criação e outras partes de informações.</span><span class="sxs-lookup"><span data-stu-id="be2de-131">A module manifest is a file that contains the names of other modules, directory layouts, versioning numbers, author data, and other pieces of information.</span></span> <span data-ttu-id="be2de-132">O PowerShell usa o arquivo de manifesto de módulo para organizar e implantar sua solução.</span><span class="sxs-lookup"><span data-stu-id="be2de-132">PowerShell uses the module manifest file to organize and deploy your solution.</span></span> <span data-ttu-id="be2de-133">No entanto, devido à natureza relativamente simples deste exemplo, um arquivo de manifesto não era necessário.</span><span class="sxs-lookup"><span data-stu-id="be2de-133">However, due to the relatively simple nature of this example, a manifest file was not needed.</span></span> <span data-ttu-id="be2de-134">Para obter mais informações, consulte [manifestos de módulo](./how-to-write-a-powershell-module-manifest.md).</span><span class="sxs-lookup"><span data-stu-id="be2de-134">For more information, see [Module Manifests](./how-to-write-a-powershell-module-manifest.md).</span></span>

6. <span data-ttu-id="be2de-135">Para instalar e executar o módulo, salve o módulo em um dos caminhos apropriados do PowerShell e faça uma chamada para `Import-Module`.</span><span class="sxs-lookup"><span data-stu-id="be2de-135">To install and run your module, save the module to one of the appropriate PowerShell paths, and make a call to `Import-Module`.</span></span>

   <span data-ttu-id="be2de-136">Os caminhos em que você pode instalar o módulo estão localizados na variável global `$env:PSModulePath`.</span><span class="sxs-lookup"><span data-stu-id="be2de-136">The paths where you can install your module are located in the `$env:PSModulePath` global variable.</span></span> <span data-ttu-id="be2de-137">Por exemplo, um caminho comum para salvar um módulo em um sistema seria `%SystemRoot%/users/<user>/Documents/WindowsPowerShell/Modules/<moduleName>`.</span><span class="sxs-lookup"><span data-stu-id="be2de-137">For example, a common path to save a module on a system would be `%SystemRoot%/users/<user>/Documents/WindowsPowerShell/Modules/<moduleName>`.</span></span> <span data-ttu-id="be2de-138">Certifique-se de criar uma pasta para o módulo existir no, mesmo que seja apenas um único arquivo. psm1.</span><span class="sxs-lookup"><span data-stu-id="be2de-138">Be sure to create a folder for your module to exist in, even if it is only a single .psm1 file.</span></span> <span data-ttu-id="be2de-139">Se você não salvou o módulo em um desses caminhos, precisará passar o local do seu módulo na chamada para `Import-Module`.</span><span class="sxs-lookup"><span data-stu-id="be2de-139">If you did not save your module to one of these paths, you would have to pass in the location of your module in the call to `Import-Module`.</span></span> <span data-ttu-id="be2de-140">(Caso contrário, o PowerShell não conseguiria encontrá-lo.) A partir do PowerShell 3,0, se você colocou o módulo em um dos caminhos de módulo do PowerShell, não será necessário importá-lo explicitamente.</span><span class="sxs-lookup"><span data-stu-id="be2de-140">(Otherwise, PowerShell would not be able to find it.) Starting with PowerShell 3.0, if you have placed your module in one of the PowerShell module paths, you do not need to explicitly import it.</span></span> <span data-ttu-id="be2de-141">Seu módulo é carregado automaticamente quando um usuário chama sua função.</span><span class="sxs-lookup"><span data-stu-id="be2de-141">You module is automatically loaded when a user calls your function.</span></span>
   <span data-ttu-id="be2de-142">Para obter mais informações sobre o caminho do módulo, consulte [importando um módulo do PowerShell e uma variável de](./importing-a-powershell-module.md) [ambiente PSModulePath](./modifying-the-psmodulepath-installation-path.md).</span><span class="sxs-lookup"><span data-stu-id="be2de-142">For more information on the module path, see [Importing a PowerShell Module](./importing-a-powershell-module.md) and [PSModulePath Environment Variable](./modifying-the-psmodulepath-installation-path.md).</span></span>

7. <span data-ttu-id="be2de-143">Para remover um módulo do serviço ativo, faça uma chamada para [Remove-Module](/powershell/module/Microsoft.PowerShell.Core/Remove-Module).</span><span class="sxs-lookup"><span data-stu-id="be2de-143">To remove a module from active service, make a call to [Remove-Module](/powershell/module/Microsoft.PowerShell.Core/Remove-Module).</span></span>

   <span data-ttu-id="be2de-144">Observe que o [Remove-Module](/powershell/module/Microsoft.PowerShell.Core/Remove-Module) remove seu módulo da memória ativa-ele não o exclui de fato de onde você salvou os arquivos do módulo.</span><span class="sxs-lookup"><span data-stu-id="be2de-144">Note that [Remove-Module](/powershell/module/Microsoft.PowerShell.Core/Remove-Module) removes your module from active memory - it does not actually delete it from where you saved the module files.</span></span>

### <a name="show-calendar-code-example"></a><span data-ttu-id="be2de-145">Mostrar-exemplo de código do calendário</span><span class="sxs-lookup"><span data-stu-id="be2de-145">Show-Calendar code example</span></span>

<span data-ttu-id="be2de-146">O exemplo a seguir é um módulo de script simples que contém uma única função chamada `Show-Calendar`.</span><span class="sxs-lookup"><span data-stu-id="be2de-146">The following example is a simple script module that contains a single function named `Show-Calendar`.</span></span>
<span data-ttu-id="be2de-147">Essa função exibe uma representação visual de um calendário.</span><span class="sxs-lookup"><span data-stu-id="be2de-147">This function displays a visual representation of a calendar.</span></span> <span data-ttu-id="be2de-148">Além disso, o exemplo contém as cadeias de caracteres de ajuda do PowerShell para Sinopse, descrição, valores de parâmetro e exemplo.</span><span class="sxs-lookup"><span data-stu-id="be2de-148">In addition, the sample contains the PowerShell Help strings for the synopsis, description, parameter values, and example.</span></span> <span data-ttu-id="be2de-149">Observe que a última linha de código garante que a função `Show-Calendar` seja exportada como um membro de módulo quando o módulo for importado.</span><span class="sxs-lookup"><span data-stu-id="be2de-149">Note that the last line of code ensures that the `Show-Calendar` function is exported as a module member when the module is imported.</span></span>

```powershell
<#
 .Synopsis
  Displays a visual representation of a calendar.

 .Description
  Displays a visual representation of a calendar. This function supports multiple months
  and lets you highlight specific date ranges or days.

 .Parameter Start
  The first month to display.

 .Parameter End
  The last month to display.

 .Parameter FirstDayOfWeek
  The day of the month on which the week begins.

 .Parameter HighlightDay
  Specific days (numbered) to highlight. Used for date ranges like (25..31).
  Date ranges are specified by the Windows PowerShell range syntax. These dates are
  enclosed in square brackets.

 .Parameter HighlightDate
  Specific days (named) to highlight. These dates are surrounded by asterisks.

 .Example
   # Show a default display of this month.
   Show-Calendar

 .Example
   # Display a date range.
   Show-Calendar -Start "March, 2010" -End "May, 2010"

 .Example
   # Highlight a range of days.
   Show-Calendar -HighlightDay (1..10 + 22) -HighlightDate "December 25, 2008"
#>
function Show-Calendar {
param(
    [DateTime] $start = [DateTime]::Today,
    [DateTime] $end = $start,
    $firstDayOfWeek,
    [int[]] $highlightDay,
    [string[]] $highlightDate = [DateTime]::Today.ToString()
    )

## Determine the first day of the start and end months.
$start = New-Object DateTime $start.Year,$start.Month,1
$end = New-Object DateTime $end.Year,$end.Month,1

## Convert the highlighted dates into real dates.
[DateTime[]] $highlightDate = [DateTime[]] $highlightDate

## Retrieve the DateTimeFormat information so that the
## calendar can be manipulated.
$dateTimeFormat  = (Get-Culture).DateTimeFormat
if($firstDayOfWeek)
{
    $dateTimeFormat.FirstDayOfWeek = $firstDayOfWeek
}

$currentDay = $start

## Process the requested months.
while($start -le $end)
{
    ## Return to an earlier point in the function if the first day of the month
    ## is in the middle of the week.
    while($currentDay.DayOfWeek -ne $dateTimeFormat.FirstDayOfWeek)
    {
        $currentDay = $currentDay.AddDays(-1)
    }

    ## Prepare to store information about this date range.
    $currentWeek = New-Object PsObject
    $dayNames = @()
    $weeks = @()

    ## Continue processing dates until the function reaches the end of the month.
    ## The function continues until the week is completed with
    ## days from the next month.
    while(($currentDay -lt $start.AddMonths(1)) -or
        ($currentDay.DayOfWeek -ne $dateTimeFormat.FirstDayOfWeek))
    {
        ## Determine the day names to use to label the columns.
        $dayName = "{0:ddd}" -f $currentDay
        if($dayNames -notcontains $dayName)
        {
            $dayNames += $dayName
        }

        ## Pad the day number for display, highlighting if necessary.
        $displayDay = " {0,2} " -f $currentDay.Day

        ## Determine whether to highlight a specific date.
        if($highlightDate)
        {
            $compareDate = New-Object DateTime $currentDay.Year,
                $currentDay.Month,$currentDay.Day
            if($highlightDate -contains $compareDate)
            {
                $displayDay = "*" + ("{0,2}" -f $currentDay.Day) + "*"
            }
        }

        ## Otherwise, highlight as part of a date range.
        if($highlightDay -and ($highlightDay[0] -eq $currentDay.Day))
        {
            $displayDay = "[" + ("{0,2}" -f $currentDay.Day) + "]"
            $null,$highlightDay = $highlightDay
        }

        ## Add the day of the week and the day of the month as note properties.
        $currentWeek | Add-Member NoteProperty $dayName $displayDay

        ## Move to the next day of the month.
        $currentDay = $currentDay.AddDays(1)

        ## If the function reaches the next week, store the current week
        ## in the week list and continue.
        if($currentDay.DayOfWeek -eq $dateTimeFormat.FirstDayOfWeek)
        {
            $weeks += $currentWeek
            $currentWeek = New-Object PsObject
        }
    }

    ## Format the weeks as a table.
    $calendar = $weeks | Format-Table $dayNames -AutoSize | Out-String

    ## Add a centered header.
    $width = ($calendar.Split("`n") | Measure-Object -Maximum Length).Maximum
    $header = "{0:MMMM yyyy}" -f $start
    $padding = " " * (($width - $header.Length) / 2)
    $displayCalendar = " `n" + $padding + $header + "`n " + $calendar
    $displayCalendar.TrimEnd()

    ## Move to the next month.
    $start = $start.AddMonths(1)

}
}
Export-ModuleMember -Function Show-Calendar
```
