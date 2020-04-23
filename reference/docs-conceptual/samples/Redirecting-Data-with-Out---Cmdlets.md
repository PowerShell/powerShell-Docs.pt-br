---
ms.date: 06/05/2017
keywords: powershell, cmdlet
title: Redirecionamento de dados com cmdlets Out
ms.openlocfilehash: d4cc14e26bdef0f973f948177d0c1e68929605fa
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2020
ms.locfileid: "67030084"
---
# <a name="redirecting-data-with-out--cmdlets"></a>Redirecionamento de dados com cmdlets Out-*

O Windows PowerShell oferece vários cmdlets que permitem controlar os dados de saída diretamente. Esses cmdlets compartilham duas importantes características.

Primeiramente, eles geralmente transformam dados em alguma forma de texto. Eles fazem isso porque geram saída de dados para os componentes do sistema que exigem entrada de texto. Isso significa que eles precisam para representar os objetos como texto. Portanto, o texto é formatado como visto na janela do console do Windows PowerShell.

Em segundo lugar, esses cmdlets usam o verbo do Windows PowerShell **Out** porque eles enviam informações do Windows PowerShell para outro lugar. O cmdlet **Out-Host** não é uma exceção: a exibição da janela do host está fora do Windows PowerShell. Isso é importante porque, quando os dados são enviados do Windows PowerShell, eles realmente são removidos. Você poderá ver isso se tentar criar um pipeline de dados que realiza a paginação de dados para a janela do host e, em seguida, tentar formatá-los como uma lista, conforme mostrado aqui:

```powershell
Get-Process | Out-Host -Paging | Format-List
```

Você pode esperar que o comando exiba páginas de informações do processo em formato de lista. Em vez disso, ele exibe a lista tabular padrão:

```output
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    101       5     1076       3316    32     0.05   2888 alg
...
    618      18    39348      51108   143   211.20    740 explorer
    257       8     9752      16828    79     3.02   2560 explorer
...
<SPACE> next page; <CR> next line; Q quit
...
```

O cmdlet **Out-Host** envia os dados diretamente para o console, por isso o comando **Format-List** nunca recebe nada para formatar.

A maneira correta de estruturar esse comando é colocar o cmdlet **Out-Host** no final do pipeline, conforme mostrado abaixo. Isso faz com que os dados do processo sejam formatados em uma lista antes de serem paginados e exibidos.

```
PS> Get-Process | Format-List | Out-Host -Paging

Id      : 2888
Handles : 101
CPU     : 0.046875
Name    : alg
...

Id      : 740
Handles : 612
CPU     : 211.703125
Name    : explorer

Id      : 2560
Handles : 257
CPU     : 3.015625
Name    : explorer
...
<SPACE> next page; <CR> next line; Q quit
...
```

Isso se aplica a todos os cmdlets **Out**. Um cmdlet **Out** sempre deve aparecer no final do pipeline.

> [!NOTE]
> Todos os cmdlets **Out** renderizam a saída como texto, usando a formatação em vigor para a janela de console, incluindo os limites de tamanho da linha.

## <a name="paging-console-output-out-host"></a>Paginando a saída do console (Out-Host)

Por padrão, o Windows PowerShell envia dados para a janela do host, que é exatamente o que o cmdlet Out-Host faz. O principal uso do cmdlet Out-Host é paginar os dados conforme abordado anteriormente. Por exemplo, o comando a seguir usa Out-Host para paginar a saída do cmdlet Get-Command:

```powershell
Get-Command | Out-Host -Paging
```

Você também pode usar a função **more** para paginar os dados. No Windows PowerShell, **more** é uma função que chama **Out-Host -Paging**. O comando a seguir demonstra como usar a função **more** para paginar a saída de Get-Command:

```powershell
Get-Command | more
```

Se você incluir um ou mais nomes de arquivo como argumentos para a função more, ela lerá os arquivos especificados e paginará o conteúdo para o host:

```
PS> more c:\boot.ini
[boot loader]
timeout=5
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
...
```

## <a name="discarding-output-out-null"></a>Descartando a saída (Out-Null)

O cmdlet **Out-Null** é projetado para descartar imediatamente qualquer entrada que receber. Isso é útil para descartar dados desnecessários obtidos como efeito colateral da execução de um comando. Ao digitar o comando a seguir, você não receberá nenhuma saída dele:

```powershell
Get-Command | Out-Null
```

O cmdlet **Out-Null** não descarta a saída de erro. Por exemplo, se você digitar o comando a seguir, uma mensagem será exibida informando que o Windows PowerShell não reconhece 'Is -NotACommand':

```
PS> Get-Command Is-NotACommand | Out-Null
Get-Command : 'Is-NotACommand' is not recognized as a cmdlet, function, operabl
e program, or script file.
At line:1 char:12
+ Get-Command  <<<< Is-NotACommand | Out-Null
```

## <a name="printing-data-out-printer"></a>Imprimindo dados (Out-Printer)

Você pode imprimir dados usando o cmdlet **Out-Printer**. O cmdlet **Out-Printer** usará sua impressora padrão se você não fornecer um nome de impressora. Você pode usar qualquer impressora baseada em Windows especificando seu nome de exibição. Não é necessário nenhum tipo de mapeamento de porta de impressora nem mesmo uma impressora física real. Por exemplo, se você tiver as ferramentas de geração de imagens de documento do Microsoft Office instaladas, poderá enviar os dados para um arquivo de imagem digitando:

```powershell
Get-Command Get-Command | Out-Printer -Name 'Microsoft Office Document Image Writer'
```

## <a name="saving-data-out-file"></a>Salvando dados (Out-File)

Você pode enviar a saída para um arquivo em vez da janela de console usando o cmdlet **Out-File**. A linha de comando a seguir envia uma lista de processos para o arquivo **C:\\temp\\processlist.txt**:

```powershell
Get-Process | Out-File -FilePath C:\temp\processlist.txt
```

Os resultados do uso do cmdlet **Out-File** poderão não ser o esperado se você estiver acostumado com o redirecionamento de saída tradicional. Para entender seu comportamento, você deve estar ciente do contexto no qual o cmdlet **Out-File** opera.

Por padrão, o cmdlet **Out-File** cria um arquivo Unicode. Esse é o melhor padrão a longo prazo, porém significa que ferramentas que esperam arquivos ASCII não funcionarão corretamente com o formato de saída padrão. Você pode alterar o formato de saída padrão para ASCII usando o parâmetro **Encoding**:

```powershell
Get-Process | Out-File -FilePath C:\temp\processlist.txt -Encoding ASCII
```

**Out-File** formata o conteúdo do arquivo para se parecer com a saída do console. Isso faz com que a saída seja truncada da mesma forma que na janela do console na maioria das circunstâncias. Por exemplo, se você executar o seguinte comando:

```powershell
Get-Command | Out-File -FilePath c:\temp\output.txt
```

A saída se parecerá com esta:

```output
CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Add-Content                     Add-Content [-Path] <String[...
Cmdlet          Add-History                     Add-History [[-InputObject] ...
...
```

Para obter uma saída que não força quebras de linha para corresponder à largura da tela, você pode usar o parâmetro **Width** para especificar a largura da linha. Como a **Width** é um parâmetro de número inteiro de 32 bits, o valor máximo que ele pode ter é 2147483647. Digite o seguinte para definir a largura da linha para esse valor máximo:

```powershell
Get-Command | Out-File -FilePath c:\temp\output.txt -Width 2147483647
```

O cmdlet **Out-File** é mais útil quando você deseja salvar a saída da mesma forma que ela seria exibida no console. Para ter maior controle sobre o formato de saída, você precisa de ferramentas mais avançadas. Elas serão abordadas no próximo capítulo, juntamente com alguns detalhes sobre a manipulação de objetos.
