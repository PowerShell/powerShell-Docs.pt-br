---
title: Exibição de lista (básica) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 918f381c-43e6-4594-a468-a40bfa8a16d6
caps.latest.revision: 7
ms.openlocfilehash: 3c94d8e98f179286112a417230fce659dc0b614c
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "72362805"
---
# <a name="list-view-basic"></a>Exibição de lista (Básica)

Este exemplo mostra como implementar um modo de exibição de lista básico que exibe o [System. ServiceProcess. ServiceController? Objetos displayproperty = FullName](/dotnet/api/System.ServiceProcess.ServiceController) retornados pelo cmdlet [Get-Service](/powershell/module/microsoft.powershell.management/get-service) . Para obter mais informações sobre os componentes de um modo de exibição de lista, consulte [criando uma exibição de lista](./creating-a-list-view.md).

### <a name="to-load-this-formatting-file"></a>Para carregar este arquivo de formatação

1. Copie o XML da seção de exemplo deste tópico em um arquivo de texto.

2. Salve o arquivo de texto. Certifique-se de adicionar a extensão de `format.ps1xml` ao arquivo para identificá-lo como um arquivo de formatação.

3. Abra o Windows PowerShell e execute o seguinte comando para carregar o arquivo de formatação na sessão atual: `Update-formatdata -prependpath PathToFormattingFile`.

   > [!WARNING]
   > Esse arquivo de formatação define a exibição de um objeto que já está definido por um arquivo de formatação do Windows PowerShell. Você deve usar o parâmetro `prependPath` ao executar o cmdlet e não pode carregar esse arquivo de formatação como um módulo.

## <a name="demonstrates"></a>Demonstra

Esse arquivo de formatação demonstra os seguintes elementos XML:

- O elemento [Name](./name-element-for-view-format.md) para a exibição.

- O elemento [ViewSelectedBy](./viewselectedby-element-format.md) que define quais objetos são exibidos pela exibição.

- O elemento [ListControl](./listcontrol-element-format.md) que define qual propriedade é exibida pela exibição.

- O elemento [ListItem](./listitem-element-for-listitems-for-listcontrol-format.md) que define o que é exibido em uma linha da exibição de lista.

- O elemento [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) que define qual propriedade é exibida.

## <a name="example"></a>Exemplo

O XML a seguir define um modo de exibição de lista que exibe quatro propriedades de [System. ServiceProcess. ServiceController? Displayproperty = objeto FullName](/dotnet/api/System.ServiceProcess.ServiceController) . Em cada linha, o nome da propriedade é exibido seguido pelo valor da propriedade.

```xml
<Configuration>
  <View>
    <Name>System.ServiceProcess.ServiceController</Name>
    <ViewSelectedBy>
      <TypeName>System.ServiceProcess.ServiceController</TypeName>
    </ViewSelectedBy>
    <ListControl>
      <ListEntries>
        <ListEntry>
          <ListItems>
            <ListItem>
              <PropertyName>Name</PropertyName>
            </ListItem>
            <ListItem>
              <PropertyName>DisplayName</PropertyName>
            </ListItem>
            <ListItem>
              <PropertyName>Status</PropertyName>
            </ListItem>
            <ListItem>
              <PropertyName>ServiceType</PropertyName>
            </ListItem>
          </ListItems>
        </ListEntry>
      </ListEntries>
    </ListControl>
  </View>
</Configuration>
```

O exemplo a seguir mostra como o Windows PowerShell exibe o [System. ServiceProcess. ServiceController? Objetos displayproperty = FullName](/dotnet/api/System.ServiceProcess.ServiceController) depois que esse arquivo de formato é carregado.

```powershell
Get-Service f*
```

```output
Name        : Fax
DisplayName : Fax
Status      : Stopped
ServiceType : Win32OwnProcess

Name        : FCSAM
DisplayName : Microsoft Antimalware Service
Status      : Running
ServiceType : Win32OwnProcess

Name        : fdPHost
DisplayName : Function Discovery Provider Host
Status      : Stopped
ServiceType : Win32ShareProcess

Name        : FDResPub
DisplayName : Function Discovery Resource Publication
Status      : Running
ServiceType : Win32ShareProcess

Name        : FontCache
DisplayName : Windows Font Cache Service
Status      : Running
ServiceType : Win32ShareProcess

Name        : FontCache3.0.0.0
DisplayName : Windows Presentation Foundation Font Cache 3.0.0.0
Status      : Stopped
ServiceType : Win32OwnProcess

Name        : FSysAgent
DisplayName : Microsoft Forefront System Agent
Status      : Running
ServiceType : Win32OwnProcess

Name        : FwcAgent
DisplayName : Firewall Client Agent
Status      : Running
ServiceType : Win32OwnProcess
```

## <a name="see-also"></a>Consulte Também

[Exemplos de arquivos de formatação](./examples-of-formatting-files.md)

[Gravando um arquivo de formatação do PowerShell](./writing-a-powershell-formatting-file.md)
