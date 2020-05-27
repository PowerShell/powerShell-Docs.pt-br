---
ms.date: 06/12/2017
keywords: DSC,powershell,configuração,instalação
title: Chamando métodos do recurso DSC diretamente
ms.openlocfilehash: 9955de4f284c182a724b004c17080a8b8e19808d
ms.sourcegitcommit: 17d798a041851382b406ed789097843faf37692d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2020
ms.locfileid: "83692405"
---
# <a name="calling-dsc-resource-methods-directly"></a>Chamando métodos do recurso DSC diretamente

>Aplica-se a: Windows PowerShell 5.0

Você pode usar o cmdlet [Invoke-DscResource](/powershell/module/PSDesiredStateConfiguration/Invoke-DscResource) para chamar diretamente as funções ou os métodos de um recurso DSC (As funções **Get-TargetResource**, **Set-TargetResource** e **Test-TargetResource** de um recurso baseado em MOF ou os métodos **Get**, **Set** e **Test** de um recurso baseado em classe).
Isso pode ser usado por terceiros que querem usar recursos DSC, ou como uma ferramenta útil ao desenvolver recursos.

Geralmente, esse cmdlet é usado em combinação com uma propriedade de metaconfiguração `refreshMode = 'Disabled'`, mas pode ser usado, independentemente do **refreshMode** para o qual está definido.

Ao chamar o cmdlet **Invoke-DscResource**, você especifica qual método ou função chamar usando o parâmetro **Method**. Especifique as propriedades do recurso passando uma tabela de hash como o valor do parâmetro **Property**.

A seguir, exemplos de chamada direta aos métodos do recurso:

## <a name="ensure-a-file-is-present"></a>Certificar-se de que um arquivo está presente

```powershell
$result = Invoke-DscResource -Name File -Method Set -Property @{
              DestinationPath = "$env:SystemDrive\\DirectAccess.txt";
              Contents = 'This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="test-that-a-file-is-present"></a>Testar se um arquivo está presente

```powershell
$result = Invoke-DscResource -Name File -Method Test -Property @{
              DestinationPath="$env:SystemDrive\\DirectAccess.txt";
              Contents='This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="get-the-contents-of-file"></a>Obter o conteúdo do arquivo

```powershell
$result = Invoke-DscResource -Name File -Method Get -Property @{
              DestinationPath="$env:SystemDrive\\DirectAccess.txt";
              Contents='This file is create by Invoke-DscResource'} -Verbose
$result.ItemValue | fl
```

>**Observação:** não é permitido chamar diretamente métodos de recurso de composição. Em vez disso, chame os métodos de recursos subjacentes que compõem o recurso de composição.

## <a name="see-also"></a>Consulte Também

- [Escrevendo um recurso personalizado de DSC com MOF](../resources/authoringResourceMOF.md)
- [Escrevendo um recurso personalizado de DSC com classes do PowerShell](../resources/authoringResourceClass.md)
- [Depurando os recursos de DSC](../troubleshooting/debugResource.md)
