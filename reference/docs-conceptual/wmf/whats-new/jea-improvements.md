---
ms.date: 06/12/2017
keywords: wmf,powershell,instalação
title: Aprimoramentos no recurso JEA (Administração Suficiente)
ms.openlocfilehash: 847ae92a6225023bcd0ee3dfe7c7058bdc356836
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2020
ms.locfileid: "71147596"
---
# <a name="improvements-to-just-enough-administration-jea"></a><span data-ttu-id="9b850-103">Aprimoramentos no recurso JEA (Administração Suficiente)</span><span class="sxs-lookup"><span data-stu-id="9b850-103">Improvements to Just Enough Administration (JEA)</span></span>

<span data-ttu-id="9b850-104">A Administração Just Enough é um novo recurso no WMF 5.0 que permite a administração baseada em funções por meio da comunicação remota do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9b850-104">Just Enough Administration is a new feature in WMF 5.0 that enables role-based administration through PowerShell remoting.</span></span> <span data-ttu-id="9b850-105">Isso amplia a infraestrutura existente do ponto de extremidade restrito, permitindo que não administradores executem comandos, scripts e executáveis específicos como administrador.</span><span class="sxs-lookup"><span data-stu-id="9b850-105">It extends the existing constrained endpoint infrastructure by allowing non-administrators to run specific commands, scripts, and executables as an administrator.</span></span> <span data-ttu-id="9b850-106">Isso possibilita a redução do número de administradores totais em seu ambiente e melhora a segurança.</span><span class="sxs-lookup"><span data-stu-id="9b850-106">This enables you to reduce the number of full administrators in your environment and improve security.</span></span>

## <a name="constrained-file-copy-tofrom-jea-endpoints"></a><span data-ttu-id="9b850-107">Cópia de arquivo restrito de/para pontos de extremidade JEA</span><span class="sxs-lookup"><span data-stu-id="9b850-107">Constrained file copy to/from JEA endpoints</span></span>

<span data-ttu-id="9b850-108">Agora, você pode copiar remotamente arquivos de/para um ponto de extremidade JEA e ter certeza de que o usuário conectado não poderá copiar *nenhum* arquivo em seu sistema.</span><span class="sxs-lookup"><span data-stu-id="9b850-108">You can now remotely copy files to/from a JEA endpoint and be assured that the connecting user can't copy just *any* file on your system.</span></span> <span data-ttu-id="9b850-109">Isso é possível ao configurar seu arquivo PSSC para montar uma unidade de usuário para conectar usuários.</span><span class="sxs-lookup"><span data-stu-id="9b850-109">This is possible by configuring your PSSC file to mount a user drive for connecting users.</span></span> <span data-ttu-id="9b850-110">A unidade de usuário é um novo PSDrive exclusivo para cada usuário conectado e persiste nas sessões.</span><span class="sxs-lookup"><span data-stu-id="9b850-110">The user drive is a new PSDrive that is unique to each connecting user and persists across sessions.</span></span> <span data-ttu-id="9b850-111">Quando `Copy-Item` é usado para copiar arquivos de ou para uma sessão JEA, ele é restrito para permitir apenas acesso à unidade do usuário.</span><span class="sxs-lookup"><span data-stu-id="9b850-111">When `Copy-Item` is used to copy files to or from a JEA session, it is constrained to only allow access to the user drive.</span></span> <span data-ttu-id="9b850-112">As tentativas de copiar arquivos para qualquer outro PSDrive falharão.</span><span class="sxs-lookup"><span data-stu-id="9b850-112">Attempts to copy files to any other PSDrive will fail.</span></span>

<span data-ttu-id="9b850-113">Para configurar a unidade de usuário no arquivo de configuração de sessão JEA, use os novos campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9b850-113">To set up the user drive in your JEA session configuration file, use the following new fields:</span></span>

```powershell
MountUserDrive = $true
UserDriveMaximumSize = 10485760    # 10 MB
```

<span data-ttu-id="9b850-114">A pasta que dá suporte à unidade do usuário será criada em `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\DriveRoots\DOMAIN_USER`</span><span class="sxs-lookup"><span data-stu-id="9b850-114">The folder backing the user drive will be created at `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\DriveRoots\DOMAIN_USER`</span></span>

