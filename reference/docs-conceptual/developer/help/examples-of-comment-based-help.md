---
title: Exemplos de ajuda baseada em comentários | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 868194a2-17e9-4184-bc36-c04a33f26494
caps.latest.revision: 4
ms.openlocfilehash: 30e98bfcf06b1720005a73ee8294aeba7e1ae066
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72367815"
---
# <a name="examples-of-comment-based-help"></a><span data-ttu-id="e2374-102">Exemplos de ajuda baseada em comentários</span><span class="sxs-lookup"><span data-stu-id="e2374-102">Examples of Comment-Based Help</span></span>

<span data-ttu-id="e2374-103">Este tópico inclui um exemplo que demonstra como usar a ajuda baseada em comentários para scripts e funções.</span><span class="sxs-lookup"><span data-stu-id="e2374-103">This topic includes example that demonstrate how to use comment-based help for scripts and functions.</span></span>

## <a name="example-1-comment-based-help-for-a-function"></a><span data-ttu-id="e2374-104">Exemplo 1: Ajuda baseada em comentários para uma função</span><span class="sxs-lookup"><span data-stu-id="e2374-104">Example 1: Comment-Based Help for a Function</span></span>

 <span data-ttu-id="e2374-105">A função de exemplo a seguir inclui ajuda baseada em comentários.</span><span class="sxs-lookup"><span data-stu-id="e2374-105">The following sample function includes comment-based Help.</span></span>

```powershell
function Add-Extension
{
    param ([string]$Name,[string]$Extension = "txt")
    $name = $name + "." + $extension
    $name

    <#
        .SYNOPSIS
        Adds a file name extension to a supplied name.

        .DESCRIPTION
        Adds a file name extension to a supplied name.
        Takes any strings for the file name or extension.

        .PARAMETER Name
        Specifies the file name.

        .PARAMETER Extension
        Specifies the extension. "Txt" is the default.

        .INPUTS
        None. You cannot pipe objects to Add-Extension.

        .OUTPUTS
        System.String. Add-Extension returns a string with the extension or file name.

        .EXAMPLE
        C:\PS> extension -name "File"
        File.txt

        .EXAMPLE
        C:\PS> extension -name "File" -extension "doc"
        File.doc

        .EXAMPLE
        C:\PS> extension "File" "doc"
        File.doc

        .LINK
        Online version: http://www.fabrikam.com/extension.html

        .LINK
        Set-Item
    #>
}
```

<span data-ttu-id="e2374-106">A saída a seguir mostra os resultados de um comando Get-Help que exibe a ajuda para a função de adição de extensão.</span><span class="sxs-lookup"><span data-stu-id="e2374-106">The following output shows the results of a Get-Help command that displays the help for the Add-Extension function.</span></span>

```powershell
C:\PS> get-help add-extension -full
```

```output
        NAME
            Add-Extension

        SYNOPSIS
            Adds a file name extension to a supplied name.

        SYNTAX
            Add-Extension [[-Name] <String>] [[-Extension] <String>] [<CommonParameters>]

        DESCRIPTION
            Adds a file name extension to a supplied name. Takes any strings for the file name or extension.

        PARAMETERS
           -Name
               Specifies the file name.

               Required?                    false
               Position?                    0
               Default value
               Accept pipeline input?       false
               Accept wildcard characters?

           -Extension
               Specifies the extension. "Txt" is the default.

               Required?                    false
               Position?                    1
               Default value
               Accept pipeline input?       false
               Accept wildcard characters?

            <CommonParameters>
               This cmdlet supports the common parameters: -Verbose, -Debug,
               -ErrorAction, -ErrorVariable, -WarningAction, -WarningVariable,
               -OutBuffer and -OutVariable. For more information, type
               "get-help about_commonparameters".

        INPUTS
            None. You cannot pipe objects to Add-Extension.

        OUTPUTS
            System.String. Add-Extension returns a string with the extension or file name.

            -------------------------- EXAMPLE 1 --------------------------

            C:\PS> extension -name "File"
            File.txt

            -------------------------- EXAMPLE 2 --------------------------

            C:\PS> extension -name "File" -extension "doc"
            File.doc

            -------------------------- EXAMPLE 3 --------------------------

            C:\PS> extension "File" "doc"
            File.doc

        RELATED LINKS
            Online version: http://www.fabrikam.com/extension.html
            Set-Item
```

