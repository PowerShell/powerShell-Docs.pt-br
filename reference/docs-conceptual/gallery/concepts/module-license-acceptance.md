---
ms.date: 06/09/2017
schema: 2.0.0
keywords: powershell
title: Módulos que exigem a aceitação da licença
ms.openlocfilehash: a2f7ed72aae8579a6723f65b86dd0993f1a22afd
ms.sourcegitcommit: d36db3a1bc44aee6bc97422b557041c3aece4c67
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80082825"
---
# <a name="modules-requiring-license-acceptance"></a>Módulos que exigem a aceitação da licença

## <a name="synopsis"></a>SINOPSE

Os departamentos jurídicos de alguns publicadores de módulo exigem que os clientes aceitem explicitamente a licença antes de instalar o módulo da Galeria do PowerShell. Se um usuário instala, atualiza ou salva um módulo, usando o PowerShellGet, seja diretamente ou como uma dependência de outro pacote, e esse módulo exige que o usuário concorde com uma licença, o usuário deverá indicar que aceita a licença ou a operação falhará.

## <a name="publish-requirements-for-modules"></a>Requisitos de publicação para os módulos

Os módulos que gostariam de exigir dos usuários a aceitação da licença devem atender aos seguintes requisitos:

- A seção PSData do manifesto do módulo deve incluir RequireLicenseAcceptance = $True.
- O módulo deve conter o arquivo license.txt no diretório raiz.
- O manifesto do módulo deve conter o Uri da Licença.
- O módulo deve ser publicado com o PowerShellGet Format Versão 2.0 e posterior.

## <a name="impact-on-installsaveupdate-module"></a>Impacto em Install/Save/Update-Module

- Os cmdlets Install/Save/Update dão suporte a um novo parâmetro **AcceptLicense** que se comporta como se o usuário tivesse visto a licença.
- Se **RequiredLicenseAcceptance** é True e **AcceptLicense** não está especificado, o usuário vê `license.txt` e recebe a pergunta: `Do you accept these license terms
  (Yes/No/YesToAll/NoToAll)`.
  - Se a licença for aceita
    - **Save-Module:** o módulo é copiado no sistema do usuário
    - **Install-Module:** o módulo é copiado no sistema do usuário, na pasta apropriada (com base no escopo)
    - **Update-Module:** o módulo é atualizado.
  - Se a licença for recusada.
    - A operação é cancelada.
    - Todos os cmdlets verificam a existência dos metadados (**requireLicenseAcceptance** e Versão do Formato) que informam a exigência da aceitação da licença
    - Se a versão do formato do cliente for anterior à 2.0, a operação falhará e solicitará que o usuário atualize o cliente.
    - Se o módulo foi publicado com uma versão de formato mais antiga do que 2.0, o sinalizador requireLicenseAcceptance é ignorado.

## <a name="module-dependencies"></a>Dependências de módulo

- Durante uma operação Install/Save/Update, se um módulo dependente (outro item depende do módulo) exigir a aceitação da licença, o comportamento de aceitação da licença (acima) será necessário.
- Se a versão do módulo já estiver listada no catálogo local como instalada no sistema, ignoraremos a verificação da licença.
- Durante a operação Install/Save/Update, se um módulo dependente exigir uma licença, e a aceitação da licença não ocorrer, a operação falhará e seguirá os processos normais para o pacote que não foi possível instalar/salvar/atualizar.

## <a name="impact-on--force"></a>Impacto sobre -Force

Especificar `–Force` NÃO é suficiente para aceitar uma licença. `–AcceptLicense` é necessário para obter a permissão de instalação. Se `–Force` for especificado, RequiredLicenseAcceptance for True e `–AcceptLicense` NÃO for especificado, a operação falhará.

## <a name="examples"></a>EXEMPLOS

### <a name="example-1-update-module-manifest-to-require-license-acceptance"></a>Exemplo 1: Atualizar manifesto de módulo para exigir a aceitação da licença

```powershell
Update-ModuleManifest -Path C:\modulemanifest.psd1 -RequireLicenseAcceptance -PrivateData @{
    PSData = @{
        # Flag to indicate whether the module requires explicit user acceptance
        RequireLicenseAcceptance = $true
    } # End of PSData hashtable

 } # End of PrivateData hashtable
```

Esse comando atualiza o arquivo de manifesto e define o sinalizador RequireLicenseAcceptance como true.

### <a name="example-2-install-module-requiring-license-acceptance"></a>Exemplo 2: Instalar o módulo exigindo a aceitação da licença

```powershell
Install-Module -Name ModuleRequireLicenseAcceptance
```

