---
ms.date: 09/12/2016
ms.topic: reference
title: Como adicionar informações de parâmetro
description: Como adicionar informações de parâmetro
ms.openlocfilehash: 8f4fc46ef256a77b058df4ba506124f80732cb39
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92663050"
---
# <a name="how-to-add-parameter-information"></a>Como adicionar informações de parâmetro

Esta seção descreve como adicionar conteúdo exibido na seção de **parâmetros** do tópico de ajuda do cmdlet. A seção de **parâmetros** do tópico da ajuda lista cada um dos parâmetros do cmdlet e fornece uma descrição detalhada de cada parâmetro.

O conteúdo da seção de **parâmetros** deve ser consistente com o conteúdo da seção de **sintaxe** do tópico da ajuda. É responsabilidade do autor da ajuda garantir que o nó **sintaxe** e **parâmetros** contenha elementos XML semelhantes.

> [!NOTE]
> Para obter uma exibição completa de um arquivo de ajuda, abra um dos `dll-Help.xml` arquivos localizados no diretório de instalação do PowerShell. Por exemplo, o `Microsoft.PowerShell.Commands.Management.dll-Help.xml` arquivo contém conteúdo para vários cmdlets do PowerShell.

### <a name="to-add-parameters"></a>Para adicionar parâmetros

1. Abra o arquivo de ajuda do cmdlet e localize o nó de comando para o cmdlet que você está documentando. Se você estiver adicionando um novo cmdlet, precisará criar um novo nó de comando. O arquivo de ajuda conterá um nó de comando para cada cmdlet para o qual você está fornecendo o conteúdo da ajuda. Aqui está um exemplo de um nó de comando em branco.

    ```xml
    <command:command>
    </command:command>
    ```

1. No nó de comando, localize o nó descrição e adicione um nó de parâmetros, conforme mostrado abaixo.
   Apenas um nó de parâmetros é permitido e deve seguir imediatamente o nó de sintaxe.

    ```xml
    <command:command>
      <command:details></command:details>
      <maml:description></maml:description>
      <command:syntax></command:syntax>
      <command:parameters>
      </command:Parameters>
    </command:command>
    ```

1. Dentro do nó parâmetros, adicione um nó de **parâmetro** para cada parâmetro do cmdlet, conforme mostrado abaixo.

   Neste exemplo, um nó de **parâmetro** é adicionado para três parâmetros.

    ```xml
    <command:parameters>
      <command:parameter></command:parameter>
      <command:parameter></command:parameter>
      <command:parameter></command:parameter>
    </command:Parameters>
    ```

   Como essas são as mesmas marcas XML que são usadas no nó de sintaxe, e como os parâmetros especificados aqui devem corresponder aos parâmetros especificados pelo nó de sintaxe, você pode copiar os nós de parâmetro do nó de sintaxe e colá-los no nó de parâmetros. No entanto, certifique-se de copiar apenas uma instância de um nó de parâmetro, mesmo que o parâmetro seja especificado em vários conjuntos de parâmetros na sintaxe.

1. Para cada nó de parâmetro, defina os valores de atributo que definem as características de cada parâmetro. Esses atributos incluem o seguinte: Required, globaling, PipelineInput e Position.

    ```xml
    <command:parameters>
      <command:parameter required="true" globbing="true"
               pipelineInput="false" position="named">
      </command:parameter>
      <command:parameter required="false" globbing="false"
               pipelineInput="false" position="named">
      </command:parameter>
      <command:parameter required="false" globbing="false"
               pipelineInput="false" position="named" ></command:parameter>
    </command:Parameters>
    ```

1. Para cada nó de parâmetro, adicione o nome do parâmetro. Aqui está um exemplo do nome do parâmetro adicionado ao nó do parâmetro.

    ```xml
    <command:parameters>
      <command:parameter required="true" globbing="true"
               pipelineInput="false" position="named">
        <maml:name> Add parameter name...  </maml:name>
      </command:parameter>
    </command:Parameters>
    ```

1. Para cada nó de **parâmetro** , adicione a descrição do parâmetro. Aqui está um exemplo da descrição do parâmetro adicionada ao nó de **parâmetro** .

    ```xml
    <command:parameters>
      <command:parameter required="true" globbing="true"
               pipelineInput="false" position="named">
        <maml:name> Add parameter name...  </maml:name>
        <maml:description>
          <maml:para> Add parameter description... </maml:para>
        </maml:description>
      </command:parameter>
    </command:parameters>
    ```

1. Para cada nó de **parâmetro** , adicione o tipo .net do parâmetro. O tipo de parâmetro é exibido junto com o nome do parâmetro.

   Aqui está um exemplo do tipo de parâmetro .NET adicionado ao nó de **parâmetro** .

    ```xml
    <command:parameters>
      <command:parameter required="true" globbing="true"
               pipelineInput="false" position="named">
        <maml:name> Add parameter name...  </maml:name>
        <maml:description>
          <maml:para> Add parameter description... </maml:para>
        </maml:description>
        <dev:type> Add .NET Framework type... </dev:type>
      </command:parameter>
    </command:parameters>
    ```

1. Para cada nó de **parâmetro** , adicione o valor padrão do parâmetro. A sentença a seguir é adicionada à descrição do parâmetro quando o conteúdo é exibido: **DefaultValue** é o padrão.

   Aqui está um exemplo do valor padrão do parâmetro que é adicionado ao nó do **parâmetro** .

    ```xml
    <command:parameters>
      <command:parameter required="true" globbing="true"
               pipelineInput="false" position="named">
        <maml:name> Add parameter name...  </maml:name>
        <maml:description>
          <maml:para> Add parameter description... </maml:para>
        </maml:description>
        <dev:type> Add .NET Framework type... </dev:type>
        <dev:defaultvalue> Add default value...</dev:defaultvalue>
      </command:parameter>
    </command:parameters>
    ```

