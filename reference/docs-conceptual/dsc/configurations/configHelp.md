---
ms.date: 12/12/2018
keywords: DSC,powershell,configuração,instalação
title: Escrever ajuda para configurações de DSC
ms.openlocfilehash: 498ec0f594ed3229e097903c4ea2ae34d3da03a2
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "71954133"
---
# <a name="writing-help-for-dsc-configurations"></a><span data-ttu-id="8b5c7-103">Escrever ajuda para configurações de DSC</span><span class="sxs-lookup"><span data-stu-id="8b5c7-103">Writing help for DSC configurations</span></span>

><span data-ttu-id="8b5c7-104">Aplica-se a: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="8b5c7-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="8b5c7-105">Você pode usar a ajuda baseada em comentários em configurações de DSC.</span><span class="sxs-lookup"><span data-stu-id="8b5c7-105">You can use comment-based help in DSC configurations.</span></span> <span data-ttu-id="8b5c7-106">Os usuários podem acessar a ajuda chamando a **Configuração** com `-?` ou usando o cmdlet [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help).</span><span class="sxs-lookup"><span data-stu-id="8b5c7-106">Users can access the help by calling the **Configuration** with `-?`, or by using the [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) cmdlet.</span></span> <span data-ttu-id="8b5c7-107">Coloque sua ajuda baseada em comentários diretamente acima da palavra-chave `Configuration`.</span><span class="sxs-lookup"><span data-stu-id="8b5c7-107">Place your Comment-based help directly above the `Configuration` keyword.</span></span>
<span data-ttu-id="8b5c7-108">Você pode colocar a ajuda do parâmetro alinhada ao seu bloco de comentários, diretamente acima da declaração do parâmetro, ou em ambos como no exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="8b5c7-108">You can place parameter help in-line with your comment block, directly above the parameter declaration, or both as in the example below.</span></span>

<span data-ttu-id="8b5c7-109">Para saber mais sobre a ajuda baseada em comentários do PowerShell, veja [about_Comment_Based_Help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help).</span><span class="sxs-lookup"><span data-stu-id="8b5c7-109">For more information about PowerShell comment-based help, see [about_Comment_Based_Help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help).</span></span>

> [!NOTE]
> <span data-ttu-id="8b5c7-110">Os ambientes de desenvolvimento do PowerShell, como VSCode, e o ISE também têm snippets que possibilitam inserir automaticamente modelos de bloco de comentários.</span><span class="sxs-lookup"><span data-stu-id="8b5c7-110">PowerShell development environments, like VSCode and the ISE, also have snippets to allow you to automatically insert comment block templates.</span></span>