## <a name="example-2-comment-based-help-for-a-script"></a><span data-ttu-id="e2374-107">Exemplo 2: Ajuda baseada em comentários para um script</span><span class="sxs-lookup"><span data-stu-id="e2374-107">Example 2: Comment-Based Help for a Script</span></span>

<span data-ttu-id="e2374-108">A função de exemplo a seguir inclui ajuda baseada em comentários.</span><span class="sxs-lookup"><span data-stu-id="e2374-108">The following sample function includes comment-based Help.</span></span>

<span data-ttu-id="e2374-109">Observe as linhas em branco entre o **#>** de fechamento e a instrução `Param`.</span><span class="sxs-lookup"><span data-stu-id="e2374-109">Notice the blank lines between the closing **#>** and the `Param` statement.</span></span> <span data-ttu-id="e2374-110">Em um script que não tem uma instrução `Param`, deve haver pelo menos duas linhas em branco entre o comentário final no tópico da ajuda e a primeira declaração da função.</span><span class="sxs-lookup"><span data-stu-id="e2374-110">In a script that does not have a `Param` statement, there must be at least two blank lines between the final comment in the Help topic and the first function declaration.</span></span> <span data-ttu-id="e2374-111">Sem essas linhas em branco, Get-Help associa o tópico da ajuda com a função, em vez do script.</span><span class="sxs-lookup"><span data-stu-id="e2374-111">Without these blank lines, Get-Help associates the Help topic with the function, instead of the script.</span></span>

```powershell
<#
  .SYNOPSIS
  Performs monthly data updates.

  .DESCRIPTION
  The Update-Month.ps1 script updates the registry with new data generated
  during the past month and generates a report.

  .PARAMETER InputPath
  Specifies the path to the CSV-based input file.

  .PARAMETER OutputPath
  Specifies the name and path for the CSV-based output file. By default,
  MonthlyUpdates.ps1 generates a name from the date and time it runs, and
  saves the output in the local directory.

  .INPUTS
  None. You cannot pipe objects to Update-Month.ps1.

  .OUTPUTS
  None. Update-Month.ps1 does not generate any output.

  .EXAMPLE
  C:\PS> .\Update-Month.ps1

  .EXAMPLE
  C:\PS> .\Update-Month.ps1 -inputpath C:\Data\January.csv

  .EXAMPLE
  C:\PS> .\Update-Month.ps1 -inputpath C:\Data\January.csv -outputPath C:\Reports\2009\January.csv
#>

param ([string]$InputPath, [string]$OutPutPath)

function Get-Data { }
```

<span data-ttu-id="e2374-112">O comando a seguir obtém a ajuda do script.</span><span class="sxs-lookup"><span data-stu-id="e2374-112">The following command gets the script Help.</span></span> <span data-ttu-id="e2374-113">Como o script não é um diretório listado na variável de ambiente Path, o comando Get-Help que obtém a ajuda do script deve especificar o caminho do script.</span><span class="sxs-lookup"><span data-stu-id="e2374-113">Because the script is not n a directory that is listed in the Path environment variable, the Get-Help command that gets the script Help must specify the script path.</span></span>

```powershell
C:\PS> get-help c:\ps-test\update-month.ps1 -full
```

