---
ms.date: 12/12/2018
keywords: DSC,powershell,configuração,instalação
title: Instruções condicionais e loops em configurações
ms.openlocfilehash: 0073d94d28afbb45bb635442129a6cddde4c805a
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "71954073"
---
# <a name="conditional-statements-and-loops-in-configurations"></a><span data-ttu-id="8653a-103">Instruções condicionais e loops em configurações</span><span class="sxs-lookup"><span data-stu-id="8653a-103">Conditional statements and loops in Configurations</span></span>

<span data-ttu-id="8653a-104">Você pode tornar suas [Configurações](configurations.md) mais dinâmicas usando palavras-chave de controle de fluxo do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8653a-104">You can make your [Configurations](configurations.md) more dynamic using PowerShell flow-control keywords.</span></span> <span data-ttu-id="8653a-105">Este artigo mostra como você pode usar instruções condicionais e loops para tornar as Configurações mais dinâmicas.</span><span class="sxs-lookup"><span data-stu-id="8653a-105">This article will show you how you can use conditional statements, and loops to make your Configurations more dynamic.</span></span> <span data-ttu-id="8653a-106">Combinar condicionais e loops com [parâmetros](add-parameters-to-a-configuration.md) e [Dados de Configuração](configData.md) proporciona a você mais flexibilidade e controle ao compilar as Configurações.</span><span class="sxs-lookup"><span data-stu-id="8653a-106">Combining conditional and loops with [parameters](add-parameters-to-a-configuration.md) and [Configuration Data](configData.md) allows you more flexibility and control when compiling your Configurations.</span></span>

<span data-ttu-id="8653a-107">Assim com uma Função ou um Bloco de Script, é possível usar qualquer linguagem do PowerShell em uma Configuração.</span><span class="sxs-lookup"><span data-stu-id="8653a-107">Just like a Function or a Script Block, you can use any PowerShell language within a Configuration.</span></span> <span data-ttu-id="8653a-108">As instruções usadas serão avaliadas somente quando você chamar a Configuração para compilar um arquivo ".mof".</span><span class="sxs-lookup"><span data-stu-id="8653a-108">The statements you use will only be evaluated when you call your Configuration to compile a ".mof" file.</span></span> <span data-ttu-id="8653a-109">Os exemplos abaixo mostram cenários simples para demonstrar conceitos.</span><span class="sxs-lookup"><span data-stu-id="8653a-109">The examples below show simple scenarios to demonstrate concepts.</span></span> <span data-ttu-id="8653a-110">As condicionais são loops usados frequentemente com parâmetros e Dados de Configuração.</span><span class="sxs-lookup"><span data-stu-id="8653a-110">Conditionals are loops are more often used with parameters and Configuration Data.</span></span>

<span data-ttu-id="8653a-111">Neste exemplo simples, o bloco de recurso **Service** recupera o estado atual de um serviço no tempo de compilação para gerar um arquivo ".mof" que mantém seu estado atual.</span><span class="sxs-lookup"><span data-stu-id="8653a-111">In this simple example, the **Service** resource block retrieves the current state of a service at compile time to generate a ".mof" file that maintains its current state.</span></span>

> [!NOTE]
> <span data-ttu-id="8653a-112">Usar blocos de recurso dinâmicos inviabiliza a eficácia do Intellisense.</span><span class="sxs-lookup"><span data-stu-id="8653a-112">Using dynamic Resource blocks will preempt the effectiveness of Intellisense.</span></span> <span data-ttu-id="8653a-113">O analisador do PowerShell não pode determinar se os valores especificados são aceitáveis enquanto a Configuração não for compilada.</span><span class="sxs-lookup"><span data-stu-id="8653a-113">The PowerShell parser cannot determine if the values specified are acceptable until the Configuration is compiled.</span></span>

```powershell
Configuration ServiceState
{
    # It is best practice to explicitly import any resources used in your Configurations.
    Import-DSCResource -Name Service -Module PSDesiredStateConfiguration
    Node localhost
    {
        Service Spooler
        {
            Name = "Spooler"
            State = $(Get-Service -Name 'spooler').Status
            StartType = $(Get-Service -Name 'spooler').StartType
        }
    }
}
```

<span data-ttu-id="8653a-114">Além disso, você pode criar um bloco de recurso **Service** para cada serviço no computador atual usando um loop `foreach`.</span><span class="sxs-lookup"><span data-stu-id="8653a-114">Additionally, you could create a **Service** block resource for every service on the current machine, using a `foreach` loop.</span></span>