```Output
License Acceptance

License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"):
```

Esse comando mostra a licença do arquivo `license.txt` e solicita ao usuário a aceitação da licença.

### <a name="example-3-install-module-requiring-license-acceptance-with--acceptlicense"></a>Exemplo 3: Instalar o módulo exigindo a aceitação da licença com -AcceptLicense

```powershell
Install-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense
```

O módulo é instalado sem qualquer solicitação de aceitação da licença.

### <a name="example-4-install-module-requiring-license-acceptance-with--force"></a>Exemplo 4: Instalar o módulo exigindo a aceitação da licença com -Force

```powershell
Install-Module -Name ModuleRequireLicenseAcceptance -Force
```

```Output
PackageManagement\Install-Package : License Acceptance is required for module 'ModuleRequireLicenseAcceptance'. Please specify '-AcceptLicense' to perform this operation.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.1.3.3\PSModule.psm1:1837 char:21
+ ...          $null = PackageManagement\Install-Package @PSBoundParameters
+                      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (Microsoft.Power....InstallPackage:InstallPackage) [Install-Package], E
   xception
    + FullyQualifiedErrorId : ForceAcceptLicense,Install-PackageUtility,Microsoft.PowerShell.PackageManagement.Cmdlets
   .InstallPackage
```

### <a name="example-5-install-module-with-dependencies-requiring-license-acceptance"></a>Exemplo 5: Instalar o módulo com dependências exigindo a aceitação da licença

O módulo **ModuleWithDependency** depende do módulo **ModuleRequireLicenseAcceptance**. O usuário recebe a solicitação para aceitar a licença.

```powershell
Install-Module -Name ModuleWithDependency
```

```Output
License Acceptance
MIT License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"):
```

### <a name="example-6-install-module-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a>Exemplo 6: Instalar o módulo com dependências exigindo a aceitação da licença e -AcceptLicense

O módulo **ModuleWithDependency** depende do módulo **ModuleRequireLicenseAcceptance**. O usuário não recebe a solicitação para aceitar a licença, pois **AcceptLicense** é especificado.

```powershell
Install-Module -Name ModuleWithDependency -AcceptLicense
```

### <a name="example-7-install-module-requiring-license-acceptance-on-a-client-older-than-psgetformatversion-20"></a>Exemplo 7: Instalar o módulo exigindo a aceitação da licença em um cliente mais antigo do que PSGetFormatVersion 2.0

```powershell
Install-Module -Name ModuleRequireLicenseAcceptance
```

```Output
WARNING: The specified module 'ModuleRequireLicenseAcceptance' with PowerShellGetFormatVersion
'2.0' is not supported by the current version of PowerShellGet. Get the latest version of the
PowerShellGet module to install this module, 'ModuleRequireLicenseAcceptance'.
```

### <a name="example-8-save-module-requiring-license-acceptance"></a>Exemplo 8: Salvar o módulo exigindo a aceitação da licença

```powershell
Save-Module -Name ModuleRequireLicenseAcceptance -Path C:\Saved
```

```Output
License Acceptance

License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"):
```

Esse comando mostra a licença do arquivo `license.txt` e solicita ao usuário a aceitação da licença.

### <a name="example-9-save-module-requiring-license-acceptance-with--acceptlicense"></a>Exemplo 9: Salvar o módulo exigindo a aceitação da licença com -AcceptLicense

```powershell
Save-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense -Path C:\Saved
```

O módulo é salvo sem qualquer solicitação de aceitação da licença.

### <a name="example-10-update-module-requiring-license-acceptance"></a>Exemplo 10: Atualizar o módulo exigindo a aceitação da licença

```powershell
Update-Module -Name ModuleRequireLicenseAcceptance
```

```Output
License Acceptance

License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"):
```

Esse comando mostra a licença do arquivo `license.txt` e solicita ao usuário a aceitação da licença.

### <a name="example-11-update-module-requiring-license-acceptance-with--acceptlicense"></a>Exemplo 11: Atualizar o módulo exigindo a aceitação da licença com -AcceptLicense

```powershell
Update-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense
```

O módulo é atualizado sem qualquer solicitação de aceitação da licença.

## <a name="more-details"></a>Mais detalhes

[Exigir a aceitação da licença para Scripts](./script-license-acceptance.md)

[Suporte à exigência de aceitação da licença no PowerShellGallery](../how-to/working-with-packages/packages-that-require-license-acceptance.md)

[Exigir a aceitação da licença ao implantar na Automação do Azure](../how-to/working-with-packages/deploy-to-azure-automation.md)
