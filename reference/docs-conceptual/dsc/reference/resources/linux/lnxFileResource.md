---
ms.date: 07/17/2020
keywords: DSC,powershell,configuração,instalação
title: Recurso nxFile de DSC para Linux
ms.openlocfilehash: 37de70fedce77161c97084d5ca7eaf8e1bce45d8
ms.sourcegitcommit: 41e1acbd9ce0f49a23c6eb99facd2c280d836836
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2020
ms.locfileid: "86463917"
---
# <a name="dsc-for-linux-nxfile-resource"></a>Recurso nxFile de DSC para Linux

O recurso **nxFile** na Configuração de Estado Desejado (DSC) do PowerShell fornece um mecanismo para gerenciar arquivos e diretórios em um nó do Linux.

## <a name="syntax"></a>Sintaxe

```Syntax
nxFile <string> #ResourceName
{
    DestinationPath = <string>
    [ SourcePath = <string> ]
    [ Type = <string> { directory | file | link } ]
    [ Contents = <string> ]
    [ Checksum = <string> { ctime | mtime | md5 }  ]
    [ Recurse = <bool> ]
    [ Force = <bool> ]
    [ Links = <string> { follow | manage | ignore } ]
    [ Group = <string> ]
    [ Mode = <string> ]
    [ Owner = <string> ]
    [ DependsOn = <string[]> ]
    [ Ensure = <string> { Absent | Present }  ]
}
```

## <a name="properties"></a>Propriedades

|Propriedade |DESCRIÇÃO |
|---|---|
|DestinationPath |Especifica o local onde você deseja garantir o estado de um arquivo ou diretório. |
|SourcePath |Especifica o caminho do qual o recurso de arquivo ou pasta deve ser copiado. Esse caminho poderá ser um caminho local ou uma URL `http/https/ftp`. As URLs `http/https/ftp` remotas só são compatíveis quando o valor da propriedade **Type** é **file**. |
|Type |Especifica se o recurso que está sendo configurado é um diretório ou um arquivo. Defina essa propriedade como **directory** para indicar que o recurso é um diretório. Defina-a como **file** para indicar que o recurso é um arquivo. O valor padrão é **file**. |
|Conteúdo |Especifica o conteúdo de um arquivo, como uma cadeia de caracteres específica. |
|Checksum (soma de verificação) |Define o tipo que deve ser usado para determinar se dois arquivos são iguais. Se **Checksum** não for especificado, somente o nome de arquivo ou diretório será usado para comparação. Os valores são: **ctime**, **mtime** ou **md5**. |
|Recurse |Indica se subdiretórios são incluídos. Defina essa propriedade como `$true` para indicar que você deseja que subdiretórios sejam incluídos. O padrão é `$false`. Essa propriedade é válida somente quando a propriedade **Type** está definida como **directory**. |
|Force |Determinadas operações de arquivo (como substituição de um arquivo ou exclusão de um diretório que não esteja vazio) resultarão em erro. O uso da propriedade **Force** substitui esses erros. O valor padrão é `$false`. |
|Links |Especifica o comportamento desejado para links simbólicos. Defina essa propriedade como **follow** para seguir links simbólicos e agir sobre o destino de links. Por exemplo, copiar o arquivo em vez do link. Defina essa propriedade como **manage** para agir sobre o link. Por exemplo, copiar o próprio link. Defina essa propriedade como **ignore** para ignorar links simbólicos. |
|Agrupar |O nome do **Grupo** que terá permissões para o arquivo ou diretório. |
|Mode |Especifica as permissões desejadas para o recurso, na notação octal ou simbólica. Por exemplo, **777** ou **rwxrwxrwx**. Se usar notação simbólica, não forneça o primeiro caractere que indica o diretório ou arquivo. |
|Proprietário |O nome do grupo que será proprietário do arquivo ou diretório. |

## <a name="common-properties"></a>Propriedades comuns

|Propriedade |DESCRIÇÃO |
|---|---|
|DependsOn |Indica que a configuração de outro recurso deve ser executada antes de ele ser configurado. Por exemplo, se a ID do bloco de script de configuração do recurso que você deseja executar primeiro for ResourceName e seu tipo for ResourceType, a sintaxe para usar essa propriedade será `DependsOn = "[ResourceType]ResourceName"`. |
|Ensure |Determina se é necessário verificar se o arquivo existe. Defina essa propriedade como **Present** para garantir que o arquivo exista. Defina-a como **Absent** para garantir que o arquivo não exista. O valor padrão é **Present**. |

## <a name="additional-information"></a>Informações adicionais

Linux e Windows usam diferentes caracteres de quebra de linha em arquivos de texto por padrão; isso pode causar resultados inesperados ao configurar alguns arquivos em um computador Linux com **nxFile**. Há várias maneiras de gerenciar o conteúdo de um arquivo do Linux e, ao mesmo tempo, evitar problemas causados por caracteres de quebra de linha inesperada:

1. Copiar o arquivo de uma origem remota (http, https ou ftp)

   Crie um arquivo no Linux com o conteúdo desejado e prepare-o em um servidor da Web ou ftp acessível com os nós que vai configurar. Defina a propriedade **SourcePath** no recurso **nxFile** com a URL da web ou do ftp para o arquivo.

   ```powershell
   Import-DSCResource -Module nx

   Node $Node
   {
      nxFile resolvConf
      {
         SourcePath = "http://10.185.85.11/conf/resolv.conf"
         DestinationPath = "/etc/resolv.conf"
         Mode = "644"
         Type = "file"
      }
   }
   ```

1. Leia o conteúdo do arquivo no script do PowerShell com [Get-Content](https://technet.microsoft.com/library/hh849787.aspx) depois de definir a propriedade **$OFS** para usar o caractere de quebra de linha do Linux.

   ```powershell
   Import-DSCResource -Module nx

   Node $Node
   {
      $OFS = "`n"
      $Contents = Get-Content C:\temp\resolv.conf

      nxFile resolvConf
      {
         DestinationPath = "/etc/resolv.conf"
         Mode = "644"
         Type = "file"
         Contents = "$Contents"
      }
   }
   ```

1. use uma função do PowerShell para substituir as quebras de linha do Windows com caracteres de quebra de linha do Linux.

   ```powershell
   Function LinuxString($inputStr){
      $outputStr = $inputStr.Replace("`r`n","`n")
      $outputStr += "`n"
      Return $outputStr
   }

   Import-DSCResource -Module nx

   Node $Node
   {
      $Contents = @'
   search contoso.com
   domain contoso.com
   nameserver 10.185.85.11
   '@
       $Contents = LinuxString $Contents

      nxFile resolvConf
      {
         DestinationPath = "/etc/resolv.conf"
         Mode = "644"
         Type = "file"
         Contents = $Contents
      }
   }
   ```

## <a name="example"></a>Exemplo

O exemplo a seguir garante que o diretório `/opt/mydir` exista e que um arquivo com conteúdo especificado exista nesse diretório.

```powershell
Import-DSCResource -Module nx

Node $node {
    nxFile DirectoryExample
    {
        Ensure = "Present"
        DestinationPath = "/opt/mydir"
        Type = "Directory"
    }

    nxFile FileExample
    {
        Ensure = "Present"
        Destinationpath = "/opt/mydir/myfile"
        Contents=@"
#!/bin/bash`necho "hello world"`n
"@
        Mode = "755"
        DependsOn = "[nxFile]DirectoryExample"
    }
}
```
