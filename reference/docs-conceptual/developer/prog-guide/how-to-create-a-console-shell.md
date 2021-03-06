---
ms.date: 09/13/2016
ms.topic: reference
title: Como criar um shell do console
description: Como criar um shell do console
ms.openlocfilehash: 9ea67c43b1ee35b1fbfc553b22a1423419317ca2
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92657215"
---
# <a name="how-to-create-a-console-shell"></a>Como criar um shell do console

O Windows PowerShell fornece uma ferramenta de Make-Shell, também conhecida como "Make-Kit", usada para criar um shell de console que não seja extensível. Os shells criados com essa nova ferramenta não podem ser estendidos posteriormente por meio de um snap-in do Windows PowerShell.

## <a name="syntax"></a>Sintaxe

Aqui está a sintaxe usada para executar Make-Shell de dentro de um make-File.

```
make-shell
  -out n.exe
  -namespace ns
  [ -lib libdirectory1[,libdirectory2,..] ]
  [ -reference ca1.dll[,ca2.dll,...] ]
  [ -formatdata fd1.format.ps1xml[,fd2.format.ps1xml,...] ]
  [ -typedata td1.type.ps1xml[,td2.type.ps1xml,...] ]
  [ -source c1.cs [,c2.cs,...] ]
  [ -authorizationmanager authorizationManagerType ]
  [ -win32icon i.ico ]
  [ -initscript p.ps1 ]
  [ -builtinscript s1.ps1[,s2.ps1,...] ]
  [ -resource resourcefile.txt ]
  [ -cscflags cscFlags ]
  [ -? | -help ]
```

## <a name="parameters"></a>Parâmetros

Aqui está uma breve descrição dos parâmetros de make-Shell.

> [!CAUTION]
> O make-shell não dá suporte a caminhos UNC para assemblies.

|Parâmetro|Descrição|
|---------------|-----------------|
|-out n.exe|Obrigatórios. O nome do Shell a ser produzido. O caminho é especificado como parte desse parâmetro.<br /><br /> Make-Shell acrescentará ". exe" a esse valor se não for especificado. **Cuidado:**  Não crie um arquivo de saída com o mesmo nome que o arquivo. dll referenciado. Se você tentar isso, a ferramenta de Make-Shell criará um arquivo. cs com o mesmo nome, que substituirá o arquivo. cs que tem o código-fonte do cmdlet.|
|-namespace NS|Obrigatórios. O namespace a ser usado para a classe derivada de [System. Management. Automation. Runspaces. Runspaceconfiguration](/dotnet/api/System.Management.Automation.Runspaces.RunspaceConfiguration) que o make-kit gera e compila.|
|-lib libdirectory1 [, libdirectory2,..]|Os diretórios que são pesquisados em assemblies do .NET, incluindo os assemblies do Windows PowerShell, os assemblies especificados pelo `reference` parâmetro, os assemblies referenciados indiretamente por outro assembly e os assemblies do sistema .net.|
|-ca1.dll de referência [, ca2.dll,...]|Uma lista separada por vírgulas dos assemblies a serem incluídos no Shell. Esses assemblies incluem todos os assemblies de cmdlet e provedor, bem como os assemblies de recursos que devem ser carregados. Se esse parâmetro não for especificado, será produzido um shell que contém apenas os cmdlets e os provedores principais fornecidos pelo Windows PowerShell.<br /><br /> Os assemblies podem ser especificados usando seu caminho completo, caso contrário, eles serão pesquisados usando o caminho especificado pelo `lib` parâmetro.|
|-FormatData fd1.format.ps1XML [, fd2.format.ps1XML,...]|Uma lista separada por vírgulas dos dados de formato a serem incluídos no Shell. Se esse parâmetro não for especificado, será produzido um shell que contém apenas os dados de formato fornecidos pelo Windows PowerShell.|
|-TypeData td1.type.ps1XML [, td2.type.ps1XML,...]|Uma lista separada por vírgulas do tipo dados a serem incluídos no Shell. Se esse parâmetro não for especificado, será produzido um shell que contém apenas os dados de tipo fornecidos pelo Windows PowerShell.|
|-Source c1.cs [, c2.cs,...]|O nome de um arquivo, fornecido pelo desenvolvedor do Shell, que contém qualquer código-fonte necessário para compilar o Shell.<br /><br /> O arquivo de código-fonte pode conter qualquer um dos seguintes códigos-fonte:<br /><br /> -A implementação do Gerenciador de autorização que substitui o Gerenciador de autorização padrão. (Isso também pode ser fornecido compilado em um assembly.)<br />-Declarações de atributo informativo de assembly: como AssemblyCompanyAttribute, AssemblyCopyrightAttribute, AssemblyFileVersionAttribute, AssemblyInformationalVersionAttribute, AssemblyProductAttribute e AssemblyTrademarkAttribute.|
|-AuthorizationManager authorizationManagerType|O tipo que contém a implementação do Gerenciador de autorização. Isso pode ser definido no código-fonte ou compilado em um assembly (especificado pelo `reference` parâmetro). Se esse parâmetro não for especificado, o Gerenciador de segurança padrão será usado. O valor deve ser o nome completo do tipo, incluindo namespaces.|
|-win32icon i. ico|O ícone do arquivo. exe para o Shell. Se não for especificado, o Shell terá o ícone que o compilador c# inclui (se houver).|
|-initscript p.ps1|O perfil de inicialização do Shell. O arquivo está incluído "no estado em que se encontra"; nenhuma verificação de validade é feita por Make-Shell.|
|-builtinscript s1.ps1 [, s2.ps1,...]|Uma lista de scripts internos para o Shell. Esses scripts são descobertos antes dos scripts no caminho, e seu conteúdo não pode ser alterado depois que o Shell é criado.<br /><br /> Os arquivos estão incluídos "no estado em que se encontram"; nenhuma verificação de validade é feita por Make-Shell.|
|-resourcefile.txt de recursos|O arquivo. txt que contém a ajuda e os recursos de faixa para o Shell. O primeiro recurso é denominado ShellHelp e contém o texto exibido se o Shell for invocado com o `help` parâmetro. O segundo recurso é denominado ShellBanner e contém o texto e as informações de direitos autorais exibidas quando o Shell é iniciado no modo interativo.<br /><br /> Se esse parâmetro não for fornecido ou se esses recursos não estiverem presentes, uma ajuda e faixa genérica serão usadas.|
|-cscflags cscFlags|Sinalizadores que devem ser passados para o compilador C# (csc.exe). Eles são transmitidos por meio de inalterado. Se esse parâmetro incluir espaços, ele deverá estar entre aspas duplas.|
|-?<br /><br /> -help|Exibe a mensagem de direitos autorais e Make-Shell opções de linha de comando.|
|-verbose|Exibe informações detalhadas enquanto o Shell está sendo criado.|

## <a name="see-also"></a>Consulte Também

[Guia do programador do Windows PowerShell](./windows-powershell-programmer-s-guide.md)

[SDK do Windows PowerShell](../windows-powershell-reference.md)
