---
ms.date: 06/05/2017
keywords: powershell, cmdlet
title: Exibindo a estrutura do objeto Get Member
ms.openlocfilehash: 80b36abd303a708195f12d96511e616178d11b5a
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2020
ms.locfileid: "67030709"
---
# <a name="viewing-object-structure-get-member"></a><span data-ttu-id="28591-103">Exibindo a estrutura do objeto (Get-Member)</span><span class="sxs-lookup"><span data-stu-id="28591-103">Viewing Object Structure (Get-Member)</span></span>

<span data-ttu-id="28591-104">Como objetos representam um papel central no Windows PowerShell, há vários comandos nativos projetados para trabalhar com tipos de objetos arbitrários.</span><span class="sxs-lookup"><span data-stu-id="28591-104">Because objects play such a central role in Windows PowerShell, there are several native commands designed to work with arbitrary object types.</span></span> <span data-ttu-id="28591-105">O mais importante é o comando **Get-Member**.</span><span class="sxs-lookup"><span data-stu-id="28591-105">The most important one is the **Get-Member** command.</span></span>

<span data-ttu-id="28591-106">A técnica mais simples para analisar os objetos que um comando retorna é direcionar a saída desse comando para o cmdlet **Get-Member**.</span><span class="sxs-lookup"><span data-stu-id="28591-106">The simplest technique for analyzing the objects that a command returns is to pipe the output of that command to the **Get-Member** cmdlet.</span></span> <span data-ttu-id="28591-107">O cmdlet **Get-Member** mostra o nome formal do tipo de objeto e uma lista completa de seus membros.</span><span class="sxs-lookup"><span data-stu-id="28591-107">The **Get-Member** cmdlet shows you the formal name of the object type and a complete listing of its members.</span></span> <span data-ttu-id="28591-108">O número de elementos que são retornados, às vezes, pode ser imenso.</span><span class="sxs-lookup"><span data-stu-id="28591-108">The number of elements that are returned can sometimes be overwhelming.</span></span> <span data-ttu-id="28591-109">Por exemplo, um objeto de processo pode ter mais de 100 membros.</span><span class="sxs-lookup"><span data-stu-id="28591-109">For example, a process object can have over 100 members.</span></span>

<span data-ttu-id="28591-110">Para ver todos os membros de um objeto e Process e paginar a saída para que você possa exibir tudo, digite:</span><span class="sxs-lookup"><span data-stu-id="28591-110">To see all the members of a Process object and page the output so you can view all of it, type:</span></span>

```powershell
Get-Process | Get-Member | Out-Host -Paging
```

<span data-ttu-id="28591-111">A saída deste comando será parecida com isto:</span><span class="sxs-lookup"><span data-stu-id="28591-111">The output from this command will look something like this:</span></span>

```output
TypeName: System.Diagnostics.Process

Name                           MemberType     Definition
----                           ----------     ----------
Handles                        AliasProperty  Handles = Handlecount
Name                           AliasProperty  Name = ProcessName
NPM                            AliasProperty  NPM = NonpagedSystemMemorySize
PM                             AliasProperty  PM = PagedMemorySize
VM                             AliasProperty  VM = VirtualMemorySize
WS                             AliasProperty  WS = WorkingSet
add_Disposed                   Method         System.Void add_Disposed(Event...
...
```

