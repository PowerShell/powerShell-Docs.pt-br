---
ms.date: 09/13/2016
ms.topic: reference
title: Parâmetros dinâmicos de cmdlet
description: Parâmetros dinâmicos de cmdlet
ms.openlocfilehash: b44dda2354e8b689e419c7bf4deefadfc4edcb07
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92653434"
---
# <a name="cmdlet-dynamic-parameters"></a>Parâmetros dinâmicos de cmdlet

Os cmdlets podem definir parâmetros que estão disponíveis para o usuário em condições especiais, como quando o argumento de outro parâmetro é um valor específico. Esses parâmetros são adicionados em tempo de execução e são chamados de parâmetros dinâmicos porque são adicionados apenas quando necessário. Por exemplo, você pode criar um cmdlet que adiciona vários parâmetros somente quando um parâmetro de opção específico é especificado.

> [!NOTE]
> Provedores e funções do PowerShell também podem definir parâmetros dinâmicos.

## <a name="dynamic-parameters-in-powershell-cmdlets"></a>Parâmetros dinâmicos nos cmdlets do PowerShell

O PowerShell usa parâmetros dinâmicos em vários dos seus cmdlets de provedor. Por exemplo, os `Get-Item` `Get-ChildItem` cmdlets e adicionam um parâmetro **CodeSigningCert** em tempo de execução quando o parâmetro **Path** especifica o caminho do provedor de **certificado** . Se o parâmetro **path** especificar um caminho para um provedor diferente, o parâmetro **CodeSigningCert** não estará disponível.

Os exemplos a seguir mostram como o parâmetro **CodeSigningCert** é adicionado em tempo de execução quando `Get-Item` é executado.

Neste exemplo, o tempo de execução do PowerShell adicionou o parâmetro e o cmdlet foi bem-sucedido.

```powershell
Get-Item -Path cert:\CurrentUser -CodeSigningCert
```

```Output
Location   : CurrentUser
StoreNames : {SmartCardRoot, UserDS, AuthRoot, CA...}
```

Neste exemplo, uma unidade de **sistema de arquivos** é especificada e um erro é retornado. A mensagem de erro indica que o parâmetro **CodeSigningCert** não pode ser encontrado.

```powershell
Get-Item -Path C:\ -CodeSigningCert
```

```Output
Get-Item : A parameter cannot be found that matches parameter name 'codesigningcert'.
At line:1 char:37
+  get-item -path C:\ -codesigningcert <<<<
--------
    CategoryInfo          : InvalidArgument: (:) [Get-Item], ParameterBindingException
    FullyQualifiedErrorId : NamedParameterNotFound,Microsoft.PowerShell.Commands.GetItemCommand
```

## <a name="support-for-dynamic-parameters"></a>Suporte para parâmetros dinâmicos

Para dar suporte a parâmetros dinâmicos, os elementos a seguir devem ser incluídos no código do cmdlet.

### <a name="interface"></a>Interface

[System. Management. Automation. IDynamicParameters](/dotnet/api/System.Management.Automation.IDynamicParameters).
Essa interface fornece o método que recupera os parâmetros dinâmicos.

Por exemplo:

`public class SendGreetingCommand : Cmdlet, IDynamicParameters`

### <a name="method"></a>Método

[System. Management. Automation. IDynamicParameters. Getdynamicparameters](/dotnet/api/System.Management.Automation.IDynamicParameters.GetDynamicParameters).
Esse método recupera o objeto que contém as definições de parâmetro dinâmico.

Por exemplo:

```csharp
 public object GetDynamicParameters()
 {
   if (employee)
   {
     context= new SendGreetingCommandDynamicParameters();
     return context;
   }
   return null;
}
private SendGreetingCommandDynamicParameters context;
```

### <a name="class"></a>Classe

Uma classe que define os parâmetros dinâmicos a serem adicionados. Essa classe deve incluir um atributo de **parâmetro** para cada parâmetro e qualquer **alias** opcional e atributos de **validação** que são necessários para o cmdlet.

Por exemplo:

```csharp
public class SendGreetingCommandDynamicParameters
{
  [Parameter]
  [ValidateSet ("Marketing", "Sales", "Development")]
  public string Department
  {
    get { return department; }
    set { department = value; }
  }
  private string department;
}
```

Para obter um exemplo completo de um cmdlet que dá suporte a parâmetros dinâmicos, consulte [como declarar parâmetros dinâmicos](./how-to-declare-dynamic-parameters.md).

## <a name="see-also"></a>Veja também

[System. Management. Automation. IDynamicParameters](/dotnet/api/System.Management.Automation.IDynamicParameters)

[System. Management. Automation. IDynamicParameters. getdynamicparameters](/dotnet/api/System.Management.Automation.IDynamicParameters.GetDynamicParameters)

[Como declarar parâmetros dinâmicos](./how-to-declare-dynamic-parameters.md)

[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md) (Escrevendo um Cmdlet do Windows PowerShell)
