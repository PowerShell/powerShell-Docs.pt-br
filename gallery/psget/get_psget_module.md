---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: galeria,powershell,cmdlet,psget
title: "Módulo Get PowerShellGet"
ms.openlocfilehash: a5a323b17709e519ec57623a9dd7499e591bbed5
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2017
---
<a id="get-powershellget-module" class="xliff"></a>
Módulo Get PowerShellGet
========================

<a id="powershellget-is-an-in-box-module-in-the-following-releases" class="xliff"></a>
### PowerShellGet é um módulo nativo nas seguintes versões
- [Windows 10](https://www.microsoft.com/en-us/windows/get-windows-10) ou mais recente
- [Windows Server 2016](https://technet.microsoft.com/en-us/windows-server-docs/get-started/windows-server-2016) ou mais recente
- [Windows Management Framework (WMF) 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) ou mais recente
- [PowerShell 6](https://github.com/PowerShell/PowerShell/releases)

<a id="get-powershellget-module-for-powershell-versions-30-and-40" class="xliff"></a>
### Módulo Get PowerShellGet para o PowerShell versões 3.0 e 4.0
- [MSI do PackageManagement](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409) 

<a id="get-the-latest-version-from-powershell-gallery" class="xliff"></a>
### Obter a versão mais recente da Galeria do PowerShell

- Antes de atualizar o PowerShellGet, você sempre deve instalar o provedor do Nuget mais recente. Para fazer isso, execute o seguinte em uma sessão do PowerShell com privilégios elevados.
```powershell
Install-PackageProvider Nuget –Force
Exit
```

<a id="for-systems-with-powershell-50-or-newer-you-can-install-the-latest-powershellget" class="xliff"></a>
#### Para sistemas com o PowerShell 5.0 (ou mais recente), você pode instalar o PowerShellGet mais recente 
- Para fazer isso no Windows 10, no Windows Server 2016, em qualquer sistema com o WMF 5.0 ou 5.1 instalado ou em qualquer sistema com o PowerShell 6, execute os seguintes comandos em uma sessão do PowerShell com privilégios elevados.
```powershell
Install-Module –Name PowerShellGet –Force
Exit
```

- Use Update-Module para obter versões mais recentes.
```powershell
Update-Module -Name PowerShellGet
Exit
```

<a id="for-systems-running-powershell-3-or-powershell-4-that-have-installed-the-packagemanagement-msihttpgomicrosoftcomfwlinklinkid746217clcid0x409" class="xliff"></a>
#### Para sistemas que executam o PowerShell 3 ou o PowerShell 4 que têm o [MSI do PackageManagement](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409) instalado

- Use o cmdlet do PowerShellGet abaixo em uma sessão do PowerShell com privilégios elevados para salvar os módulos em um diretório local

```powershell
Save-Module PowerShellGet -Path C:\LocalFolder
Exit
```

- Verifique se os módulos PowerShellGet e PackageManagment não estão carregados em nenhum outro processo.
- Exclua o conteúdo das pastas `$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\` e `$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\`.
- Reabra o Console do PS com permissões elevadas e execute os comandos a seguir.

```powershell
Copy-Item "C:\LocalFolder\PowerShellGet\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\" -Recurse -Force
Copy-Item "C:\LocalFolder\PackageManagement\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\" -Recurse -Force