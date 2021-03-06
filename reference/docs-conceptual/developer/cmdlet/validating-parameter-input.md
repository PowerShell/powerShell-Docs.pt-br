---
ms.date: 09/13/2016
ms.topic: reference
title: Validação de entrada de parâmetro
description: Validação de entrada de parâmetro
ms.openlocfilehash: a97b5c670e8c36463a85bbef1506f6311bdd5ec3
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92660391"
---
# <a name="validating-parameter-input"></a>Validação de entrada de parâmetro

O PowerShell pode validar os argumentos passados para parâmetros de cmdlet de várias maneiras.
O PowerShell pode validar o comprimento, o intervalo e o padrão dos caracteres do argumento.
Ele pode validar o número de argumentos disponíveis (a contagem).
Essas regras de validação são definidas por atributos de validação que são declarados com o atributo Parameter em propriedades públicas da classe cmdlet.

Para validar um argumento de parâmetro, o tempo de execução do PowerShell usa as informações fornecidas pelos atributos de validação para confirmar o valor do parâmetro antes da execução do cmdlet.
Se a entrada do parâmetro não for válida, o usuário receberá uma mensagem de erro.
Cada parâmetro de validação define uma regra de validação que é imposta pelo PowerShell.

O PowerShell impõe as regras de validação com base nos atributos a seguir.

### <a name="validatecount"></a>ValidateCount

Especifica o número mínimo e máximo de argumentos que um parâmetro pode aceitar.
Para obter mais informações, consulte [declaração de atributo ValidateCount](./validatecount-attribute-declaration.md).

### <a name="validatelength"></a>ValidateLength

Especifica o número mínimo e máximo de caracteres no argumento de parâmetro.
Para obter mais informações, consulte [declaração de atributo ValidateLength](./validatelength-attribute-declaration.md).

### <a name="validatepattern"></a>ValidatePattern

Especifica uma expressão regular que valida o argumento do parâmetro.
Para obter mais informações, consulte [declaração de atributo ValidatePattern](./validatepattern-attribute-declaration.md).

### <a name="validaterange"></a>ValidateRange

Especifica os valores mínimo e máximo do argumento de parâmetro.
Para obter mais informações, consulte [declaração de atributo ValidateRange](./validaterange-attribute-declaration.md).

### <a name="validateset"></a>ValidateSet

Especifica os valores válidos para o argumento de parâmetro.
Para obter mais informações, consulte [declaração de atributo ValidateSet](./validateset-attribute-declaration.md).

## <a name="see-also"></a>Consulte Também

[Como validar a entrada de parâmetro](./how-to-validate-parameter-input.md)

[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md) (Escrevendo um Cmdlet do Windows PowerShell)
