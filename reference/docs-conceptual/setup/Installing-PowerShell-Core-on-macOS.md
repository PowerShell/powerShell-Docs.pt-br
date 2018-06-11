# <a name="installing-powershell-core-on-macos"></a><span data-ttu-id="94d15-101">Instalar o PowerShell Core no macOS</span><span class="sxs-lookup"><span data-stu-id="94d15-101">Installing PowerShell Core on macOS</span></span>

<span data-ttu-id="94d15-102">O PowerShell Core oferece suporte para macOS 10.12 e superior.</span><span class="sxs-lookup"><span data-stu-id="94d15-102">PowerShell Core supports macOS 10.12 and higher.</span></span>
<span data-ttu-id="94d15-103">Todos os pacotes estão disponíveis na nossa página [versões][] do GitHub.</span><span class="sxs-lookup"><span data-stu-id="94d15-103">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="94d15-104">Depois de instalar o pacote, execute `pwsh` em um terminal.</span><span class="sxs-lookup"><span data-stu-id="94d15-104">Once the package is installed, run `pwsh` from a terminal.</span></span>

### <a name="installation-via-homebrew-on-macos-1012"></a><span data-ttu-id="94d15-105">Instalação por meio do Homebrew no macOS 10.12</span><span class="sxs-lookup"><span data-stu-id="94d15-105">Installation via Homebrew on macOS 10.12</span></span>

<span data-ttu-id="94d15-106">[Homebrew][brew] é o gerenciador de pacotes preferido para macOS.</span><span class="sxs-lookup"><span data-stu-id="94d15-106">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="94d15-107">Se o comando `brew` não for encontrado, será necessário instalar o Homebrew seguindo [as instruções][brew].</span><span class="sxs-lookup"><span data-stu-id="94d15-107">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

<span data-ttu-id="94d15-108">Depois da instalação do Homebrew, é fácil instalar o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="94d15-108">Once you've installed Homebrew, installing PowerShell is easy.</span></span>
<span data-ttu-id="94d15-109">Primeiro, instale o [Homebrew-Cask][cask], assim você pode instalar mais pacotes:</span><span class="sxs-lookup"><span data-stu-id="94d15-109">First, install [Homebrew-Cask][cask], so you can install more packages:</span></span>

```sh
brew tap caskroom/cask
```

<span data-ttu-id="94d15-110">Agora, você pode instalar o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="94d15-110">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell
```

<span data-ttu-id="94d15-111">Por fim, verifique se a instalação está funcionando corretamente:</span><span class="sxs-lookup"><span data-stu-id="94d15-111">Finally, verify that your install is working properly:</span></span>

```sh
pwsh
```

<span data-ttu-id="94d15-112">Quando são lançadas novas versões do PowerShell, basta atualizar fórmula do Homebrew e atualizar o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="94d15-112">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> <span data-ttu-id="94d15-113">Os comandos acima podem ser chamados por meio de um host do PowerShell (pwsh), mas será necessário sair e entrar novamente no shell do PowerShell para concluir a atualização.</span><span class="sxs-lookup"><span data-stu-id="94d15-113">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade.</span></span>
> <span data-ttu-id="94d15-114">e atualizar os valores mostrados em $PSVersionTable.</span><span class="sxs-lookup"><span data-stu-id="94d15-114">and refresh the values shown in $PSVersionTable.</span></span>

[brew]: http://brew.sh/
[cask]: https://caskroom.github.io/

### <a name="installation-via-direct-download"></a><span data-ttu-id="94d15-115">Instalação por meio de download direto</span><span class="sxs-lookup"><span data-stu-id="94d15-115">Installation via Direct Download</span></span>

<span data-ttu-id="94d15-116">Faça o download do pacote PKG `powershell-6.0.2-osx.10.12-x64.pkg` da página [versões][] em seu computador com macOS.</span><span class="sxs-lookup"><span data-stu-id="94d15-116">Download the PKG package `powershell-6.0.2-osx.10.12-x64.pkg` from the [releases][] page onto your macOS machine.</span></span>

<span data-ttu-id="94d15-117">Clique duas vezes no arquivo e siga os prompts, ou instale-o do terminal:</span><span class="sxs-lookup"><span data-stu-id="94d15-117">You can double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.0.2-osx.10.12-x64.pkg -target /
```

## <a name="binary-archives"></a><span data-ttu-id="94d15-118">Arquivos binários</span><span class="sxs-lookup"><span data-stu-id="94d15-118">Binary Archives</span></span>

