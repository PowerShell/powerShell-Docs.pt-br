---
title: Como solicitar confirmações | Microsoft Docs
ms.date: 09/13/2016
ms.openlocfilehash: ebe928724f1b750afc11c1e3c1207375f4ec8e42
ms.sourcegitcommit: 0907b8c6322d2c7c61b17f8168d53452c8964b41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/05/2020
ms.locfileid: "87784088"
---
# <a name="how-to-request-confirmations"></a><span data-ttu-id="a4117-102">Como solicitar confirmações</span><span class="sxs-lookup"><span data-stu-id="a4117-102">How to Request Confirmations</span></span>

<span data-ttu-id="a4117-103">Este exemplo mostra como chamar os métodos [System. Management. Automation. cmdlet. ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) e [System. Management. Automation. cmdlet. ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) para solicitar confirmações do usuário antes que uma ação seja executada.</span><span class="sxs-lookup"><span data-stu-id="a4117-103">This example shows how to call the [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) and [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) methods to request confirmations from the user before an action is taken.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4117-104">Para obter mais informações sobre como o Windows PowerShell lida com essas solicitações, consulte [solicitando confirmação](./requesting-confirmation-from-cmdlets.md).</span><span class="sxs-lookup"><span data-stu-id="a4117-104">For more information about how Windows PowerShell handles these requests, see [Requesting Confirmation](./requesting-confirmation-from-cmdlets.md).</span></span>

## <a name="to-request-confirmation"></a><span data-ttu-id="a4117-105">Para solicitar confirmação</span><span class="sxs-lookup"><span data-stu-id="a4117-105">To request confirmation</span></span>

1. <span data-ttu-id="a4117-106">Verifique se o `SupportsShouldProcess` parâmetro do atributo cmdlet está definido como `true` .</span><span class="sxs-lookup"><span data-stu-id="a4117-106">Ensure that the `SupportsShouldProcess` parameter of the Cmdlet attribute is set to `true`.</span></span> <span data-ttu-id="a4117-107">(Para funções, esse é um parâmetro do atributo CmdletBinding.)</span><span class="sxs-lookup"><span data-stu-id="a4117-107">(For functions this is a parameter of the CmdletBinding attribute.)</span></span>

    ```csharp
    [Cmdlet(VerbsDiagnostic.Test, "RequestConfirmationTemplate1",
            SupportsShouldProcess = true)]
    ```

2. <span data-ttu-id="a4117-108">Adicione um `Force` parâmetro ao cmdlet para que o usuário possa substituir uma solicitação de confirmação.</span><span class="sxs-lookup"><span data-stu-id="a4117-108">Add a `Force` parameter to your cmdlet so that the user can override a confirmation request.</span></span>

    ```csharp
    [Parameter()]
    public SwitchParameter Force
    {
      get { return force; }
      set { force = value; }
    }
    private bool force;
    ```

3. <span data-ttu-id="a4117-109">Adicione uma `if` instrução que usa o valor de retorno do método [System. Management. Automation. cmdlet. ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) para determinar se o método [System. Management. Automation. cmdlet. ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) é chamado.</span><span class="sxs-lookup"><span data-stu-id="a4117-109">Add an `if` statement that uses the return value of the [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) method to determine if the [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) method is called.</span></span>

4. <span data-ttu-id="a4117-110">Adicione uma segunda `if` instrução que usa o valor de retorno do método [System. Management. Automation. cmdlet. ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) e o valor do `Force` parâmetro para determinar se a operação deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="a4117-110">Add a second `if` statement that uses the return value of the [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) method and the value of the `Force` parameter to determine whether the operation should be performed.</span></span>

## <a name="example"></a><span data-ttu-id="a4117-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a4117-111">Example</span></span>

<span data-ttu-id="a4117-112">No exemplo de código a seguir, os métodos [System. Management. Automation. cmdlet. ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) e [System. Management. Automation. cmdlet. ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) são chamados de dentro da substituição do método [System. Management. Automation. cmdlet. ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) .</span><span class="sxs-lookup"><span data-stu-id="a4117-112">In the following code example, the [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) and [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) methods are called from within the override of the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method.</span></span> <span data-ttu-id="a4117-113">No entanto, você também pode chamar esses métodos de outros métodos de processamento de entrada.</span><span class="sxs-lookup"><span data-stu-id="a4117-113">However, you can also call these methods from the other input processing methods.</span></span>

```csharp
protected override void ProcessRecord()
{
  if (ShouldProcess("ShouldProcess target"))
  {
    if (Force || ShouldContinue("", ""))
    {
      // Add code that performs the operation.
    }
  }
}
```

## <a name="see-also"></a><span data-ttu-id="a4117-114">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="a4117-114">See Also</span></span>

[<span data-ttu-id="a4117-115">Escrevendo um Cmdlet do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4117-115">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
