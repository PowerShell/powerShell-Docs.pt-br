---
ms.date: 09/13/2016
ms.topic: reference
title: Suporte à ajuda online
description: Suporte à ajuda online
ms.openlocfilehash: 0164b5e6c6c8d66a6ab2467a8adfb7efffe0fe17
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92645428"
---
# <a name="supporting-online-help"></a>Suporte à ajuda online

A partir do PowerShell 3,0, há duas maneiras de dar suporte ao `Get-Help` recurso online para comandos do PowerShell. Este tópico explica como implementar esse recurso para diferentes tipos de comando.

## <a name="about-online-help"></a>Sobre a ajuda online

A ajuda online sempre foi uma parte vital do PowerShell. Embora o `Get-Help` cmdlet exiba tópicos de ajuda no prompt de comando, muitos usuários preferem a experiência de leitura online, incluindo codificação por cores, hiperlinks e compartilhamento de ideias em conteúdo da Comunidade e documentos baseados em wiki. O mais importante é que, antes do advento da ajuda atualizável, a ajuda online forneceu a versão mais atualizada dos arquivos de ajuda.

Com o advento da ajuda atualizável no PowerShell 3,0, a ajuda online ainda exerce uma função vital. Além da experiência do usuário flexível, a ajuda online fornece ajuda aos usuários que não ou que não podem usar a ajuda atualizável para baixar tópicos da ajuda.

## <a name="how-get-help--online-works"></a>Como o Get-Help-online funciona

Para ajudar os usuários a encontrar os tópicos da ajuda online para comandos, o `Get-Help` comando tem um parâmetro online que abre a versão online do tópico da ajuda para um comando no navegador de Internet padrão do usuário.

Por exemplo, o comando a seguir abre o tópico da ajuda online para o `Invoke-Command` cmdlet.

```powershell
Get-Help Invoke-Command -Online
```

Para implementar `Get-Help -Online` , o `Get-Help` cmdlet procura um Uniform Resource Identifier (URI) para o tópico de ajuda da versão online nos locais a seguir.

- O primeiro link na seção **links relacionados** do tópico da ajuda para o comando. O tópico da ajuda deve ser instalado no computador do usuário. Esse recurso foi introduzido no PowerShell 2,0.

- A propriedade **HelpUri** de qualquer comando. A propriedade **HelpUri** é acessível mesmo quando o tópico da ajuda do comando não está instalado no computador do usuário. Esse recurso foi introduzido no PowerShell 3,0.

  `Get-Help` procura um URI na primeira entrada da seção **links relacionados** antes de obter o valor da propriedade **HelpUri** . Se o valor da propriedade estiver incorreto ou alterado, você poderá substituí-lo inserindo um valor diferente no primeiro link relacionado. No entanto, o primeiro link relacionado funciona somente quando os tópicos da ajuda são instalados no computador do usuário.

## <a name="adding-a-uri-to-the-first-related-link-of-a-command-help-topic"></a>Adicionando um URI ao primeiro link relacionado de um tópico de ajuda de comando

Você pode dar suporte a `Get-Help -Online` qualquer comando, adicionando um URI válido à primeira entrada na seção **links relacionados** do tópico da ajuda baseada em XML para o comando. Essa opção só é válida em tópicos de ajuda baseados em XML e funciona somente quando o tópico da ajuda está instalado no computador do usuário. Quando o tópico da ajuda é instalado e o URI é populado, esse valor tem precedência sobre a propriedade **HelpUri** do comando.

Para dar suporte a esse recurso, o URI deve aparecer no `maml:uri` elemento sob o primeiro `maml:relatedLinks/maml:navigationLink` elemento no `maml:relatedLinks` elemento.

O XML a seguir mostra o posicionamento correto do URI. O `Online version:` texto no `maml:linkText` elemento é uma prática recomendada, mas não é necessário.

```xml
<maml:relatedLinks>
    <maml:navigationLink>
        <maml:linkText>Online version:</maml:linkText>
        <maml:uri>https://go.microsoft.com/fwlink/?LinkID=113279</maml:uri>
    </maml:navigationLink>
    <maml:navigationLink>
        <maml:linkText>about_History</maml:linkText>
        <maml:uri/>
    </maml:navigationLink>
</maml:relatedLinks>
```

## <a name="adding-the-helpuri-property-to-a-command"></a>Adicionando a propriedade HelpUri a um comando

Esta seção mostra como adicionar a propriedade HelpUri a comandos de tipos diferentes.

### <a name="adding-a-helpuri-property-to-a-cmdlet"></a>Adicionando uma propriedade HelpUri a um cmdlet

Para os cmdlets escritos em C#, adicione um atributo **HelpUri** à classe **cmdlet** . O valor do atributo deve ser um URI que começa com `http` ou `https` .

O código a seguir mostra o atributo **HelpUri** da `Get-History` classe cmdlet.

```csharp
[Cmdlet(VerbsCommon.Get, "History", HelpUri = "https://go.microsoft.com/fwlink/?LinkID=001122")]
```

### <a name="adding-a-helpuri-property-to-an-advanced-function"></a>Adicionando uma propriedade HelpUri a uma função avançada

Para funções avançadas, adicione uma propriedade **HelpUri** ao atributo **CmdletBinding** . O valor da propriedade deve ser um URI que comece com "http" ou "https".

O código a seguir mostra o atributo **HelpUri** da `New-Calendar` função

```powershell
function New-Calendar {
    [CmdletBinding(SupportsShouldProcess=$true,
    HelpURI="https://go.microsoft.com/fwlink/?LinkID=01122")]
```

### <a name="adding-a-helpuri-attribute-to-a-cim-command"></a>Adicionando um atributo HelpUri a um comando CIM

Para comandos CIM, adicione um atributo **HelpUri** ao elemento **CMDLETMETADATA** no arquivo CDXML.
O valor do atributo deve ser um URI que começa com `http` ou `https` .

O código a seguir mostra o atributo HelpUri do `Start-Debug` comando CIM

```xml
<CmdletMetadata Verb="Debug" HelpUri="https://go.microsoft.com/fwlink/?LinkID=001122"/>
```

### <a name="adding-a-helpuri-attribute-to-a-workflow"></a>Adicionando um atributo HelpUri a um fluxo de trabalho

Para fluxos de trabalho que são gravados na linguagem do PowerShell, adicione um **. ExternalHelp** a diretiva de comentário para o código do fluxo de trabalho. O valor da diretiva deve ser um URI que começa com `http` ou `https` .

> [!NOTE]
> A propriedade HelpUri não tem suporte para fluxos de trabalho baseados em XAML no PowerShell.

O código a seguir mostra o. Diretiva ExternalHelp em um arquivo de fluxo de trabalho.

```powershell
# .ExternalHelp "https://go.microsoft.com/fwlink/?LinkID=138338"
```
