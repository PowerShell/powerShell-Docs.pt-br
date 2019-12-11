---
ms.date: 06/12/2017
keywords: wmf,powershell,instalação
title: Aprimoramentos no recurso JEA (Administração Suficiente)
ms.openlocfilehash: 847ae92a6225023bcd0ee3dfe7c7058bdc356836
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "71147596"
---
# <a name="improvements-to-just-enough-administration-jea"></a>Aprimoramentos no recurso JEA (Administração Suficiente)

A Administração Just Enough é um novo recurso no WMF 5.0 que permite a administração baseada em funções por meio da comunicação remota do PowerShell. Isso amplia a infraestrutura existente do ponto de extremidade restrito, permitindo que não administradores executem comandos, scripts e executáveis específicos como administrador. Isso possibilita a redução do número de administradores totais em seu ambiente e melhora a segurança.

## <a name="constrained-file-copy-tofrom-jea-endpoints"></a>Cópia de arquivo restrito de/para pontos de extremidade JEA

Agora, você pode copiar remotamente arquivos de/para um ponto de extremidade JEA e ter certeza de que o usuário conectado não poderá copiar *nenhum* arquivo em seu sistema. Isso é possível ao configurar seu arquivo PSSC para montar uma unidade de usuário para conectar usuários. A unidade de usuário é um novo PSDrive exclusivo para cada usuário conectado e persiste nas sessões. Quando `Copy-Item` é usado para copiar arquivos de ou para uma sessão JEA, ele é restrito para permitir apenas acesso à unidade do usuário. As tentativas de copiar arquivos para qualquer outro PSDrive falharão.

Para configurar a unidade de usuário no arquivo de configuração de sessão JEA, use os novos campos a seguir:

```powershell
MountUserDrive = $true
UserDriveMaximumSize = 10485760    # 10 MB
```

A pasta que dá suporte à unidade do usuário será criada em `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\DriveRoots\DOMAIN_USER`

Para utilizar a unidade de usuário e copiar arquivos de/para um ponto de extremidade JEA configurado para expor a unidade do usuário, use os parâmetros `-ToSession` e `-FromSession` em `Copy-Item`.

```powershell
# Connect to the JEA endpoint
$jeasession = New-PSSession -ComputerName 'srv01' -ConfigurationName 'UserDemo'

# Copy a file in the local folder to the remote machine.
# Note: you cannot specify the file name or subfolder on the remote machine.
# You must exactly type "User:"
Copy-Item -Path .\SampleFile.txt -Destination User: -ToSession $jeasession

# Copy the file back from the remote machine to your local machine
Copy-Item -Path User:\SampleFile.txt -Destination . -FromSession $jeasession
```

Em seguida, você pode escrever funções personalizadas para processar os dados armazenados na unidade do usuário e disponibilizar esses para os usuários no arquivo de Capacidade de Função.

## <a name="support-for-group-managed-service-accounts"></a>Suporte para Contas de Serviço Gerenciado de Grupo

Em alguns casos, uma tarefa que um usuário precisa para executar em uma sessão JEA precisará acessar recursos fora do computador local. Quando uma sessão JEA é configurada para usar uma conta virtual, qualquer tentativa de acessar esses recursos parecem que serão provenientes da identidade do computador local, não da conta virtual ou do usuário conectado. No TP5, habilitamos o suporte para executar o JEA sob o contexto de uma [Conta de Serviço Gerenciado de Grupo](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj128431\(v=ws.11\)), facilitando muito o acesso aos recursos de rede usando uma identidade de domínio.

Para configurar uma sessão JEA para executar sob uma conta gMSA, use a nova chave a seguir no arquivo PSSC:

```powershell
# Provide the name of your gMSA account here (don't include a trailing $)
# The local machine must be privileged to use this gMSA in Active Directory
GroupManagedServiceAccount = 'myGMSAforJEA'

# You cannot configure a JEA endpoint to use both a gMSA and virtual account
# You can leave the RunAsVirtualAccount field commented out or explicitly set it to false
RunAsVirtualAccount = $false
```

> [!NOTE]
> Contas de Serviço Gerenciado de Grupo não arcam com o isolamento ou o escopo limitado de contas virtuais.
> Cada usuário conectado compartilha a mesma identidade de gMSA, que pode ter permissões em toda a empresa. Tenha muito cuidado ao optar por usar uma gMSA, e sempre prefira contas virtuais que são limitadas no computador local, quando possível.

## <a name="conditional-access-policies"></a>Políticas de acesso condicional

O JEA é excelente para limitar o que alguém pode fazer quando ele se conecta a um sistema para gerenciá-lo, mas e se você também desejar limitar *quando* alguém pode usar JEA? Adicionamos opções de configuração aos arquivos de configuração de sessão (.pssc) para permitir que você especifique grupos de segurança aos quais um usuário deve pertencer para estabelecer uma sessão JEA. Isso é especialmente útil se você tiver um sistema JIT (Just In Time) em seu ambiente e quiser que os usuários elevem os próprios privilégios antes de acessar um ponto de extremidade JEA altamente privilegiado.

O novo campo *RequiredGroups* no arquivo de PSSC permite que você especifique a lógica para determinar se um usuário pode se conectar ao JEA. Ele consiste em especificar uma tabela de hash (opcionalmente aninhada) que usa as chaves 'E' e 'Ou' para construir as regras. Veja alguns exemplos de como utilizar esse campo:

```powershell
# Example 1: Connecting users must belong to a security group called "elevated-jea"
RequiredGroups = @{ And = 'elevated-jea' }

# Example 2: Connecting users must have signed on with 2 factor authentication or a smart card
# The 2 factor authentication group name is "2FA-logon" and the smart card group name is "smartcard-logon"
RequiredGroups = @{ Or = '2FA-logon', 'smartcard-logon' }

# Example 3: Connecting users must elevate into "elevated-jea" with their JIT system and have logged on with 2FA or a smart card
RequiredGroups = @{ And = 'elevated-jea', @{ Or = '2FA-logon', 'smartcard-logon' }}
```

## <a name="fixed-virtual-accounts-are-now-supported-on-windows-server-2008-r2"></a>Corrigido: contas virtuais agora têm suporte no Windows Server 2008 R2

No WMF 5.1, agora você poderá usar contas virtuais no Windows Server 2008 R2, permitindo configurações consistentes e paridade de recursos entre o Windows Server 2008 R2 - 2016. Contas virtuais permanecem sem suporte ao usar JEA no Windows 7.