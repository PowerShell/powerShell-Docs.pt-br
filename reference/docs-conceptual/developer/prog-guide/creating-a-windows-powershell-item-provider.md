---
ms.date: 09/13/2016
ms.topic: reference
title: Criar um provedor de itens do Windows PowerShell
description: Criar um provedor de itens do Windows PowerShell
ms.openlocfilehash: f98ea90bf9ce7222076a91fb26dc42977c70bff2
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92645180"
---
# <a name="creating-a-windows-powershell-item-provider"></a>Criar um provedor de itens do Windows PowerShell

Este tópico descreve como criar um provedor do Windows PowerShell que pode manipular os dados em um armazenamento de dados. Neste tópico, os elementos de dados no repositório são chamados de "itens" do repositório de dados. Como consequência, um provedor que pode manipular os dados no repositório é conhecido como um provedor de itens do Windows PowerShell.

> [!NOTE]
> Você pode baixar o arquivo de origem do C# (AccessDBSampleProvider03.cs) para este provedor usando o kit de desenvolvimento de software do Microsoft Windows para Windows Vista e .NET Framework os componentes de tempo de execução do 3,0. Para obter instruções de download, consulte [como instalar o Windows PowerShell e baixar o SDK do Windows PowerShell](/powershell/scripting/developer/installing-the-windows-powershell-sdk).
> Os arquivos de origem baixados estão disponíveis no **\<PowerShell Samples>** diretório. Para obter mais informações sobre outras implementações de provedor do Windows PowerShell, consulte [projetando seu provedor do Windows PowerShell](./designing-your-windows-powershell-provider.md).

O provedor de item do Windows PowerShell descrito neste tópico Obtém itens de dados de um banco de dado do Access. Nesse caso, um "item" é uma tabela no banco de dados do Access ou uma linha em uma tabela.

## <a name="defining-the-windows-powershell-item-provider-class"></a>Definindo a classe do provedor de item do Windows PowerShell

Um provedor de item do Windows PowerShell deve definir uma classe .NET que deriva da classe base [System. Management. Automation. Provider. @ cmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) . A seguir está a definição de classe para o provedor de item descrito nesta seção.

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample03/AccessDBProviderSample03.cs" range="34-36":::

Observe que nessa definição de classe, o atributo [System. Management. Automation. Provider. Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) inclui dois parâmetros. O primeiro parâmetro especifica um nome amigável para o provedor usado pelo Windows PowerShell. O segundo parâmetro especifica os recursos específicos do Windows PowerShell que o provedor expõe para o tempo de execução do Windows PowerShell durante o processamento do comando. Para esse provedor, não há nenhum recurso específico do Windows PowerShell adicionado.

## <a name="defining-base-functionality"></a>Definindo a funcionalidade base

Conforme descrito em [criar seu provedor do Windows PowerShell](./designing-your-windows-powershell-provider.md), a classe [System. Management. Automation. Provider. Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) deriva de várias outras classes que forneceram funcionalidade de provedor diferente. Portanto, um provedor de item do Windows PowerShell deve definir toda a funcionalidade fornecida por essas classes.

Para obter mais informações sobre como implementar a funcionalidade para adicionar informações de inicialização específicas da sessão e para liberar recursos usados pelo provedor, consulte [criando um provedor básico do Windows PowerShell](./creating-a-basic-windows-powershell-provider.md).
No entanto, a maioria dos provedores, incluindo o provedor descrito aqui, pode usar a implementação padrão dessa funcionalidade fornecida pelo Windows PowerShell.

Antes que o provedor de itens do Windows PowerShell possa manipular os itens no repositório, ele deve implementar os métodos da classe base [System. Management. Automation. Provider. Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) para acessar o armazenamento de dados. Para obter mais informações sobre como implementar essa classe, consulte [criando um provedor de unidade do Windows PowerShell](./creating-a-windows-powershell-drive-provider.md).

## <a name="checking-for-path-validity"></a>Verificando a validade do caminho

