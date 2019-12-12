---
title: Como validar o comprimento do argumento | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ValidateLength attribute, example
ms.assetid: d5ddaa6e-4904-46da-beb0-0295a8f38332
caps.latest.revision: 12
ms.openlocfilehash: 8a21675acd087df93f93c25952c78931255d60b3
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "72365485"
---
# <a name="how-to-validate-the-argument-length"></a><span data-ttu-id="305a7-102">Como validar o tamanho do argumento</span><span class="sxs-lookup"><span data-stu-id="305a7-102">How to Validate the Argument Length</span></span>

<span data-ttu-id="305a7-103">Este exemplo mostra como especificar uma regra de validação que o tempo de execução do Windows PowerShell pode usar para verificar o número de caracteres (o comprimento) do argumento de parâmetro antes de o cmdlet ser executado.</span><span class="sxs-lookup"><span data-stu-id="305a7-103">This example shows how to specify a validation rule that the Windows PowerShell runtime can use to check the number of characters (the length) of the parameter argument before the cmdlet is run.</span></span> <span data-ttu-id="305a7-104">Você define essa regra de validação declarando o atributo ValidateLength.</span><span class="sxs-lookup"><span data-stu-id="305a7-104">You set this validation rule by declaring the ValidateLength attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="305a7-105">Para obter mais informações sobre a classe que define esse atributo, consulte [System. Management. Automation. Validatelengthattribute](/dotnet/api/System.Management.Automation.ValidateLengthAttribute).</span><span class="sxs-lookup"><span data-stu-id="305a7-105">For more information about the class that defines this attribute, see [System.Management.Automation.Validatelengthattribute](/dotnet/api/System.Management.Automation.ValidateLengthAttribute).</span></span>

## <a name="to-validate-the-argument-length"></a><span data-ttu-id="305a7-106">Para validar o comprimento do argumento</span><span class="sxs-lookup"><span data-stu-id="305a7-106">To validate the argument length</span></span>

- <span data-ttu-id="305a7-107">Adicione o atributo Validate conforme mostrado no código a seguir.</span><span class="sxs-lookup"><span data-stu-id="305a7-107">Add the Validate attribute as shown in the following code.</span></span> <span data-ttu-id="305a7-108">Este exemplo especifica que o comprimento do argumento deve ter um comprimento de 0 a 10 caracteres.</span><span class="sxs-lookup"><span data-stu-id="305a7-108">This example specifies that the length of the argument should have a length of 0 to 10 characters.</span></span>

    ```csharp
    [ValidateLength(0, 10)]
    [Parameter(Position = 0, Mandatory = true)]
    public string UserName
    {
      get { return userName; }
      set { userName = value; }
    }
    private string userName;
    ```

<span data-ttu-id="305a7-109">Para obter mais informações sobre como declarar esse atributo, consulte [declaração de atributo ValidateLength](./validatelength-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="305a7-109">For more information about how to declare this attribute, see [ValidateLength Attribute Declaration](./validatelength-attribute-declaration.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="305a7-110">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="305a7-110">See Also</span></span>

[<span data-ttu-id="305a7-111">Declaração de atributo ValidateLength</span><span class="sxs-lookup"><span data-stu-id="305a7-111">ValidateLength Attribute Declaration</span></span>](./validatelength-attribute-declaration.md)

<span data-ttu-id="305a7-112">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md) (Escrevendo um Cmdlet do Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="305a7-112">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md)</span></span>