<span data-ttu-id="9b850-115">Para utilizar a unidade de usuário e copiar arquivos de/para um ponto de extremidade JEA configurado para expor a unidade do usuário, use os parâmetros `-ToSession` e `-FromSession` em `Copy-Item`.</span><span class="sxs-lookup"><span data-stu-id="9b850-115">To utilize the user drive and copy files to/from a JEA endpoint configured to expose the User drive, use the `-ToSession` and `-FromSession` parameters on `Copy-Item`.</span></span>

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

<span data-ttu-id="9b850-116">Em seguida, você pode escrever funções personalizadas para processar os dados armazenados na unidade do usuário e disponibilizar esses para os usuários no arquivo de Capacidade de Função.</span><span class="sxs-lookup"><span data-stu-id="9b850-116">You can then write custom functions to process the data stored in the user drive and make those available to users in your Role Capability file.</span></span>

## <a name="support-for-group-managed-service-accounts"></a><span data-ttu-id="9b850-117">Suporte para Contas de Serviço Gerenciado de Grupo</span><span class="sxs-lookup"><span data-stu-id="9b850-117">Support for Group Managed Service Accounts</span></span>

<span data-ttu-id="9b850-118">Em alguns casos, uma tarefa que um usuário precisa para executar em uma sessão JEA precisará acessar recursos fora do computador local.</span><span class="sxs-lookup"><span data-stu-id="9b850-118">In some cases, a task a user needs to perform in a JEA session may need to access resources beyond the local machine.</span></span> <span data-ttu-id="9b850-119">Quando uma sessão JEA é configurada para usar uma conta virtual, qualquer tentativa de acessar esses recursos parecem que serão provenientes da identidade do computador local, não da conta virtual ou do usuário conectado.</span><span class="sxs-lookup"><span data-stu-id="9b850-119">When a JEA session is configured to use a virtual account, any attempt to reach such resources will appear to come from the local machine's identity, not the virtual account or connected user.</span></span> <span data-ttu-id="9b850-120">No TP5, habilitamos o suporte para executar o JEA sob o contexto de uma [Conta de Serviço Gerenciado de Grupo](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj128431\(v=ws.11\)), facilitando muito o acesso aos recursos de rede usando uma identidade de domínio.</span><span class="sxs-lookup"><span data-stu-id="9b850-120">In TP5, we have enabled support for running JEA under the context of a [Group Managed Service Account](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj128431\(v=ws.11\)), making it much easier to access network resources by using a domain identity.</span></span>

<span data-ttu-id="9b850-121">Para configurar uma sessão JEA para executar sob uma conta gMSA, use a nova chave a seguir no arquivo PSSC:</span><span class="sxs-lookup"><span data-stu-id="9b850-121">To configure a JEA session to run under a gMSA account, use the following new key in your PSSC file:</span></span>

```powershell
# Provide the name of your gMSA account here (don't include a trailing $)
# The local machine must be privileged to use this gMSA in Active Directory
GroupManagedServiceAccount = 'myGMSAforJEA'

# You cannot configure a JEA endpoint to use both a gMSA and virtual account
# You can leave the RunAsVirtualAccount field commented out or explicitly set it to false
RunAsVirtualAccount = $false
```

> [!NOTE]
> <span data-ttu-id="9b850-122">Contas de Serviço Gerenciado de Grupo não arcam com o isolamento ou o escopo limitado de contas virtuais.</span><span class="sxs-lookup"><span data-stu-id="9b850-122">Group Managed Service Accounts do not afford the isolation or limited scope of virtual accounts.</span></span>
> <span data-ttu-id="9b850-123">Cada usuário conectado compartilha a mesma identidade de gMSA, que pode ter permissões em toda a empresa.</span><span class="sxs-lookup"><span data-stu-id="9b850-123">Every connecting user will share the same gMSA identity, which may have permissions across your entire enterprise.</span></span> <span data-ttu-id="9b850-124">Tenha muito cuidado ao optar por usar uma gMSA, e sempre prefira contas virtuais que são limitadas no computador local, quando possível.</span><span class="sxs-lookup"><span data-stu-id="9b850-124">Be very careful when selecting to use a gMSA, and always prefer virtual accounts which are limited to the local machine when possible.</span></span>