```output
            NAME
                C:\ps-test\Update-Month.ps1

            SYNOPSIS
                Performs monthly data updates.

            SYNTAX
                C:\ps-test\Update-Month.ps1 [-InputPath] <String> [[-OutputPath]
                <String>] [<CommonParameters>]

            DESCRIPTION
                The Update-Month.ps1 script updates the registry with new data
                generated during the past month and generates a report.

            PARAMETERS
               -InputPath
                   Specifies the path to the CSV-based input file.

                   Required?                    true
                   Position?                    0
                   Default value
                   Accept pipeline input?       false
                   Accept wildcard characters?

               -OutputPath
                   Specifies the name and path for the CSV-based output file. By
                   default, MonthlyUpdates.ps1 generates a name from the date
                   and time it runs, and saves the output in the local directory.

                   Required?                    false
                   Position?                    1
                   Default value
                   Accept pipeline input?       false
                   Accept wildcard characters?

               <CommonParameters>
                   This cmdlet supports the common parameters: -Verbose, -Debug,
                   -ErrorAction, -ErrorVariable, -WarningAction, -WarningVariable,
                   -OutBuffer and -OutVariable. For more information, type,
                   "get-help about_commonparameters".

            INPUTS
                   None. You cannot pipe objects to Update-Month.ps1.

            OUTPUTS
                   None. Update-Month.ps1 does not generate any output.

            -------------------------- EXAMPLE 1 --------------------------

            C:\PS> .\Update-Month.ps1

            -------------------------- EXAMPLE 2 --------------------------

            C:\PS> .\Update-Month.ps1 -inputpath C:\Data\January.csv

            -------------------------- EXAMPLE 3 --------------------------

            C:\PS> .\Update-Month.ps1 -inputpath C:\Data\January.csv -outputPath
            C:\Reports\2009\January.csv

            RELATED LINKS
```

## <a name="example-3-parameter-descriptions-in-a-param-statement"></a><span data-ttu-id="e2374-114">Exemplo 3: descrições de parâmetro em uma instrução param</span><span class="sxs-lookup"><span data-stu-id="e2374-114">Example 3: Parameter Descriptions in a Param Statement</span></span>

<span data-ttu-id="e2374-115">Este exemplo mostra como inserir ParameterDescriptions na instrução `Param` de uma função ou script.</span><span class="sxs-lookup"><span data-stu-id="e2374-115">This example show how to insert parameterdescriptions in the `Param` statement of a function or script.</span></span> <span data-ttu-id="e2374-116">Esse formato é mais útil quando as descrições de parâmetro são breves.</span><span class="sxs-lookup"><span data-stu-id="e2374-116">This format is most useful when the parameter descriptions are brief.</span></span>

```powershell
function Add-Extension
{
    param
    (
        [string]
        # Specifies the file name.
        $name,

        [string]
        # Specifies the file name extension. "Txt" is the default.
        $extension = "txt"
    )
    $name = $name + "." + $extension
    $name

    <#
        .SYNOPSIS
        Adds a file name extension to a supplied name.
...
    #>
```

<span data-ttu-id="e2374-117">Os resultados são os mesmos dos resultados, por exemplo 1.</span><span class="sxs-lookup"><span data-stu-id="e2374-117">The results are the same as the results for Example 1.</span></span> <span data-ttu-id="e2374-118">O Get-Help interpreta as descrições de parâmetro como se elas estivessem acompanhadas pela palavra-chave `.Parameter`.</span><span class="sxs-lookup"><span data-stu-id="e2374-118">Get-Help interprets the parameter descriptions as though they were accompanied by the `.Parameter` keyword.</span></span>

## <a name="example-4--redirecting-to-an-xml-file"></a><span data-ttu-id="e2374-119">Exemplo 4: redirecionando para um arquivo XML</span><span class="sxs-lookup"><span data-stu-id="e2374-119">Example 4:  Redirecting to an XML File</span></span>

