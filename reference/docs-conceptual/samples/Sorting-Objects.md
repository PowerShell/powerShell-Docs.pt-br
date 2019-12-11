---
ms.date: 06/05/2017
keywords: powershell, cmdlet
title: Classificação de objetos
ms.openlocfilehash: ed78e7e333f3468781c9cd96df2194fbdfebe753
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "67030777"
---
# <a name="sorting-objects"></a>Classificação de objetos

É possível organizar os dados exibidos para facilitar a verificação usando o cmdlet `Sort-Object`. `Sort-Object` usa o nome de uma ou mais propriedades para classificar e retorna os dados classificados pelos valores dessas propriedades.

## <a name="basic-sorting"></a>Classificação básica

Pense no problema de listar os subdiretórios e os arquivos no diretório atual.
Se quisermos classificar por **LastWriteTime** e depois por **Nome**, poderemos fazer isso digitando:

```powershell
Get-ChildItem |
  Sort-Object -Property LastWriteTime, Name |
  Format-Table -Property LastWriteTime, Name
```

```output
LastWriteTime          Name
-------------          ----
11/6/2017 10:10:11 AM  .localization-config
11/6/2017 10:10:11 AM  .openpublishing.build.ps1
11/6/2017 10:10:11 AM  appveyor.yml
11/6/2017 10:10:11 AM  LICENSE
11/6/2017 10:10:11 AM  LICENSE-CODE
11/6/2017 10:10:11 AM  ThirdPartyNotices
11/6/2017 10:10:15 AM  tests
6/6/2018 7:58:59 PM    CONTRIBUTING.md
6/6/2018 7:58:59 PM    README.md
...
```

Você também pode classificar os objetos na ordem inversa, especificando o parâmetro de opção **Descending**.

```powershell
Get-ChildItem |
  Sort-Object -Property LastWriteTime, Name -Descending |
  Format-Table -Property LastWriteTime, Name
```

```output
LastWriteTime          Name
-------------          ----
12/1/2018 10:13:50 PM  reference
12/1/2018 10:13:50 PM  dsc
...
6/6/2018 7:58:59 PM    README.md
6/6/2018 7:58:59 PM    CONTRIBUTING.md
11/6/2017 10:10:15 AM  tests
11/6/2017 10:10:11 AM  ThirdPartyNotices
11/6/2017 10:10:11 AM  LICENSE-CODE
11/6/2017 10:10:11 AM  LICENSE
11/6/2017 10:10:11 AM  appveyor.yml
11/6/2017 10:10:11 AM  .openpublishing.build.ps1
11/6/2017 10:10:11 AM  .localization-config
```

## <a name="using-hash-tables"></a>Usando tabelas de hash

Você pode classificar diferentes propriedades em ordens diferentes usando tabelas de hash em uma matriz.
Cada tabela de hash usa uma chave **Expression** para especificar o nome da propriedade como uma cadeia de caracteres e uma chave **Ascending** ou **Descending** para especificar a ordem de classificação por `$true` ou `$false`.
A chave **Expression** é obrigatória.
A chave **Ascending** ou **Descending** é opcional.

O exemplo a seguir classifica os objetos em ordem decrescente por **LastWriteTime** e ordem crescente por **Name**.

```powershell
Get-ChildItem |
  Sort-Object -Property @{ Expression = 'LastWriteTime'; Descending = $true }, @{ Expression = 'Name'; Ascending = $true } |
  Format-Table -Property LastWriteTime, Name
```

```output
LastWriteTime          Name
-------------          ----
12/1/2018 10:13:50 PM  dsc
12/1/2018 10:13:50 PM  reference
11/29/2018 6:56:01 PM  .openpublishing.redirection.json
11/29/2018 6:56:01 PM  gallery
11/24/2018 10:33:22 AM developer
11/20/2018 7:22:19 PM  .markdownlint.json
...
```

Você também pode definir um scriptblock como a chave **Expression**.
Ao executar o cmdlet `Sort-Object`, o scriptblock é executado e o resultado é usado para classificação.

O exemplo a seguir classifica objetos em ordem decrescente pelo período de tempo entre **CreationTime** e **LastWriteTime**.

```powershell
Get-ChildItem |
  Sort-Object -Property @{ Expression = { $_.LastWriteTime - $_.CreationTime }; Descending = $true } |
  Format-Table -Property LastWriteTime, CreationTime
```

```output
LastWriteTime          CreationTime
-------------          ------------
12/1/2018 10:13:50 PM  11/6/2017 10:10:11 AM
12/1/2018 10:13:50 PM  11/6/2017 10:10:11 AM
11/7/2018 6:52:24 PM   11/6/2017 10:10:11 AM
11/7/2018 6:52:24 PM   11/6/2017 10:10:15 AM
11/3/2018 9:58:17 AM   11/6/2017 10:10:11 AM
10/26/2018 4:50:21 PM  11/6/2017 10:10:11 AM
11/17/2018 1:10:57 PM  11/29/2017 5:48:30 PM
11/12/2018 6:29:53 PM  12/7/2017 7:57:07 PM
...
```

## <a name="tips"></a>Dicas

Você pode omitir o nome do parâmetro **Property** da seguinte maneira:

```powershell
Sort-Object LastWriteTime, Name
```

Além disso, é possível consultar `Sort-Object` por seu alias interno, `sort`:

```powershell
sort LastWriteTime, Name
```

As chaves nas tabelas de hash para a classificação podem ser abreviadas da seguinte maneira:

```powershell
Sort-Object @{ e = 'LastWriteTime'; d = $true }, @{ e = 'Name'; a = $true }
```

Neste exemplo, o **e** significa **Expression**, o **d** significa **Descending** e o **a** significa **Ascending**.

Para melhorar a legibilidade, você pode colocar as tabelas de hash em uma variável separada:

```powershell
$order = @(
  @{ Expression = 'LastWriteTime'; Descending = $true }
  @{ Expression = 'Name'; Ascending = $true }
)

Get-ChildItem |
  Sort-Object $order |
  Format-Table LastWriteTime, Name
```