## <a name="conditional-access-policies"></a><span data-ttu-id="9b850-125">Políticas de acesso condicional</span><span class="sxs-lookup"><span data-stu-id="9b850-125">Conditional access policies</span></span>

<span data-ttu-id="9b850-126">O JEA é excelente para limitar o que alguém pode fazer quando ele se conecta a um sistema para gerenciá-lo, mas e se você também desejar limitar *quando* alguém pode usar JEA?</span><span class="sxs-lookup"><span data-stu-id="9b850-126">JEA is great at limiting what someone can do when they've connected to a system to manage it, but what if you also want to limit *when* someone can use JEA?</span></span> <span data-ttu-id="9b850-127">Adicionamos opções de configuração aos arquivos de configuração de sessão (.pssc) para permitir que você especifique grupos de segurança aos quais um usuário deve pertencer para estabelecer uma sessão JEA.</span><span class="sxs-lookup"><span data-stu-id="9b850-127">We have added configuration options into the session configuration files (.pssc) to let you specify security groups to which a user must belong in order to establish a JEA session.</span></span> <span data-ttu-id="9b850-128">Isso é especialmente útil se você tiver um sistema JIT (Just In Time) em seu ambiente e quiser que os usuários elevem os próprios privilégios antes de acessar um ponto de extremidade JEA altamente privilegiado.</span><span class="sxs-lookup"><span data-stu-id="9b850-128">This is especially helpful if you have a Just In Time (JIT) system in your environment, and want to make your users elevate their privileges before accessing a highly-privileged JEA endpoint.</span></span>

<span data-ttu-id="9b850-129">O novo campo *RequiredGroups* no arquivo de PSSC permite que você especifique a lógica para determinar se um usuário pode se conectar ao JEA.</span><span class="sxs-lookup"><span data-stu-id="9b850-129">The new *RequiredGroups* field in the PSSC file allows you to specify the logic to determine if a user can connect to JEA.</span></span> <span data-ttu-id="9b850-130">Ele consiste em especificar uma tabela de hash (opcionalmente aninhada) que usa as chaves 'E' e 'Ou' para construir as regras.</span><span class="sxs-lookup"><span data-stu-id="9b850-130">It consists of specifying a hashtable (optionally nested) that uses the 'And' and 'Or' keys to construct your rules.</span></span> <span data-ttu-id="9b850-131">Veja alguns exemplos de como utilizar esse campo:</span><span class="sxs-lookup"><span data-stu-id="9b850-131">Here are some examples of how to use this field:</span></span>

```powershell
# Example 1: Connecting users must belong to a security group called "elevated-jea"
RequiredGroups = @{ And = 'elevated-jea' }

# Example 2: Connecting users must have signed on with 2 factor authentication or a smart card
# The 2 factor authentication group name is "2FA-logon" and the smart card group name is "smartcard-logon"
RequiredGroups = @{ Or = '2FA-logon', 'smartcard-logon' }

# Example 3: Connecting users must elevate into "elevated-jea" with their JIT system and have logged on with 2FA or a smart card
RequiredGroups = @{ And = 'elevated-jea', @{ Or = '2FA-logon', 'smartcard-logon' }}
```

## <a name="fixed-virtual-accounts-are-now-supported-on-windows-server-2008-r2"></a><span data-ttu-id="9b850-132">Corrigido: contas virtuais agora têm suporte no Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="9b850-132">Fixed: Virtual accounts are now supported on Windows Server 2008 R2</span></span>

<span data-ttu-id="9b850-133">No WMF 5.1, agora você poderá usar contas virtuais no Windows Server 2008 R2, permitindo configurações consistentes e paridade de recursos entre o Windows Server 2008 R2 - 2016.</span><span class="sxs-lookup"><span data-stu-id="9b850-133">In WMF 5.1, you are now able to use virtual accounts on Windows Server 2008 R2, enabling consistent configurations and feature parity across Windows Server 2008 R2 - 2016.</span></span> <span data-ttu-id="9b850-134">Contas virtuais permanecem sem suporte ao usar JEA no Windows 7.</span><span class="sxs-lookup"><span data-stu-id="9b850-134">Virtual accounts remain unsupported when using JEA on Windows 7.</span></span>