```powershell
Configuration ServiceState
{
    # It is best practice to explicitly import any resources used in your Configurations.
    Import-DSCResource -Name Service -Module PSDesiredStateConfiguration
    Node localhost
    {
        Foreach ($service in $(Get-Service))
        {
            Service $service.Name
            {
                Name = $service.Name
                State = $service.Status
                StartType = $service.StartType
            }
        }
    }
}
```

<span data-ttu-id="8653a-115">Também é possível criar configurações somente para computadores que estão online, usando uma instrução `if` simples.</span><span class="sxs-lookup"><span data-stu-id="8653a-115">You could also only create configurations for machines that are online, by using a simple `if` statement.</span></span>

```powershell
Configuration ServiceState
{
    # It is best practice to explicitly import any resources used in your Configurations.
    Import-DSCResource -Name Service -Module PSDesiredStateConfiguration

    Foreach ($computer in @('Server01', 'Server02', 'Server03'))
    {
        if (Test-Connection -ComputerName $computer)
        {
            Node $computer
            {
                Service "Spooler"
                {
                    Name = "Spooler"
                    State = "Started"
                }
            }
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="8653a-116">Os blocos de recurso dinâmicos nos exemplos acima fazem referência ao computador atual.</span><span class="sxs-lookup"><span data-stu-id="8653a-116">The dynamic resource blocks in the above examples reference the current machine.</span></span> <span data-ttu-id="8653a-117">Nesse caso, esse seria o computador no qual você cria a Configuração, não o Nó de destino.</span><span class="sxs-lookup"><span data-stu-id="8653a-117">In this instance, that would be the machine you are authoring the Configuration on, not the target Node.</span></span>

<!---
Mention Get-DSCConfigurationFromSystem
-->

## <a name="summary"></a><span data-ttu-id="8653a-118">Resumo</span><span class="sxs-lookup"><span data-stu-id="8653a-118">Summary</span></span>

<span data-ttu-id="8653a-119">Resumindo, você pode usar qualquer linguagem do PowerShell em uma Configuração.</span><span class="sxs-lookup"><span data-stu-id="8653a-119">In summary, you can use any PowerShell language within a Configuration.</span></span>

<span data-ttu-id="8653a-120">Isso inclui itens como:</span><span class="sxs-lookup"><span data-stu-id="8653a-120">This includes things like:</span></span>

- <span data-ttu-id="8653a-121">Objetos personalizados</span><span class="sxs-lookup"><span data-stu-id="8653a-121">Custom Objects</span></span>
- <span data-ttu-id="8653a-122">Tabelas de hash</span><span class="sxs-lookup"><span data-stu-id="8653a-122">Hashtables</span></span>
- <span data-ttu-id="8653a-123">Manipulação da cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="8653a-123">String manipulation</span></span>
- <span data-ttu-id="8653a-124">Comunicação remota</span><span class="sxs-lookup"><span data-stu-id="8653a-124">Remoting</span></span>
- <span data-ttu-id="8653a-125">WMI e CIM</span><span class="sxs-lookup"><span data-stu-id="8653a-125">WMI and CIM</span></span>
- <span data-ttu-id="8653a-126">Objetos do ActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="8653a-126">ActiveDirectory objects</span></span>
- <span data-ttu-id="8653a-127">e mais...</span><span class="sxs-lookup"><span data-stu-id="8653a-127">and more...</span></span>

<span data-ttu-id="8653a-128">Qualquer código do PowerShell definido em uma Configuração será avaliado no tempo de compilação, mas você também pode colocar o código no script que contém sua Configuração.</span><span class="sxs-lookup"><span data-stu-id="8653a-128">Any PowerShell code defined in a Configuration will be evaluated a compile time, but you can also place code in the script containing your Configuration.</span></span> <span data-ttu-id="8653a-129">Qualquer código fora do bloco de Configuração será executado ao importar sua Configuração.</span><span class="sxs-lookup"><span data-stu-id="8653a-129">Any code outside of the Configuration block will be executed when you import your Configuration.</span></span>

## <a name="see-also"></a><span data-ttu-id="8653a-130">Consulte também</span><span class="sxs-lookup"><span data-stu-id="8653a-130">See also</span></span>

- [<span data-ttu-id="8653a-131">Adicionar parâmetros a uma configuração</span><span class="sxs-lookup"><span data-stu-id="8653a-131">Add parameters to a Configuration</span></span>](add-parameters-to-a-configuration.md)
- [<span data-ttu-id="8653a-132">Separar dados de configuração das Configurações</span><span class="sxs-lookup"><span data-stu-id="8653a-132">Separate Configuration data from Configurations</span></span>](configData.md)
