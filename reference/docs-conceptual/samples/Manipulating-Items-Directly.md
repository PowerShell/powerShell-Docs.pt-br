---
ms.date: 06/05/2017
keywords: powershell, cmdlet
title: Manipulando itens diretamente
description: O PowerShell fornece vários cmdlets que ajudam a gerenciar itens em computadores locais e remotos. Os itens são objetos expostos por provedores do PowerShell, como o sistema de arquivos, o Registro, os certificados e outros.
ms.openlocfilehash: 20132b63a8ff4ef24b1d8346066315dbb053e59c
ms.sourcegitcommit: 9080316e3ca4f11d83067b41351531672b667b7a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/24/2020
ms.locfileid: "92500310"
---
# <a name="manipulating-items-directly"></a>Manipulando itens diretamente

Os elementos exibidos em unidades do Windows PowerShell, como os arquivos e pastas em unidades de sistema de arquivos e as chaves do registro nas unidades do registro do Windows PowerShell, são chamados de *itens* no Windows PowerShell. Os cmdlets para trabalhar com eles item possuem o substantivo **Item** em seus nomes.

O resultado do comando **Get-Command -Noun Item** mostra que existem nove cmdlets de itens do Windows PowerShell.

```
PS> Get-Command -Noun Item

CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Clear-Item                      Clear-Item [-Path] <String[]...
Cmdlet          Copy-Item                       Copy-Item [-Path] <String[]>...
Cmdlet          Get-Item                        Get-Item [-Path] <String[]> ...
Cmdlet          Invoke-Item                     Invoke-Item [-Path] <String[...
Cmdlet          Move-Item                       Move-Item [-Path] <String[]>...
Cmdlet          New-Item                        New-Item [-Path] <String[]> ...
Cmdlet          Remove-Item                     Remove-Item [-Path] <String[...
Cmdlet          Rename-Item                     Rename-Item [-Path] <String>...
Cmdlet          Set-Item                        Set-Item [-Path] <String[]> ...
```

## <a name="creating-new-items-new-item"></a>Criando novos itens (New-Item)

Para criar um novo item no sistema de arquivos, use o cmdlet **New-Item** . Inclua o parâmetro **Path** com o caminho para o item e o parâmetro **ItemType** com um valor de "file" ou "directory".

Por exemplo, para criar um novo diretório chamado “New.Directory” no diretório C:\\Temp, digite:

```
PS> New-Item -Path c:\temp\New.Directory -ItemType Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  11:29 AM            New.Directory
```

Para criar um arquivo, altere o valor do parâmetro **ItemType** para "file". Por exemplo, para criar um arquivo chamado "file1.txt" no diretório New.Directory, digite:

```
PS> New-Item -Path C:\temp\New.Directory\file1.txt -ItemType file

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

Você pode usar a mesma técnica para criar uma nova chave do registro. Na verdade, uma chave do registro é mais fácil de criar porque o único tipo de item no registro do Windows é uma chave. (Entradas do Registro são *propriedades* do item.) Por exemplo, para criar uma chave chamada "_Test" na subchave CurrentVersion, digite:

```
PS> New-Item -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion_Test

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion

SKC  VC Name                           Property
---  -- ----                           --------
  0   0 _Test                          {}
```

Ao digitar um caminho do registro, certifique-se de incluir os dois-pontos ( **:** ) nos nomes de unidades do Windows PowerShell, HKLM: e HKCU:. Sem os dois pontos, o Windows PowerShell não reconhece o nome de unidade no caminho.

## <a name="why-registry-values-are-not-items"></a>Por que os valores do registro não são itens

Ao usar o cmdlet **Get-ChildItem** para localizar os itens em uma chave do registro, você nunca verá entradas reais do registro ou seus valores.

Por exemplo, a chave do Registro **HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Run** geralmente contém várias entradas do Registro que representam aplicativos executados quando o sistema é iniciado.

No entanto, ao usar **Get-ChildItem** para procurar itens filhos na chave, tudo o que você verá é a subchave **OptionalComponents** da chave:

```
PS> Get-ChildItem HKLM:\Software\Microsoft\Windows\CurrentVersion\Run

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\Micros
oft\Windows\CurrentVersion\Run
SKC  VC Name                           Property
---  -- ----                           --------
  3   0 OptionalComponents             {}
