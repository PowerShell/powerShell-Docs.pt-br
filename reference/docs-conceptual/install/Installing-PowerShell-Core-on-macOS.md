---
title: Instalar o PowerShell Core no macOS
description: Informações sobre a instalação do PowerShell Core no macOS
ms.date: 12/12/2018
ms.openlocfilehash: ad1306e99261e8e6e2fd49d3199d863929c31e92
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73444435"
---
# <a name="installing-powershell-core-on-macos"></a>Instalar o PowerShell Core no macOS

O PowerShell Core oferece suporte para macOS 10.12 e superior.
Todos os pacotes estão disponíveis na nossa página [lançamentos][] do GitHub.
Depois de instalar o pacote, execute `pwsh` em um terminal.

> [!TIP]
> Se você já tiver o [SDK do .NET Core](/dotnet/core/sdk) instalado, será fácil instalar o PowerShell como uma [ferramenta global do .NET](/dotnet/core/tools/global-tools).
>
> ```
> dotnet tool install --global PowerShell
> ```

## <a name="about-brew"></a>Sobre Brew

[Homebrew][brew] é o gerenciador de pacotes preferido para macOS.
Se o comando `brew` não for encontrado, será necessário instalar o Homebrew seguindo [as instruções][brew].
Caso contrário, você poderá instalar o PowerShell por [Download direto](#installation-via-direct-download) ou pelos [Arquivos binários](#binary-archives).

## <a name="installation-of-latest-stable-release-via-homebrew-on-macos-1012-or-higher"></a>Instalação da versão estável mais recente por meio do Homebrew no macOS 10.12 ou superior

Confira [Sobre Brew](#about-brew) para obter mais informações sobre Brew.

Agora, você pode instalar o PowerShell:

```sh
brew cask install powershell
```

Por fim, verifique se a instalação está funcionando corretamente:

```sh
pwsh
```

Quando novas versões do PowerShell forem lançadas, atualize a fórmula do Homebrew e faça upgrade do PowerShell:

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> Os comandos acima podem ser chamados por meio de um host do PowerShell (pwsh), mas será necessário sair e entrar novamente no shell do PowerShell para concluir o upgrade e atualizar os valores mostrados em `$PSVersionTable`.

[brew]: https://brew.sh/

## <a name="installation-of-latest-preview-release-via-homebrew-on-macos-1012-or-higher"></a>Instalação da versão prévia estável mais recente por meio do Homebrew no macOS 10.12 ou superior

Confira [Sobre Brew](#about-brew) para obter mais informações sobre Brew.

Depois de instalar o Homebrew, você pode instalar o PowerShell.
Primeiro, instale o pacote [Cask-Versions][cask-versions] que permite instalar versões alternativas de pacotes cask:

```sh
brew tap homebrew/cask-versions
```

Agora, você pode instalar o PowerShell:

```sh
brew cask install powershell-preview
```

Por fim, verifique se a instalação está funcionando corretamente:

```sh
pwsh-preview
```

Quando novas versões do PowerShell forem lançadas, atualize a fórmula do Homebrew e faça upgrade do PowerShell:

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> Os comandos acima podem ser chamados por meio de um host do PowerShell (pwsh), mas será necessário sair e entrar novamente no shell do PowerShell para concluir a atualização.
> e atualizar os valores mostrados em `$PSVersionTable`.

## <a name="installation-via-direct-download"></a>Instalação por meio de download direto

Baixe o pacote PKG `powershell-6.2.0-osx-x64.pkg`
na página [Lançamentos][] no computador com macOS.

Clique duas vezes no arquivo e siga os prompts, ou instale-o do terminal:

```sh
sudo installer -pkg powershell-6.2.0-osx-x64.pkg -target /
```

Instalar [OpenSSL](#install-openssl). O OpenSSL é necessário para operações CIM e comunicação remota do PowerShell.

## <a name="binary-archives"></a>Arquivos binários

Os arquivos binários `tar.gz` do PowerShell são fornecidos para plataformas macOS a fim de habilitar cenários de implantação avançada.

### <a name="installing-binary-archives-on-macos"></a>Instalação de arquivos binários no macOS

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-osx-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /usr/local/microsoft/powershell/6.2.0

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /usr/local/microsoft/powershell/6.2.0

# Set execute permissions
sudo chmod +x /usr/local/microsoft/powershell/6.2.0/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /usr/local/microsoft/powershell/6.2.0/pwsh /usr/local/bin/pwsh
```

Instalar [OpenSSL](#install-openssl). O OpenSSL é necessário para operações CIM e comunicação remota do PowerShell.

## <a name="installing-dependencies"></a>Instalar dependências

### <a name="install-xcode-command-line-tools"></a>Instalar ferramentas da linha de comando XCode

```sh
xcode-select --install
```

### <a name="install-openssl"></a>Instalar OpenSSL

O OpenSSL é necessário para operações CIM e comunicação remota do PowerShell. Você pode instalar por meio de MacPorts ou Brew.

#### <a name="install-openssl-via-brew"></a>Instalar o OpenSSL por meio de Brew

Confira [Sobre Brew](#about-brew) para obter mais informações sobre Brew.

Execute `brew install openssl` para instalar o OpenSSL.

#### <a name="install-openssl-via-macports"></a>Instalar o OpenSSL por meio de MacPorts

1. Instale as [ferramentas da linha de comando XCode](#install-xcode-command-line-tools).
1. Instale MacPorts.
   Se precisar de instruções, confira o [guia de instalação](https://guide.macports.org/chunked/installing.macports.html).
1. Atualize o MacPorts executando `sudo port selfupdate`.
1. Atualize os pacotes de MacPorts executando `sudo port upgrade outdated`.
1. Instale o OpenSSL executando `sudo port install openssl`.
1. Vincule as bibliotecas para disponibilizá-las para o PowerShell:

```sh
sudo mkdir -p /usr/local/opt/openssl
sudo ln -s /opt/local/lib /usr/local/opt/openssl/lib
```

## <a name="uninstalling-powershell-core"></a>Desinstalação do PowerShell Core

Se você instalou o PowerShell com Homebrew, use o comando a seguir para desinstalar:

```sh
brew cask uninstall powershell
```

Se você instalou o PowerShell por meio de download direto, o PowerShell deve ser removido manualmente:

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

Para remover os caminhos adicionais do PowerShell, confira a seção [caminhos](#paths) neste documento e remova os caminhos com `sudo rm`.

> [!NOTE]
> Isso não é necessário se você tiver instalado usando o Homebrew.

## <a name="paths"></a>Caminhos

* `$PSHOME` é `/usr/local/microsoft/powershell/6.2.0/`
* Perfis de usuário serão lidos de `~/.config/powershell/profile.ps1`
* Perfis padrão serão lidos de `$PSHOME/profile.ps1`
* Módulos de usuário serão lidos de `~/.local/share/powershell/Modules`
* Módulos compartilhados serão lidos de `/usr/local/share/powershell/Modules`
* Módulos padrão serão lidos de `$PSHOME/Modules`
* Histórico de PSReadline será gravado em `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`

Os perfis respeitam a configuração por host do PowerShell.
Assim, os perfis de hosts específicos padrão existem no `Microsoft.PowerShell_profile.ps1` nas mesmas localizações.

O PowerShell respeita a [Especificação de Diretório Base XDG][xdg-bds] no macOS.

Como o macOS é uma derivação do BSD, o prefixo `/usr/local` é usado em vez de `/opt`.
Portanto, `$PSHOME` é `/usr/local/microsoft/powershell/6.2.0/`, e o link simbólico é colocado em `/usr/local/bin/pwsh`.

## <a name="additional-resources"></a>Recursos adicionais

* [Homebrew Web][brew]
* [Repositório do Homebrew no Github][GitHub]
* [Homebrew-Cask][cask]

[brew]: http://brew.sh/
[Cask]: https://github.com/Homebrew/homebrew-cask
[cask-versions]: https://github.com/Homebrew/homebrew-cask-versions
[GitHub]: https://github.com/Homebrew
[lançamentos]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