<span data-ttu-id="94d15-119">Arquivos binários `tar.gz` do PowerShell são fornecidos para plataformas macOS e Linux para habilitar cenários de implantação avançada.</span><span class="sxs-lookup"><span data-stu-id="94d15-119">PowerShell binary `tar.gz` archives are provided for macOS and Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="installing-binary-archives-on-macos"></a><span data-ttu-id="94d15-120">Instalação de arquivos binários no macOS</span><span class="sxs-lookup"><span data-stu-id="94d15-120">Installing binary archives on macOS</span></span>

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-osx-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /usr/local/microsoft/powershell/6.0.2

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /usr/local/microsoft/powershell/6.0.2

# Set execute permissions
sudo chmod +x /usr/local/microsoft/powershell/6.0.2/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /usr/local/microsoft/powershell/6.0.2/pwsh /usr/local/bin/pwsh
```

## <a name="uninstalling-powershell-core"></a><span data-ttu-id="94d15-121">Desinstalação do PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="94d15-121">Uninstalling PowerShell Core</span></span>

<span data-ttu-id="94d15-122">Se você instalou o PowerShell com Homebrew, a desinstalação é fácil:</span><span class="sxs-lookup"><span data-stu-id="94d15-122">If you installed PowerShell with Homebrew, uninstallation is easy:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="94d15-123">Se você instalou o PowerShell por meio de download direto, o PowerShell deve ser removido manualmente:</span><span class="sxs-lookup"><span data-stu-id="94d15-123">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="94d15-124">Para remover os caminhos adicionais do PowerShell, confira a seção [caminhos][] neste documento e remova os caminhos desejados com `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="94d15-124">To remove the additional PowerShell paths, please see the [paths][] section in this document and remove the desired the paths using `sudo rm`.</span></span>

> [!NOTE]
> <span data-ttu-id="94d15-125">Isso não é necessário se você tiver instalado usando o Homebrew.</span><span class="sxs-lookup"><span data-stu-id="94d15-125">This is not necessary if you installed with Homebrew.</span></span>

[caminhos]:#paths
[paths]:#paths

## <a name="paths"></a><span data-ttu-id="94d15-127">Caminhos</span><span class="sxs-lookup"><span data-stu-id="94d15-127">Paths</span></span>

* <span data-ttu-id="94d15-128">`$PSHOME` é `/opt/microsoft/powershell/6.0.0/`</span><span class="sxs-lookup"><span data-stu-id="94d15-128">`$PSHOME` is `/opt/microsoft/powershell/6.0.0/`</span></span>
* <span data-ttu-id="94d15-129">Perfis de usuário serão lidos de `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="94d15-129">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="94d15-130">Perfis padrão serão lidos de `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="94d15-130">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="94d15-131">Módulos de usuário serão lidos de `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="94d15-131">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="94d15-132">Módulos compartilhados serão lidos de `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="94d15-132">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="94d15-133">Módulos padrão serão lidos de `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="94d15-133">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="94d15-134">Histórico de PSReadline será gravado em `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="94d15-134">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="94d15-135">Os perfis respeitam a configuração por host do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="94d15-135">The profiles respect PowerShell's per-host configuration.</span></span>
<span data-ttu-id="94d15-136">Então, os perfis de host específicos padrão existe no `Microsoft.PowerShell_profile.ps1` nas mesmas localizações.</span><span class="sxs-lookup"><span data-stu-id="94d15-136">So the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="94d15-137">O PowerShell respeita a [Especificação de Diretório Base XDG][xdg-bds] no macOS.</span><span class="sxs-lookup"><span data-stu-id="94d15-137">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on macOS.</span></span>

<span data-ttu-id="94d15-138">Como o macOS é uma derivação do BSD, o prefixo `/usr/local` é usado em vez de `/opt`.</span><span class="sxs-lookup"><span data-stu-id="94d15-138">Because macOS is a derivation of BSD, the prefix `/usr/local` is used instead of `/opt`.</span></span>
<span data-ttu-id="94d15-139">Portanto, `$PSHOME` é `/usr/local/microsoft/powershell/6.0.0/`, e o symlink é colocado em `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="94d15-139">Thus, `$PSHOME` is `/usr/local/microsoft/powershell/6.0.0/`, and the symlink is placed at `/usr/local/bin/pwsh`.</span></span>

[versões]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html