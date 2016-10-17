# Get-InstalledModule

Obtém os módulos instalados em um computador.

## Descrição

O cmdlet Get-InstalledModule obtém os módulos do PowerShell que foram instalados no computador usando o cmdlet Install-Module.

Para cada módulo instalado, Get-InstalledModule retorna um objeto PSRepositoryItemInfo que pode, opcionalmente, ser redirecionado para Uninstall-Module para desinstalar os módulos instalados.

- Get-InstalledModule pode filtrar os módulos instalados com base em parâmetros de versão e nome.
- Get-InstalledModule pode filtrar segundo os parâmetros de versão: MinimumVersion, MaximumVersion, RequiredVersion, AllVersions.
  - Esses parâmetros são mutuamente exclusivos, exceto MinmimumVersion e MaximumVersion.
  - Esses parâmetros de versão são permitidos apenas com o nome exclusivo do módulo, sem curingas.
  - Se o parâmetro RequiredVersion não for especificado, Get-InstalledModule retornará a versão mais recente do módulo instalado que for igual ou maior que a versão mínima especificada ou a versão mais recente do módulo se nenhuma versão mínima tiver sido especificada. 
  - Se o parâmetro RequiredVersion for especificado, Get-InstalledModule retornará apenas a versão do módulo instalado que corresponde exatamente à versão especificada.

## Sintaxe do cmdlet
```powershell
Get-Command -Name Get-InstalledModule -Module PowerShellGet -Syntax
```

## Referência da ajuda online sobre cmdlets

[Get-InstalledModule](http://go.microsoft.com/fwlink/?LinkId=526863)

## Comandos de exemplo

```powershell

# Get all modules installed using PowerShellGet cmdlets
Get-InstalledModule

# Get a specific installed module
Get-InstalledModule DJoin

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.0        DJoin                               PSGallery            This is a PowerShell frontend to the DJOIN.exe c...

# Get installed module with wildcards
Get-InstalledModule -Name AzureRM*

# Get all versions of an installed module
Get-InstalledModule -Name AzureRM.Automation -AllVersions

# Get installed module with MinimumVersion
Get-InstalledModule -Name AzureRM.Automation -MinimumVersion 1.0.0

# Get installed module with MaximumVersion
Get-InstalledModule -Name AzureRM.Automation -MaximumVersion 1.0.8

# Get installed module with version range
Get-InstalledModule -Name AzureRM.Automation -MinimumVersion 1.0.0 -MaximumVersion 1.0.8

# Get installed module with RequiredVersion
Get-InstalledScript -Name AzureRM.Automation -RequiredVersion 1.0.3

# Properties of Get-InstalledModule returned object
Get-InstalledModule DJoin | Format-List * -Force

Name                       : DJoin
Version                    : 1.0
Type                       : Module
Description                : This is a PowerShell frontend to the DJOIN.exe command which provides better
                             discoverability and usability.
Author                     : Jeffrey Snover
CompanyName                : jsnover
Copyright                  : (C) Microsoft Corporation. All rights reserved.
PublishedDate              : 2/15/2016 7:12:37 PM
InstalledDate              : 4/5/2016 4:13:39 PM
UpdatedDate                :
LicenseUri                 :
ProjectUri                 :
IconUri                    :
Tags                       : {Nano, PSModule}
Includes                   : {Function, RoleCapability, Command, DscResource...}
PowerShellGetFormatVersion :
ReleaseNotes               :
Dependencies               : {}
RepositorySourceLocation   : https://www.powershellgallery.com/api/v2/
Repository                 : PSGallery
PackageManagementProvider  : NuGet
AdditionalMetadata         : {description, installeddate, tags, PackageManagementProvider...}
InstalledLocation          : C:\Program Files\WindowsPowerShell\Modules\DJoin\1.0

```



## Propriedades InstalledDate e UpdatedDate no objeto PSGetRepositoryItemInfo

    During the install operation:
        InstalledDate: current DateTime (Get-Date) value
        UpdatedDate: null

    During the Update operation:
        InstalledDate: InstalledDate from the previous installation otherwise current DateTime (Get-Date) value
        UpdatedDate: current DateTime (Get-Date) value

```powershell
Install-Module -Name ContosoServer -RequiredVersion 1.0 -Repository INT
Get-InstalledModule -Name ContosoServer | Format-Table Name, InstalledDate, UpdatedDate

Name          InstalledDate         UpdatedDate
----          -------------         -----------
ContosoServer 2/29/2016 11:59:14 AM


\Update-Module -Name ContosoServer
Get-InstalledModule -Name ContosoServer | Format-Table Name, InstalledDate, UpdatedDate

Name          InstalledDate         UpdatedDate
----          -------------         -----------
ContosoServer 2/29/2016 11:59:14 AM 2/29/2016 12:00:15 PM
```

<!--HONumber=Aug16_HO3-->