Ao procurar um item de dados, o tempo de execução do Windows PowerShell fornece um caminho do Windows PowerShell para o provedor, conforme definido na seção "conceitos de PSPath" de [como o Windows PowerShell funciona](/previous-versions/ms714658(v=vs.85)).
Um provedor de item do Windows PowerShell deve verificar a sintaxe sintática e semântica de qualquer caminho passado para ele implementando o método [System. Management. Automation. Provider. docmdletprovider. Isvalidpath *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.IsValidPath) . Esse método retornará `true` se o caminho for válido e, `false` caso contrário,. Lembre-se de que a implementação desse método não deve verificar a existência do item no caminho, mas apenas que o caminho é sintaticamente e semanticamente correto.

Aqui está a implementação do método [System. Management. Automation. Provider. createcmdletprovider. Isvalidpath *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.IsValidPath) para esse provedor. Observe que essa implementação chama um método auxiliar NormalizePath para converter todos os separadores no caminho para um uniforme.

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample03/AccessDBProviderSample03.cs" range="274-298":::

## <a name="determining-if-an-item-exists"></a>Determinando se um item existe

Depois de verificar o caminho, o tempo de execução do Windows PowerShell deve determinar se existe um item de dados nesse caminho. Para dar suporte a esse tipo de consulta, o provedor de item do Windows PowerShell implementa o método [System. Management. Automation. Provider. docmdletprovider.](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) Itemse *. Esse método retorna `true` um item encontrado no caminho especificado e `false` (padrão) caso contrário.

Aqui está a implementação do método [System. Management. Automation. Provider. createcmdletprovider. myexists *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) para esse provedor. Observe que esse método chama os métodos auxiliares PathIsDrive, ChunkPath e GetTable e usa um objeto DatabaseTableInfo definido pelo provedor.

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample03/AccessDBProviderSample03.cs" range="229-267":::

#### <a name="things-to-remember-about-implementing-itemexists"></a>Coisas a serem lembradas sobre a implementação de itens existentes

As condições a seguir podem se aplicar à implementação de [System. Management. Automation. Provider. @ cmdletprovider. itens existentes *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists):

- Ao definir a classe do provedor, um provedor de item do Windows PowerShell pode declarar os recursos do provedor de ExpandWildcards, filtrar, incluir ou excluir da enumeração [System. Management. Automation. Provider. Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) . Nesses casos, a implementação do método [System. Management. Automation. Provider. docmdletprovider. myexists *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) deve garantir que o caminho passado para o método atenda aos requisitos dos recursos especificados. Para fazer isso, o método deve acessar a propriedade apropriada, por exemplo, as propriedades [System. Management. Automation. Provider. cmdletprovider. Exclude *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) e [System. Management. Automation. Provider. cmdletprovider. include *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) .

- A implementação desse método deve lidar com qualquer forma de acesso ao item que pode tornar o item visível para o usuário. Por exemplo, se um usuário tiver acesso de gravação a um arquivo por meio do provedor FileSystem (fornecido pelo Windows PowerShell), mas não tiver acesso de leitura, o arquivo ainda existirá e [System. Management. Automation. Provider. @ cmdletprovider. myexists *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) retornará `true` . Sua implementação pode exigir a verificação de um item pai para ver se o item filho pode ser enumerado.

## <a name="attaching-dynamic-parameters-to-the-test-path-cmdlet"></a>Anexando parâmetros dinâmicos ao cmdlet Test-Path

Às vezes, o `Test-Path` cmdlet que chama [System. Management. Automation. Provider. docmdletprovider. myexists *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) requer parâmetros adicionais que são especificados dinamicamente no tempo de execução. Para fornecer esses parâmetros dinâmicos, o provedor de item do Windows PowerShell deve implementar o método [System. Management. Automation. Provider. docmdletprovider. Itemexistsdynamicparameters *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExistsDynamicParameters) . Esse método recupera os parâmetros dinâmicos para o item no caminho indicado e retorna um objeto que tem propriedades e campos com atributos de análise semelhantes a uma classe de cmdlet ou um objeto [System. Management. Automation. Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) . O tempo de execução do Windows PowerShell usa o objeto retornado para adicionar os parâmetros ao `Test-Path` cmdlet.