```

Embora seria algo conveniente tratar as entradas do registro como itens, não é possível você especificar um caminho para uma entrada de registro de uma maneira que garanta que ele seja exclusivo. A notação de caminho não faz distinção entre a subchave do Registro chamada **Run** e a entrada do Registro **(Default)** na subchave **Run** . Além disso, como nomes de entrada do Registro podem conter o caractere de barra invertida ( **\\** ), se as entradas de Registro fossem itens, você não poderia usar a notação de caminho para distinguir uma entrada do Registro denominada **Windows\\CurrentVersion\\Run** da subchave localizada nesse caminho.

## <a name="renaming-existing-items-rename-item"></a>Renomeando itens existentes (Rename-Item)

Para alterar o nome de uma configuração de sessão, use o cmdlet **Rename-Item** . O comando a seguir altera o nome do arquivo **file1.txt** para **fileOne.txt** .

```powershell
Rename-Item -Path C:\temp\New.Directory\file1.txt fileOne.txt
```

O cmdlet **Rename-Item** pode alterar o nome de um arquivo ou uma pasta, mas não pode mover um item. O comando a seguir falhará porque ele tenta mover o arquivo da pasta New.Directory para o diretório Temp.

```
PS> Rename-Item -Path C:\temp\New.Directory\fileOne.txt c:\temp\fileOne.txt
Rename-Item : Cannot rename because the target specified is not a path.
At line:1 char:12
+ Rename-Item  <<<< -Path C:\temp\New.Directory\fileOne c:\temp\fileOne.txt
```

## <a name="moving-items-move-item"></a>Movendo itens (Move Item)

Para mover um arquivo ou pasta, use o cmdlet **Move-Item** .

Por exemplo, o comando a seguir move o diretório New.Directory do diretório C:\\temp para a raiz da unidade C:. Para confirmar que o item foi movido, inclua o parâmetro **PassThru** do cmdlet **Move-Item** . Sem o **Passthru** , o cmdlet **Move-Item** não exibirá nenhum resultado.

```
PS> Move-Item -Path C:\temp\New.Directory -Destination C:\ -PassThru

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  12:14 PM            New.Directory
```

## <a name="copying-items-copy-item"></a>Copiando itens (Copy-Item)

Se você estiver familiarizado com as operações de cópia em outros shells, poderá achar o comportamento do cmdlet **Copy-Item** do Windows PowerShell um tanto incomum. Quando você copia um item de um local para outro, o Copy-Item não copia o conteúdo por padrão.

Por exemplo, se você copiar o diretório **New.Directory** da unidade C: para o diretório C:\\temp, o comando será executado com êxito, mas os arquivos no diretório New.Directory não serão copiados.

```powershell
Copy-Item -Path C:\New.Directory -Destination C:\temp
```

Se você exibir o conteúdo do **C:\\temp\\New.Directory** , verá que ele não contém nenhum arquivo:

```
PS> Get-ChildItem -Path C:\temp\New.Directory
PS>
```

Por que o cmdlet **Copy-Item** não copia o conteúdo para um novo local?

O cmdlet **Copy-Item** foi projetado para ser genérico, não apenas para copiar arquivos e pastas. Além disso, mesmo ao copiar arquivos e pastas, convém copiar apenas o contêiner e não os itens dentro dela.

Para copiar todo o conteúdo de uma pasta, inclua o parâmetro **Recurse** do cmdlet **Copy-Item** no comando. Se você já copiou o diretório sem o seu conteúdo, adicione o parâmetro **Force** , que permite substituir a pasta vazia.

```
PS> Copy-Item -Path C:\New.Directory -Destination C:\temp -Recurse -Force -Passthru

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18   1:53 PM            New.Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

## <a name="deleting-items-remove-item"></a>Excluindo itens (Remove-Item)

Para excluir arquivos ou pastas, use o cmdlet **Remove-Item** . Cmdlets do Windows PowerShell, como o **Remove-Item** , que podem executar alterações significativas e irreversíveis, geralmente solicitarão confirmação quando você inserir seus comandos. Por exemplo, se você tentar remover a pasta **New.Directory** , será solicitado a confirmar o comando, pois a pasta contém arquivos:

```
PS> Remove-Item C:\New.Directory

Confirm
The item at C:\temp\New.Directory has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
 sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

Como **Sim** é a resposta padrão, para excluir a pasta e seus arquivos, pressione a tecla **Enter** . Para remover a pasta sem confirmar, use o parâmetro **-Recurse** .

```powershell
Remove-Item C:\temp\New.Directory -Recurse
```

## <a name="executing-items-invoke-item"></a>Executando itens (Invoke-Item)

O Windows PowerShell usa o cmdlet **Invoke-Item** para executar uma ação padrão para um arquivo ou pasta. Essa ação padrão é determinada pelo manipulador de aplicativo padrão no registro. O efeito é o mesmo que clicar duas vezes o item no Explorador de arquivos.

Por exemplo, suponha que você execute o seguinte comando:

```powershell
Invoke-Item C:\WINDOWS
```

Aparece uma janela do Explorer localizada em C:\\Windows, como se você tivesse clicado duas vezes na pasta C:\\Windows.

Se você chamar o arquivo **Boot.ini** em um sistema anterior ao Windows Vista:

```powershell
Invoke-Item C:\boot.ini
```

Se o tipo de arquivo .ini estiver associado ao Bloco de Notas, o arquivo Boot.ini é aberto nele.
