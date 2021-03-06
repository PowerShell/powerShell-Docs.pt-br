---
ms.date: 09/13/2016
ms.topic: reference
title: Elemento TableControl (formato)
description: Elemento TableControl (formato)
ms.openlocfilehash: 93e05e22d61504d7781b6f3c07f9a3fd0b3c9e8a
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92651456"
---
# <a name="tablecontrol-element-format"></a>Elemento TableControl (formato)

Define um formato de tabela para uma exibição.

Elemento ViewDefinitions (Format) View element (Format) TableControl elemento (Format)

## <a name="syntax"></a>Sintaxe

```xml
<TableControl>
  <AutoSize/>
  <HideTableHeaders/>
  <TableHeaders>...</TableHeaders>
  <TableRowEntries>...</TableRowEntries>
</TableControl>

```

## <a name="attributes-and-elements"></a>Atributos e elementos

As seções a seguir descrevem atributos, elementos filho e elemento pai do `TableControl` elemento. Você deve especificar as linhas da tabela. Todos os outros elementos filho são opcionais.

### <a name="attributes"></a>Atributos

nenhuma.

### <a name="child-elements"></a>Elementos filho

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento AutoSize para TableControl (formato)](./autosize-element-for-tablecontrol-format.md)|Elemento opcional.<br /><br /> Especifica se o tamanho da coluna e o número de colunas são ajustados com base no tamanho dos dados.|
|[Elemento HideTableHeaders para TableControl (Format)](./hidetableheaders-element-format.md)|Elemento opcional.<br /><br /> Indica se o cabeçalho da tabela não é exibido.|
|[Elemento TableHeaders para TableControl (Format)](./tableheaders-element-format.md)|Elemento necessário.<br /><br /> Define os rótulos, as larguras e o alinhamento dos dados para as colunas da exibição de tabela.|
|[Elemento TableRowEntries para TableControl (formato)](./tablerowentries-element-for-tablecontrol-format.md)|Elemento opcional.<br /><br /> Fornece as definições do modo de exibição de tabela.|

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento View (formato)](./view-element-format.md)|Define uma exibição que é usada para exibir os membros de um ou mais objetos.|

## <a name="remarks"></a>Comentários

Para obter mais informações sobre os componentes de uma exibição de tabela, consulte [criando uma exibição de tabela](./creating-a-table-view.md).

## <a name="example"></a>Exemplo

Este exemplo mostra um `TableControl` elemento que é usado para exibir as propriedades do objeto [System. ServiceProcess. ServiceController](/dotnet/api/System.ServiceProcess.ServiceController) .

```xml
<View>
  <Name>service</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <TableControl>
    <TableHeaders>...</TableHeaders>
    <TableRowEntries>...</TableRowEntries>
  </TableControl>
</View>

```

## <a name="see-also"></a>Consulte Também

[Criar uma exibição de tabela](./creating-a-table-view.md)

[Elemento View (formato)](./view-element-format.md)

[Elemento AutoSize para TableControl (formato)](./autosize-element-for-tablecontrol-format.md)

[Elemento HideTableHeaders (formato)](./hidetableheaders-element-format.md)

[Elemento TableHeaders (formato)](./tableheaders-element-format.md)

[Elemento TableRowEntries (Format)](./tablerowentries-element-for-tablecontrol-format.md)

[Escrever um arquivo de formatação do PowerShell](./writing-a-powershell-formatting-file.md)