Este provedor de item do Windows PowerShell não implementa esse método. No entanto, o código a seguir é a implementação padrão desse método.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovideritemexistdynamicparameters](Msh_samplestestcmdlets#testprovideritemexistdynamicparameters)]  -->

## <a name="retrieving-an-item"></a>Recuperando um item

Para recuperar um item, o provedor de item do Windows PowerShell deve substituir o método [System. Management. Automation. Provider. docmdletprovider. GetItem *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) para dar suporte a chamadas do `Get-Item` cmdlet. Esse método grava o item usando o método [System. Management. Automation. Provider. cmdletprovider. Writeitemobject *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteItemObject) .

Aqui está a implementação do método [System. Management. Automation. Provider. createcmdletprovider. GetItem *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) para esse provedor. Observe que esse método usa os métodos auxiliares GetTable e GetRow para recuperar itens que são tabelas no banco de dados do Access ou linhas em uma tabela Data.

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample03/AccessDBProviderSample03.cs" range="132-163":::

#### <a name="things-to-remember-about-implementing-getitem"></a>Coisas a serem lembradas sobre a implementação de GetItem

As condições a seguir podem se aplicar a uma implementação de [System. Management. Automation. Provider. @ cmdletprovider. GetItem *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem):

- Ao definir a classe do provedor, um provedor de item do Windows PowerShell pode declarar os recursos do provedor de ExpandWildcards, filtrar, incluir ou excluir da enumeração [System. Management. Automation. Provider. Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) . Nesses casos, a implementação de [System. Management. Automation. Provider. @ cmdletprovider. GetItem *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) deve garantir que o caminho passado para o método atenda a esses requisitos. Para fazer isso, o método deve acessar a propriedade apropriada, por exemplo, as propriedades [System. Management. Automation. Provider. cmdletprovider. Exclude *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) e [System. Management. Automation. Provider. cmdletprovider. include *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) .

- Por padrão, as substituições desse método não devem recuperar objetos que geralmente são ocultados do usuário, a menos que a propriedade [System. Management. Automation. Provider. cmdletprovider. Force *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) seja definida como `true` . Por exemplo, o método [System. Management. Automation. Provider. itempropertyprovider. GetItem *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) para o provedor FileSystem verifica a propriedade [System. Management. Automation. Provider. cmdletprovider. Force *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) antes de tentar chamar [System. Management. Automation. Provider. cmdletprovider. Writeitemobject *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteItemObject) para arquivos ocultos ou do sistema.

## <a name="attaching-dynamic-parameters-to-the-get-item-cmdlet"></a>Anexando parâmetros dinâmicos ao cmdlet Get-Item

Às vezes, o `Get-Item` cmdlet requer parâmetros adicionais que são especificados dinamicamente no tempo de execução. Para fornecer esses parâmetros dinâmicos, o provedor de item do Windows PowerShell deve implementar o método [System. Management. Automation. Provider. docmdletprovider. Getitemdynamicparameters *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItemDynamicParameters) . Esse método recupera os parâmetros dinâmicos para o item no caminho indicado e retorna um objeto que tem propriedades e campos com atributos de análise semelhantes a uma classe de cmdlet ou um objeto [System. Management. Automation. Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) . O tempo de execução do Windows PowerShell usa o objeto retornado para adicionar os parâmetros ao `Get-Item` cmdlet.

Este provedor não implementa esse método. No entanto, o código a seguir é a implementação padrão desse método.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidergetitemdynamicparameters](Msh_samplestestcmdlets#testprovidergetitemdynamicparameters)]  -->

## <a name="setting-an-item"></a>Configurando um item

Para definir um item, o provedor de item do Windows PowerShell deve substituir o método [System. Management. Automation. Provider. docmdletprovider. SetItem *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) para dar suporte a chamadas do `Set-Item` cmdlet. Esse método define o valor do item no caminho especificado.

Este provedor não fornece uma substituição para o método  [System. Management. Automation. Provider. createcmdletprovider. SetItem *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) . No entanto, a implementação padrão desse método é a seguinte:

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidersetitem](Msh_samplestestcmdlets#testprovidersetitem)]  -->

#### <a name="things-to-remember-about-implementing-setitem"></a>Coisas a serem lembradas sobre a implementação de SetItem

As condições a seguir podem se aplicar à implementação de [System. Management. Automation. Provider. @ cmdletprovider. SetItem *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem):

- Ao definir a classe do provedor, um provedor de item do Windows PowerShell pode declarar os recursos do provedor de ExpandWildcards, filtrar, incluir ou excluir da enumeração [System. Management. Automation. Provider. Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) . Nesses casos, a implementação de [System. Management. Automation. Provider. @ cmdletprovider. SetItem *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) deve garantir que o caminho passado para o método atenda a esses requisitos. Para fazer isso, o método deve acessar a propriedade apropriada, por exemplo, as propriedades [System. Management. Automation. Provider. cmdletprovider. Exclude *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) e [System. Management. Automation. Provider. cmdletprovider. include *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) .

- Por padrão, as substituições desse método não devem definir ou gravar objetos ocultos do usuário, a menos que a propriedade [System. Management. Automation. Provider. cmdletprovider. Force *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) seja definida como `true` . Um erro deve ser enviado para o método [System. Management. Automation. Provider. cmdletprovider. WriteError](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteError) se o caminho representar um item oculto e [System. Management. Automation. Provider. cmdletprovider. Force *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) é definido como `false` .

- Sua implementação do método [System. Management. Automation. Provider. docmdletprovider. SetItem *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) deve chamar [System. Management. Automation. Provider. cmdletprovider. ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) e verificar seu valor de retorno antes de fazer qualquer alteração no armazenamento de dados. Esse método é usado para confirmar a execução de uma operação quando uma alteração é feita no armazenamento de dados, por exemplo, excluindo arquivos. O método [System. Management. Automation. Provider. cmdletprovider. ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) envia o nome do recurso a ser alterado para o usuário, com o tempo de execução do Windows PowerShell levando em conta quaisquer configurações de linha de comando ou variáveis de preferência para determinar o que deve ser exibido.

  Após a chamada para [System. Management. Automation. Provider. cmdletprovider. ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) retornar `true` , o método [System. Management. Automation. Provider. docmdletprovider. SetItem *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) deverá chamar o método [System. Management. Automation. Provider. cmdletprovider. ShouldContinue](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) . Esse método envia uma mensagem ao usuário para permitir que os comentários verifiquem se a operação deve continuar. A chamada para [System. Management. Automation. Provider. cmdletprovider. ShouldContinue](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) permite uma verificação adicional de modificações potencialmente perigosas do sistema.

## <a name="retrieving-dynamic-parameters-for-setitem"></a>Recuperando parâmetros dinâmicos para SetItem

Às vezes, o `Set-Item` cmdlet requer parâmetros adicionais que são especificados dinamicamente no tempo de execução. Para fornecer esses parâmetros dinâmicos, o provedor de item do Windows PowerShell deve implementar o método [System. Management. Automation. Provider. docmdletprovider. Setitemdynamicparameters *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItemDynamicParameters) . Esse método recupera os parâmetros dinâmicos para o item no caminho indicado e retorna um objeto que tem propriedades e campos com atributos de análise semelhantes a uma classe de cmdlet ou um objeto [System. Management. Automation. Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) . O tempo de execução do Windows PowerShell usa o objeto retornado para adicionar os parâmetros ao `Set-Item` cmdlet.

Este provedor não implementa esse método. No entanto, o código a seguir é a implementação padrão desse método.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidersetitemdynamicparameters](Msh_samplestestcmdlets#testprovidersetitemdynamicparameters)]  -->

## <a name="clearing-an-item"></a>Limpando um item

Para limpar um item, o provedor de item do Windows PowerShell implementa o método [System. Management. Automation. Provider. createcmdletprovider. ClearItem *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ClearItem) para dar suporte a chamadas do `Clear-Item` cmdlet. Esse método apaga o item de dados no caminho especificado.

Este provedor não implementa esse método. No entanto, o código a seguir é a implementação padrão desse método.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testproviderclearitem](Msh_samplestestcmdlets#testproviderclearitem)]  -->

#### <a name="things-to-remember-about-implementing-clearitem"></a>Coisas a serem lembradas sobre a implementação de ClearItem

As condições a seguir podem se aplicar a uma implementação de [System. Management. Automation. Provider. @ cmdletprovider. ClearItem *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ClearItem):

- Ao definir a classe do provedor, um provedor de item do Windows PowerShell pode declarar os recursos do provedor de ExpandWildcards, filtrar, incluir ou excluir da enumeração [System. Management. Automation. Provider. Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) . Nesses casos, a implementação de [System. Management. Automation. Provider. @ cmdletprovider. ClearItem *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ClearItem) deve garantir que o caminho passado para o método atenda a esses requisitos. Para fazer isso, o método deve acessar a propriedade apropriada, por exemplo, as propriedades [System. Management. Automation. Provider. cmdletprovider. Exclude *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) e [System. Management. Automation. Provider. cmdletprovider. include *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) .

- Por padrão, as substituições desse método não devem definir ou gravar objetos ocultos do usuário, a menos que a propriedade [System. Management. Automation. Provider. cmdletprovider. Force *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) seja definida como `true` . Um erro deve ser enviado para o método [System. Management. Automation. Provider. cmdletprovider. WriteError](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteError) se o caminho representar um item que está oculto do usuário e [System. Management. Automation. Provider. cmdletprovider. Force *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) é definido como `false` .

- Sua implementação do método [System. Management. Automation. Provider. docmdletprovider. SetItem *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) deve chamar [System. Management. Automation. Provider. cmdletprovider. ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) e verificar seu valor de retorno antes de fazer qualquer alteração no armazenamento de dados. Esse método é usado para confirmar a execução de uma operação quando uma alteração é feita no armazenamento de dados, por exemplo, excluindo arquivos. O método [System. Management. Automation. Provider. cmdletprovider. ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) envia o nome do recurso a ser alterado para o usuário, com o tempo de execução do Windows PowerShell e manipula quaisquer configurações de linha de comando ou variáveis de preferência para determinar o que deve ser exibido.

  Após a chamada para [System. Management. Automation. Provider. cmdletprovider. ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) retornar `true` , o método [System. Management. Automation. Provider. docmdletprovider. SetItem *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) deverá chamar o método [System. Management. Automation. Provider. cmdletprovider. ShouldContinue](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) . Esse método envia uma mensagem ao usuário para permitir que os comentários verifiquem se a operação deve continuar. A chamada para [System. Management. Automation. Provider. cmdletprovider. ShouldContinue](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) permite uma verificação adicional de modificações potencialmente perigosas do sistema.

## <a name="retrieve-dynamic-parameters-for-clearitem"></a>Recuperar parâmetros dinâmicos para ClearItem

Às vezes, o `Clear-Item` cmdlet requer parâmetros adicionais que são especificados dinamicamente no tempo de execução. Para fornecer esses parâmetros dinâmicos, o provedor de item do Windows PowerShell deve implementar o método [System. Management. Automation. Provider. docmdletprovider. Clearitemdynamicparameters *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ClearItemDynamicParameters) . Esse método recupera os parâmetros dinâmicos para o item no caminho indicado e retorna um objeto que tem propriedades e campos com atributos de análise semelhantes a uma classe de cmdlet ou um objeto [System. Management. Automation. Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) . O tempo de execução do Windows PowerShell usa o objeto retornado para adicionar os parâmetros ao `Clear-Item` cmdlet.

Este provedor de item não implementa esse método. No entanto, o código a seguir é a implementação padrão desse método.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testproviderclearitemdynamicparameters](Msh_samplestestcmdlets#testproviderclearitemdynamicparameters)]  -->

## <a name="performing-a-default-action-for-an-item"></a>Executando uma ação padrão para um item

Um provedor de item do Windows PowerShell pode implementar o método [System. Management. Automation. Provider. createcmdletprovider. Invokedefaultaction *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.InvokeDefaultAction) para dar suporte a chamadas do `Invoke-Item` cmdlet, o que permite que o provedor execute uma ação padrão para o item no caminho especificado. Por exemplo, o provedor FileSystem pode usar esse método para chamar ShellExecute para um item específico.

Este provedor não implementa esse método. No entanto, o código a seguir é a implementação padrão desse método.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testproviderinvokedefaultaction](Msh_samplestestcmdlets#testproviderinvokedefaultaction)]  -->

#### <a name="things-to-remember-about-implementing-invokedefaultaction"></a>Coisas a serem lembradas sobre a implementação de InvokeDefaultAction

As condições a seguir podem se aplicar a uma implementação de [System. Management. Automation. Provider. @ cmdletprovider. Invokedefaultaction *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.InvokeDefaultAction):

- Ao definir a classe do provedor, um provedor de item do Windows PowerShell pode declarar os recursos do provedor de ExpandWildcards, filtrar, incluir ou excluir da enumeração [System. Management. Automation. Provider. Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) . Nesses casos, a implementação de [System. Management. Automation. Provider. @ cmdletprovider. Invokedefaultaction *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.InvokeDefaultAction) deve garantir que o caminho passado para o método atenda a esses requisitos. Para fazer isso, o método deve acessar a propriedade apropriada, por exemplo, as propriedades [System. Management. Automation. Provider. cmdletprovider. Exclude *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) e [System. Management. Automation. Provider. cmdletprovider. include *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) .

- Por padrão, as substituições desse método não devem definir ou gravar objetos ocultos do usuário, a menos que a propriedade [System. Management. Automation. Provider. cmdletprovider. Force *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) seja definida como `true` . Um erro deve ser enviado para o método [System. Management. Automation. Provider. cmdletprovider. WriteError](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteError) se o caminho representar um item que está oculto do usuário e [System. Management. Automation. Provider. cmdletprovider. Force *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) é definido como `false` .

## <a name="retrieve-dynamic-parameters-for-invokedefaultaction"></a>Recuperar parâmetros dinâmicos para InvokeDefaultAction

Às vezes, o `Invoke-Item` cmdlet requer parâmetros adicionais que são especificados dinamicamente no tempo de execução. Para fornecer esses parâmetros dinâmicos, o provedor de item do Windows PowerShell deve implementar o método [System. Management. Automation. Provider. docmdletprovider. Invokedefaultactiondynamicparameters *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.InvokeDefaultActionDynamicParameters) . Esse método recupera os parâmetros dinâmicos para o item no caminho indicado e retorna um objeto que tem propriedades e campos com atributos de análise semelhantes a uma classe de cmdlet ou um objeto [System. Management. Automation. Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) . O tempo de execução do Windows PowerShell usa o objeto retornado para adicionar os parâmetros dinâmicos ao `Invoke-Item` cmdlet.

Este provedor de item não implementa esse método. No entanto, o código a seguir é a implementação padrão desse método.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testproviderinvokedefaultactiondynamicparameters](Msh_samplestestcmdlets#testproviderinvokedefaultactiondynamicparameters)]  -->

## <a name="implementing-helper-methods-and-classes"></a>Implementando métodos e classes auxiliares

Este provedor de item implementa vários métodos auxiliares e classes que são usadas pelos métodos de substituição públicos definidos pelo Windows PowerShell. O código para esses métodos e classes auxiliares são mostrados na seção de [exemplo de código](#code-sample) .

### <a name="normalizepath-method"></a>Método NormalizePath

Este provedor de item implementa um método auxiliar NormalizePath para garantir que o caminho tenha um formato consistente. O formato especificado usa uma barra invertida ( \\ ) como um separador.

### <a name="pathisdrive-method"></a>Método PathIsDrive

Esse provedor de item implementa um método auxiliar PathIsDrive para determinar se o caminho especificado é, na verdade, o nome da unidade.

### <a name="chunkpath-method"></a>Método ChunkPath

Esse provedor de item implementa um método auxiliar ChunkPath que divide o caminho especificado para que o provedor possa identificar seus elementos individuais. Ele retorna uma matriz composta pelos elementos Path.

### <a name="gettable-method"></a>Método GetTable

Esse provedor de item implementa o método auxiliar gettablenames que retorna um objeto DatabaseTableInfo que representa informações sobre a tabela especificada na chamada.

### <a name="getrow-method"></a>Método GetRow

O método [System. Management. Automation. Provider. createcmdletprovider. GetItem *](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) desse provedor de item chama o método auxiliar GetRows. Esse método auxiliar recupera um objeto DatabaseRowInfo que representa informações sobre a linha especificada na tabela.

### <a name="databasetableinfo-class"></a>Classe DatabaseTableInfo

Este provedor de item define uma classe DatabaseTableInfo que representa uma coleção de informações em uma tabela de dados no banco de dado. Essa classe é semelhante à classe [System. IO. DirectoryInfo](/dotnet/api/System.IO.DirectoryInfo) .

O provedor de item de exemplo define um método DatabaseTableInfo. getTableName que retorna uma coleção de objetos de informações de tabela que definem as tabelas no banco de dados. Esse método inclui um bloco try/catch para garantir que qualquer erro de banco de dados seja exibido como uma linha com zero entradas.

### <a name="databaserowinfo-class"></a>Classe DatabaseRowInfo

Este provedor de item define a classe auxiliar DatabaseRowInfo que representa uma linha em uma tabela do banco de dados. Essa classe é semelhante à classe [System. IO. FileInfo](/dotnet/api/System.IO.FileInfo) .

O provedor de exemplo define um método DatabaseRowInfo. GetRows para retornar uma coleção de objetos de informações de linha para a tabela especificada. Esse método inclui um bloco try/catch para interceptar exceções. Quaisquer erros resultarão em nenhuma informação de linha.

## <a name="code-sample"></a>Exemplo de código

Para obter o código de exemplo completo, consulte [exemplo de código AccessDbProviderSample03](./accessdbprovidersample03-code-sample.md).

## <a name="defining-object-types-and-formatting"></a>Definindo tipos de objeto e formatação

Ao escrever um provedor, pode ser necessário adicionar membros a objetos existentes ou definir novos objetos. Quando terminar, crie um arquivo de tipos que o Windows PowerShell pode usar para identificar os membros do objeto e um arquivo de formato que define como o objeto é exibido. Para obter mais informações sobre o, consulte [estendendo tipos de objeto e formatação](/previous-versions/ms714665(v=vs.85)).

## <a name="building-the-windows-powershell-provider"></a>Criando o provedor do Windows PowerShell

Consulte [como registrar cmdlets, provedores e aplicativos de host](/previous-versions/ms714644(v=vs.85)).

## <a name="testing-the-windows-powershell-provider"></a>Testando o provedor do Windows PowerShell

Quando este provedor de itens do Windows PowerShell é registrado com o Windows PowerShell, você só pode testar a funcionalidade básica e de unidade do provedor. Para testar a manipulação de itens, você também deve implementar a funcionalidade de contêiner descrita em [implementando um provedor de contêiner do Windows PowerShell](./creating-a-windows-powershell-container-provider.md).

## <a name="see-also"></a>Consulte Também

[SDK do Windows PowerShell](../windows-powershell-reference.md)

[Guia do programador do Windows PowerShell](./windows-powershell-programmer-s-guide.md)

[Criando provedores do Windows PowerShell](./how-to-create-a-windows-powershell-provider.md)

[Criando seu provedor do Windows PowerShell](./designing-your-windows-powershell-provider.md)

[Estendendo tipos de objeto e formatação](/previous-versions/ms714665(v=vs.85))

[Como funciona o Windows PowerShell](/previous-versions/ms714658(v=vs.85))

[Criando um provedor de contêiner do Windows PowerShell](./creating-a-windows-powershell-container-provider.md)

[Criando um provedor de unidade do Windows PowerShell](./creating-a-windows-powershell-drive-provider.md)

[Como registrar cmdlets, provedores e aplicativos host](/previous-versions/ms714644(v=vs.85))