1. Para cada parâmetro que tem vários valores, adicione um nó de valores possíveis.

   Aqui está um exemplo de um nó de valores possíveis que define dois valores possíveis para o parâmetro

    ```xml
    <dev:possiblevalues>
      <dev:possiblevalue>
        <dev:value>Unknown</dev:value>
        <maml:description>
          <maml:para></maml:para>
        </maml:description>
      </dev:possiblevalue>
      <dev:possiblevalue>
        <dev:value>String</dev:value>
        <maml:description>
          <maml:para></maml:para>
        </maml:description>
      </dev:possibleValue>
    </dev:possiblevalues>
    ```

Aqui estão algumas coisas a serem lembradas ao adicionar parâmetros.

- Os atributos do parâmetro não são exibidos em todas as exibições do tópico de ajuda do cmdlet. No entanto, eles são exibidos em uma tabela após a descrição do parâmetro quando o usuário solicita a exibição **completa** ( `Get-Help <cmdletname> -full` ) ou **parâmetro** ( `Get-Help <cmdletname> -parameter` ) do tópico.

- A descrição do parâmetro é uma das partes mais importantes de um tópico de ajuda de cmdlet. A descrição deve ser breve, bem como completa. Além disso, lembre-se de que se a descrição do parâmetro se tornar muito longa, como quando dois parâmetros interagem entre si, você pode adicionar mais conteúdo na seção anotações do tópico de ajuda do cmdlet.

  A descrição do parâmetro fornece dois tipos de informações.

- O que o cmdlet faz quando o parâmetro é usado.

- O que é um valor válido para o parâmetro.

- Como os valores de parâmetro são expressos como objetos .NET, os usuários precisam de mais informações sobre esses valores do que em uma ajuda de linha de comando tradicional. Informe ao usuário que tipo de dados o parâmetro foi projetado para aceitar e inclua exemplos.

O valor padrão do parâmetro é o valor que será usado se o parâmetro não for especificado na linha de comando. Observe que o valor padrão é opcional e não é necessário para alguns parâmetros, como os parâmetros necessários. No entanto, você deve especificar um valor padrão para a maioria dos parâmetros opcionais.

O valor padrão ajuda o usuário a entender o efeito de não usar o parâmetro. Descreva o valor padrão muito especificamente, como o "diretório atual" ou o "diretório de instalação do PowerShell ( `$PSHOME` )" para um caminho opcional. Você também pode escrever uma frase que descreva o padrão, como a seguinte frase usada para o parâmetro **PassThru** : "Se PassThru não for especificado, o cmdlet não passa objetos pelo pipeline". Além disso, como o valor é exibido em oposto ao **valor padrão** do nome do campo, não é necessário incluir o termo "valor padrão" na entrada.

O valor padrão do parâmetro não é exibido em todas as exibições do tópico de ajuda do cmdlet. No entanto, ele é exibido em uma tabela (juntamente com os atributos de parâmetro) após a descrição do parâmetro quando o usuário solicita a exibição **completa** ( `Get-Help <cmdletname> -full` ) ou **parâmetro** ( `Get-Help
<cmdletname> -parameter` ) do tópico.

O XML a seguir mostra um par de `<dev:defaultValue>` marcas adicionadas ao `<command:parameter>` nó.
Observe que o valor padrão segue imediatamente após a marca de fechamento `</command:parameterValue>` (quando o valor do parâmetro é especificado) ou a `</maml:description>` marca de fechamento da descrição do parâmetro. nome.

```xml
<command:parameters>
  <command:parameter required="true" globbing="true"
           pipelineInput="false" position="named">
    <maml:name> Parameter name </maml:name>
    <maml:description>
      <maml:para> Parameter Description </maml:para>
    </maml:description>
    <command:parameterValue required="true">
      Value
    </command:parameterValue>
    <dev:defaultValue> Default parameter value </dev:defaultValue>
  </command:parameter>
</command:parameters>
```

Adicionar valores para tipos enumerados

Se o parâmetro tiver vários valores ou valores de um tipo enumerado, você poderá usar um \<dev:possibleValues> nó opcional. Esse nó permite que você especifique um nome e uma descrição para vários valores.

Lembre-se de que as descrições dos valores enumerados não aparecem em nenhum dos modos de exibição padrão da ajuda exibidos pelo `Get-Help` cmdlet, mas outros visualizadores da ajuda podem exibir esse conteúdo em suas exibições.

O XML a seguir mostra um `<dev:possibleValues>` nó com dois valores especificados.

```xml
<command:parameters>
  <command:parameter required="true" globbing="true"
           pipelineInput="false" position="named">
    <maml:name> Parameter name </maml:name>
    <maml:description>
      <maml:para> Parameter Description </maml:para>
    </maml:description>
    <command:parameterValue required="true">
      Value
    </command:parameterValue>
    <dev:defaultValue> Default parameter value </dev:defaultValue>
    <dev:possibleValues>
      <dev:possibleValue>
        <dev:value> Value 1 </dev:value>
        <maml:description>
          <maml:para> Description 1 </maml:para>
        </maml:description>
      <dev:possibleValue>
      <dev:possibleValue>
        <dev:value> Value 2 </dev:value>
        <maml:description>
          <maml:para> Description 2 </maml:para>
        </maml:description>
      <dev:possibleValue>
    </dev:possibleValues>
  </command:parameter>
</command:parameters>
```