<span data-ttu-id="8b5c7-111">O exemplo a seguir mostra um script que contém uma configuração e uma ajuda baseada em comentários para cada configuração.</span><span class="sxs-lookup"><span data-stu-id="8b5c7-111">The following example shows a script that contains a configuration and comment-based help for it.</span></span> <span data-ttu-id="8b5c7-112">Este exemplo mostra uma configuração com parâmetros.</span><span class="sxs-lookup"><span data-stu-id="8b5c7-112">This example shows a Configuration with parameters.</span></span> <span data-ttu-id="8b5c7-113">Para saber mais sobre como usar parâmetros em suas configurações, consulte [Adicionar parâmetros às suas configurações](add-parameters-to-a-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="8b5c7-113">To learn more about using parameters in your Configurations, see [Add Parameters to your Configurations](add-parameters-to-a-configuration.md).</span></span>

```powershell
<#
.SYNOPSIS
A brief description of the function or script. This keyword can be used only once for each configuration.


.DESCRIPTION
A detailed description of the function or script. This keyword can be used only once for each configuration.


.PARAMETER ComputerName
The description of a parameter. Add a .PARAMETER keyword for each parameter in the function or script syntax.

Type the parameter name on the same line as the .PARAMETER keyword. Type the parameter description on the lines following the .PARAMETER keyword.
Windows PowerShell interprets all text between the .PARAMETER line and the next keyword or the end of the comment block as part of the parameter description.
The description can include paragraph breaks.

The Parameter keywords can appear in any order in the comment block, but the function or script syntax determines the order in which the parameters
(and their descriptions) appear in help topic. To change the order, change the syntax.

.EXAMPLE
HelpSample -ComputerName localhost

A sample command that uses the function or script, optionally followed by sample output and a description. Repeat this keyword for each example.
PowerShell automatically prefaces the first line with a PowerShell prompt. Additional lines are treated as output and description. The example can contain spaces, newlines and PowerShell code.

If you have multiple examples, there is no need to number them. PowerShell will number the examples in help text.
.EXAMPLE
HelpSample -FilePath "C:\output.txt"

This example will be labeled "EXAMPLE 2" when help is displayed to the user.
#>
configuration HelpSample1
{
    param
    (
        [string]$ComputerName = 'localhost',
        # Provide a PARAMETER section for each parameter that your script or function accepts.
        [string]$FilePath = 'C:\Destination.txt'
    )

    Node $ComputerName
    {
        File HelloWorld
        {
            Contents="Hello World"
            DestinationPath = $FilePath
        }
    }
}
```

## <a name="viewing-configuration-help"></a><span data-ttu-id="8b5c7-114">Exibindo a ajuda de configuração</span><span class="sxs-lookup"><span data-stu-id="8b5c7-114">Viewing configuration help</span></span>

<span data-ttu-id="8b5c7-115">Para exibir a ajuda de uma configuração, use o cmdlet `Get-Help` com o nome da função, ou digite o nome da função seguido por `-?`.</span><span class="sxs-lookup"><span data-stu-id="8b5c7-115">To view the help for a configuration, use the `Get-Help` cmdlet with the name of the function, or type the name of the function followed by `-?`.</span></span> <span data-ttu-id="8b5c7-116">Veja a seguir o resultado da configuração anterior passada para `Get-Help`.</span><span class="sxs-lookup"><span data-stu-id="8b5c7-116">The following is the output of the previous Configuration passed to `Get-Help`.</span></span>

```powershell
Get-Help HelpSample1 -Detailed
```

```output
NAME
    HelpSample1

SYNOPSIS
    A brief description of the function or script. This keyword can be used only once for each configuration.


SYNTAX
    HelpSample1 [[-InstanceName] <String>] [[-DependsOn] <String[]>] [[-PsDscRunAsCredential] <PSCredential>] [[-OutputPath] <String>] [[-ConfigurationData] <Hashtable>] [[-ComputerName] <String>] [[-FilePath] <String>] [<CommonParameters>]


DESCRIPTION
    A detailed description of the function or script. This keyword can be used only once for each configuration.


PARAMETERS
    -InstanceName <String>

    -DependsOn <String[]>

    -PsDscRunAsCredential <PSCredential>

    -OutputPath <String>

    -ConfigurationData <Hashtable>

    -ComputerName <String>
        The description of a parameter. Add a .PARAMETER keyword for each parameter in the function or script syntax.

        Type the parameter name on the same line as the .PARAMETER keyword. Type the parameter description on the lines following the .PARAMETER keyword.
        Windows PowerShell interprets all text between the .PARAMETER line and the next keyword or the end of the comment block as part of the parameter description.
        The description can include paragraph breaks.

        The Parameter keywords can appear in any order in the comment block, but the function or script syntax determines the order in which the parameters
        (and their descriptions) appear in help topic. To change the order, change the syntax.

    -FilePath <String>
        Provide a PARAMETER section for each parameter that your script or function accepts.

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (https:/go.microsoft.com/fwlink/?LinkID=113216).

    -------------------------- EXAMPLE 1 --------------------------

    PS C:\>HelpSample -ComputerName localhost

    A sample command that uses the function or script, optionally followed by sample output and a description. Repeat this keyword for each example.
    PowerShell automatically prefaces the first line with a PowerShell prompt. Additional lines are treated as output and description. The example can contain spaces, newlines and PowerShell code.

    If you have multiple examples, there is no need to number them. PowerShell will number the examples in help text.




    -------------------------- EXAMPLE 2 --------------------------

    PS C:\>HelpSample -FilePath "C:\output.txt"

    This example will be labeled "EXAMPLE 2" when help is displayed to the user.




REMARKS
    To see the examples, type: "get-help HelpSample1 -examples".
    For more information, type: "get-help HelpSample1 -detailed".
    For technical information, type: "get-help HelpSample1 -full".
```

> [!NOTE]
> <span data-ttu-id="8b5c7-117">Os atributos de parâmetro e campos de sintaxe são gerados automaticamente pelo PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8b5c7-117">Syntax fields and parameter attributes are automatically generated for you by PowerShell.</span></span>

## <a name="see-also"></a><span data-ttu-id="8b5c7-118">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="8b5c7-118">See Also</span></span>

- [<span data-ttu-id="8b5c7-119">Configurações DSC</span><span class="sxs-lookup"><span data-stu-id="8b5c7-119">DSC Configurations</span></span>](configurations.md)
- [<span data-ttu-id="8b5c7-120">Gravar, compilar e aplicar uma configuração</span><span class="sxs-lookup"><span data-stu-id="8b5c7-120">Write, Compile, and Apply a Configuration</span></span>](write-compile-apply-configuration.md)
- [<span data-ttu-id="8b5c7-121">Adicionar parâmetros a uma configuração</span><span class="sxs-lookup"><span data-stu-id="8b5c7-121">Add Parameters to a Configuration</span></span>](add-parameters-to-a-configuration.md)