<span data-ttu-id="e2374-120">Você pode escrever tópicos de ajuda baseados em XML para funções e scripts.</span><span class="sxs-lookup"><span data-stu-id="e2374-120">You can write XML-based Help topics for functions and scripts.</span></span> <span data-ttu-id="e2374-121">Embora a ajuda baseada em comentários seja mais fácil de implementar, a ajuda baseada em XML é necessária se você quiser um controle mais preciso sobre o conteúdo da ajuda ou se estiver traduzindo tópicos da ajuda em vários idiomas. O exemplo a seguir mostra as primeiras linhas do script Update-Month. ps1.</span><span class="sxs-lookup"><span data-stu-id="e2374-121">Although comment-based Help is easier to implement, XML-based Help is required if you want more precise control over Help content or if you are translating Help topics into multiple languages.The following example shows the first few lines of the Update-Month.ps1 script.</span></span> <span data-ttu-id="e2374-122">O script usa a palavra-chave `.ExternalHelp` para especificar o caminho para um tópico de ajuda baseado em XML para o script.</span><span class="sxs-lookup"><span data-stu-id="e2374-122">The script uses the `.ExternalHelp` keyword to specify the path to an XML-based Help topic for the script.</span></span>

```powershell
#  .ExternalHelp C:\MyScripts\Update-Month-Help.xml

    param ([string]$InputPath, [string]$OutPutPath)

    function Get-Data { }
```

<span data-ttu-id="e2374-123">O exemplo a seguir mostra o uso da palavra-chave `.ExternalHelp` em uma função.</span><span class="sxs-lookup"><span data-stu-id="e2374-123">The following example shows the use of the `.ExternalHelp` keyword in a function.</span></span>

```powershell
function Add-Extension
{
    param ([string] $name, [string]$extension = "txt")
    $name = $name + "." + $extension
    $name

    # .ExternalHelp C:\ps-test\Add-Extension.xml
}
```

## <a name="example-5--redirecting-to-a-different-help-topic"></a><span data-ttu-id="e2374-124">Exemplo 5: redirecionando para um tópico de ajuda diferente</span><span class="sxs-lookup"><span data-stu-id="e2374-124">Example 5:  Redirecting to a Different Help Topic</span></span>

<span data-ttu-id="e2374-125">O código a seguir é um trecho do início da função interna `Help` no Windows PowerShell, que exibe uma tela de texto de ajuda por vez.</span><span class="sxs-lookup"><span data-stu-id="e2374-125">The following code is an excerpt from the beginning of the built-in `Help` function in Windows PowerShell, which displays one screen of Help text at a time.</span></span> <span data-ttu-id="e2374-126">Como o tópico da ajuda para o cmdlet Get-Help descreve a função Help, a função Help usa as palavras-chave `.ForwardHelpTargetName` e `.ForwardHelpCategory` para redirecionar o usuário para o tópico de ajuda do cmdlet Get-Help.</span><span class="sxs-lookup"><span data-stu-id="e2374-126">Because the Help topic for the Get-Help cmdlet describes the Help function, the Help function uses the `.ForwardHelpTargetName` and `.ForwardHelpCategory` keywords to redirect the user to the Get-Help cmdlet Help topic.</span></span>

```powershell
function help
{

    <#
      .FORWARDHELPTARGETNAME Get-Help
      .FORWARDHELPCATEGORY Cmdlet
    #>
    [CmdletBinding(DefaultParameterSetName='AllUsersView')]
    param(
            [Parameter(Position=0, ValueFromPipelineByPropertyName=$true)]
            [System.String]
            ${Name},
    ...
```

<span data-ttu-id="e2374-127">O comando a seguir usa esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e2374-127">The following command uses this feature.</span></span> <span data-ttu-id="e2374-128">Quando um usuário digita um comando Get-Help para a função Help, get-help exibe o tópico da ajuda para o cmdlet Get-Help.</span><span class="sxs-lookup"><span data-stu-id="e2374-128">When a user types a Get-Help command for the Help function, Get-Help displays the Help topic for the Get-Help cmdlet.</span></span>

```powershell
C:\PS> get-help help
```

```output
            NAME
                Get-Help

            SYNOPSIS
                Displays information about Windows PowerShell cmdlets and concepts.
            ...
```