<span data-ttu-id="28591-112">Podemos tornar essa longa lista de informações mais utilizável com filtragem dos elementos que você deseja ver.</span><span class="sxs-lookup"><span data-stu-id="28591-112">We can make this long list of information more usable by filtering for elements we want to see.</span></span> <span data-ttu-id="28591-113">O comando **Get-Member** permite listar somente os membros que são propriedades.</span><span class="sxs-lookup"><span data-stu-id="28591-113">The **Get-Member** command lets you list only members that are properties.</span></span> <span data-ttu-id="28591-114">Há várias formas de propriedades.</span><span class="sxs-lookup"><span data-stu-id="28591-114">There are several forms of properties.</span></span> <span data-ttu-id="28591-115">O cmdlet exibirá as propriedades de qualquer tipo se definirmos o **Get-Member MemberType** parâmetro para o valor **Properties**.</span><span class="sxs-lookup"><span data-stu-id="28591-115">The cmdlet displays properties of any type if we set the **Get-Member MemberType** parameter to the value **Properties**.</span></span> <span data-ttu-id="28591-116">A lista resultante ainda é muito longa, mas um pouco mais fácil de gerenciar:</span><span class="sxs-lookup"><span data-stu-id="28591-116">The resulting list is still very long, but a bit more manageable:</span></span>

```
PS> Get-Process | Get-Member -MemberType Properties

   TypeName: System.Diagnostics.Process

Name                       MemberType     Definition
----                       ----------     ----------
Handles                    AliasProperty  Handles = Handlecount
Name                       AliasProperty  Name = ProcessName
...
ExitCode                   Property       System.Int32 ExitCode {get;}
...
Handle                     Property       System.IntPtr Handle {get;}
...
CPU                        ScriptProperty System.Object CPU {get=$this.Total...
...
Path                       ScriptProperty System.Object Path {get=$this.Main...
...
```

> [!NOTE]
> <span data-ttu-id="28591-117">Os valores permitidos para MemberType são AliasProperty, CodeProperty, Property, NoteProperty, ScriptProperty, Properties, PropertySet, Method, CodeMethod, ScriptMethod, Methods, ParameterizedProperty, MemberSet e All.</span><span class="sxs-lookup"><span data-stu-id="28591-117">The allowed values of MemberType are AliasProperty, CodeProperty, Property, NoteProperty, ScriptProperty, Properties, PropertySet, Method, CodeMethod, ScriptMethod, Methods, ParameterizedProperty, MemberSet, and All.</span></span>

<span data-ttu-id="28591-118">Há mais de 60 propriedades para um processo.</span><span class="sxs-lookup"><span data-stu-id="28591-118">There are over 60 properties for a process.</span></span> <span data-ttu-id="28591-119">O motivo que faz o Windows PowerShell geralmente mostrar apenas algumas propriedades para qualquer objeto conhecido é que mostrar todas elas produziria uma quantidade incontrolável de informações.</span><span class="sxs-lookup"><span data-stu-id="28591-119">The reason Windows PowerShell often shows only a handful of properties for any well-known object is that showing all of them would produce an unmanageable amount of information.</span></span>

> [!NOTE]
> <span data-ttu-id="28591-120">O Windows PowerShell determina como exibir um tipo de objeto usando informações armazenadas em arquivos XML que têm nomes que terminam com .format.ps1xml.</span><span class="sxs-lookup"><span data-stu-id="28591-120">Windows PowerShell determines how to display an object type by using information stored in XML files that have names ending in .format.ps1xml.</span></span> <span data-ttu-id="28591-121">Os dados de formatação para objetos de processo, que são objetos System.Diagnostics.Process do .NET, são armazenados em DotNetTypes.format.ps1xml.</span><span class="sxs-lookup"><span data-stu-id="28591-121">The formatting data for process objects, which are .NET System.Diagnostics.Process objects, is stored in DotNetTypes.format.ps1xml.</span></span>

<span data-ttu-id="28591-122">Se você precisar examinar propriedades diferentes que o Windows PowerShell exibe por padrão, deverá formatar os dados de saída por conta própria.</span><span class="sxs-lookup"><span data-stu-id="28591-122">If you need to look at properties other than those that Windows PowerShell displays by default, you will need to format the output data yourself.</span></span> <span data-ttu-id="28591-123">Isso pode ser feito usando os cmdlets de formato.</span><span class="sxs-lookup"><span data-stu-id="28591-123">This can be done by using the format cmdlets.</span></span>
