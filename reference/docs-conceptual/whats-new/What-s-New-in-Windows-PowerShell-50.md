---
ms.date: 06/05/2017
keywords: powershell, cmdlet
title: Novidades sobre o Windows PowerShell 5.0
ms.openlocfilehash: d86c9c947c521e0aee261a8a0335f1557b0d5a34
ms.sourcegitcommit: 4a2cf30351620a58ba95ff5d76b247e601907589
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71325131"
---
# <a name="whats-new-in-windows-powershell-50"></a>Novidades sobre o Windows PowerShell 5.0

O Windows PowerShell 5.0 inclui recursos novos importantes que estendem e melhoram o uso, bem como permitem controlar e gerenciar ambientes baseados no Windows de forma mais fácil e abrangente.

O Windows PowerShell 5.0 é compatível com versões anteriores. Cmdlets, provedores, módulos, snap-ins, scripts, funções e perfis projetados para o Windows PowerShell 4.0, o Windows PowerShell 3.0 e o Windows PowerShell 2.0 geralmente funcionam no Windows PowerShell 5.0 sem alterações.

## <a name="installing-windows-powershell"></a>Instalar o Windows PowerShell

O Windows PowerShell 5.0 está instalado por padrão no Windows Server 2016 Technical Preview e Windows 10.

Para instalar o Windows PowerShell 5.0 em Windows Server 2012 R2, Windows 8.1 Enterprise ou Windows 8.1 Pro, baixe e instale o [Windows Management Framework 5.0](https://aka.ms/wmf5download). Certifique-se de ler os detalhes de download e atender a todos os requisitos de sistema antes de instalar o Windows Management Framework 5.0.

## <a name="in-this-topic"></a>Neste tópico

- [Atualizações do Windows PowerShell 4.0 DSC na KB 3000850](#windows-powershell-40-updates-in-november-2014-update-rollup-kb-3000850)
- [Novos recursos no Windows PowerShell 5.0](#new-features-in-windows-powershell-50)
- [Novos recursos no Windows PowerShell 4.0](#new-features-in-windows-powershell-40)
- [Novos recursos no Windows PowerShell 3.0](#new-features-in-windows-powershell-30)

## <a name="windows-powershell-40-updates-in-november-2014-update-rollup-kb-3000850"></a>Atualizações do Windows PowerShell 4.0 no pacote cumulativo de atualizações de novembro de 2014 (KB 3000850)

Muitas atualizações e aprimoramentos para a DSC (Configuração de Estado Desejado) do Windows PowerShell no Windows PowerShell 4.0 estão disponíveis no [pacote cumulativo de atualizações de novembro de 2014 para o Windows RT 8.1, Windows 8.1 e Windows Server 2012 R2](https://support.microsoft.com/kb/3000850/) (KB 3000850). Você pode determinar se o KB 3000850 está instalado no sistema executando o `Get-Hotfix -Id KB3000850` no Windows PowerShell.

- Atualizações para os cmdlets existentes no módulo [PSDesiredStateConfiguration](https://technet.microsoft.com/library/dn391651(v=wps.640).aspx)
  - O [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) é mais rápido (especialmente no ISE).
  - [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) tem um novo parâmetro, -UseExisting, que reaplica a última configuração aplicada.
  - [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) -Force foi corrigido.
  - [Get-DscLocalConfigurationManager](https://technet.microsoft.com/library/dn407378.aspx) exibe informações mais úteis sobre o estado do mecanismo.
  - [Test-DscConfiguration](https://technet.microsoft.com/library/dn407382.aspx) agora retorna o nome do computador com True ou False.
  - [New-DscChecksum](https://technet.microsoft.com/library/dn521622.aspx) agora dá suporte a caminhos UNC.

- Novos cmdlets no módulo [PSDesiredStateConfiguration](https://technet.microsoft.com/library/dn391651(v=wps.640).aspx)
  - [Update-DscConfiguration](https://technet.microsoft.com/library/mt143541(v=wps.630).aspx):  executa uma verificação do servidor de pull sob demanda.
  - [Stop-DscConfiguration](https://technet.microsoft.com/library/mt143542(v=wps.630).aspx):  interrompe uma configuração que já está em execução.
  - [Remove-DscConfigurationDocument](https://technet.microsoft.com/library/mt143544(v=wps.630).aspx):  permite que você remova documentos de configuração em vários estágios (pendentes, anteriores ou atuais).

- Aprimoramentos de linguagem
  - DependsOn agora dá suporte a recursos de composição.
  - DependsOn agora dá suporte a números nos nomes de instância do recurso.
  - Expressões de nó avaliadas como vazias não geram mais erros.
  - Um erro que ocorrerá se uma expressão de nó que foi avaliada como vazia for corrigida.
  - Configurações que chamam configurações agora funcionam no console do Windows PowerShell.

- Aprimoramentos do modo de pull
  - O modo pull agora dá suporte a todos os arquivos ZIP.
  - **AllowModuleOverwrite** agora funciona corretamente.

- Aprimoramentos de resiliência
  - O novo **DebugMode** permite recarregar módulos de recursos.
  - Se ocorrer uma falha de configuração, o arquivo pending.mof não será excluído.
  - O LCM (Gerenciador de Configurações Local) agora está mais resiliente quando as definições de metaconfiguração são corrompidas.

- Melhorias de diagnóstico
  - Um aviso é exibido quando o LCM define o temporizador para diferentes configurações que você especificou.
  - Os arquivos de log de erros agora contém a pilha de chamadas de recursos do Windows PowerShell.

- Aprimoramentos de flexibilidade
  - O recurso LocalConfigurationManager tem uma nova propriedade, **ActionAfterReboot**.
    - ContinueConfiguration (valor padrão): retoma automaticamente uma configuração depois que um nó de destino é reiniciado.
    - StopConfiguration: não retoma automaticamente uma configuração depois que um nó é reiniciado.
  - Uma execução de consistência agora pode ocorrer com mais frequência do que uma operação PULL ou vice-versa.
  - Suporte a controle de versão:  agora, o DSC pode reconhecer um documento que foi gerado em um cliente mais recente (incluído no [WMF 5.0](https://aka.ms/wmf5download)).

- Aprimoramentos de prevenção de erro
  - A versão do módulo é aplicada antes de uma configuração ser aplicada.
  - **DebugPreference** agora está definido corretamente para chamadas Get-, Set- ou Test-TargetResource.

- Melhorias de manipulação de credenciais
  - Um certificado agora será usado se ambos os **Certificate** e **PSDscAllowPlainTextPassword** forem especificados.
  - As credenciais são descriptografadas, até mesmo para Get-TargetResource.
  - As credenciais de metaconfiguração são criptografadas e descriptografadas.
  - PSCredentials agora são descriptografados quando estão em um objeto inserido.

- Aprimoramentos de recursos internos
  - O recurso do pacote
    - Não instala o pacote errado (do local ou da fontes da Web).
    - Agora dá suporte a HTTPS.
  - Agora há suporte para HTTPS no [Recursos do pacote](https://technet.microsoft.com/library/dn282132.aspx).
  - O [recurso do arquivo](https://technet.microsoft.com/library/dn249917.aspx) agora dá suporte a credenciais.

## <a name="new-features-in-windows-powershell-50"></a>Novos recursos no Windows PowerShell 5.0

- [Novos recursos no Windows PowerShell](#new-features-in-windows-powershell)
- [Novos recursos na Configuração de Estado Desejado do Windows PowerShell](#new-features-in-windows-powershell-desired-state-configuration)
- [Novos recursos no ISE do Windows PowerShell](#new-features-in-windows-powershell-ise)
- [Novos recursos nos Serviços Web do Windows PowerShell](#new-features-in-windows-powershell-web-services-management-odata-iis-extension)
- [Correções de bugs importantes no Windows PowerShell 5.0](#notable-bug-fixes-in-windows-powershell-50)

### <a name="new-features-in-windows-powershell"></a>Novos recursos no Windows PowerShell

- No Windows PowerShell 5.0, você pode desenvolver usando classes, usando sintaxe formal e semântica semelhantes a outras linguagens de programação orientadas a objeto. **Class**, **Enum** e outras palavras-chave foram adicionadas à linguagem do Windows PowerShell para dar suporte ao novo recurso. Para obter mais informações sobre como trabalhar com classes, consulte about_Classes.

- O Windows PowerShell 5.0 introduz um fluxo de informações novo e estruturado que pode ser usado para transmitir dados estruturados entre um script e seus chamadores (ou ambiente de hospedagem). Agora você pode usar o Write-Host para emitir a saída para o fluxo de informações. Fluxos de informações também funcionam para PowerShell.Streams, trabalhos, trabalhos agendados e fluxos de trabalho. Os recursos a seguir dão suporte ao fluxo de informações.
  - Um novo cmdlet Write-Information permite especificar como o Windows PowerShell lida com dados de fluxo de informações para um comando. Write-Host é um wrapper para Write-Information. Write-Information também é uma atividade de fluxo de trabalho com suporte.
  - Dois novos parâmetros comuns, InformationVariable e InformationAction, permitem determinar como os fluxos de informações de um comando são exibidos. Os valores válidos para InformationAction são SilentlyContinue, Stop, Continue, Inquire, Ignore ou Suspend, com SilentlyContinue sendo o padrão. InformationVariable especifica uma cadeia de caracteres como o nome de uma variável na qual você deseja que os dados de Write-Host de um comando sejam salvos.
  - Uma nova variável de preferência, InformationPreference, especifica sua preferência padrão para dados de fluxo de informações em uma sessão do Windows PowerShell. O valor padrão é SilentlyContinue.
  - Dois novos parâmetros comuns de fluxo de trabalho, PSInformation e InformationAction, foram adicionados.
  - Quando você usa o comando Format-Table, colunas de tabela agora são formatadas automaticamente avaliando os primeiros 300 ms de dados que passam pelo fluxo.

- Em colaboração com o [Microsoft Research](https://research.microsoft.com/), um novo cmdlet, ConvertFrom-String, foi adicionado. ConvertFrom-String permite extrair e analisar objetos estruturados do conteúdo de cadeias de caracteres de texto. Para obter mais informações, consulte ConvertFrom-String.
- Um novo cmdlet Convert-String formata automaticamente o texto com base em um exemplo que você fornecer em um parâmetro -Example.
- Um novo módulo, o Microsoft.PowerShell.Archive, inclui cmdlets que permitem compactar arquivos e pastas em arquivos compactados (também conhecido como ZIP), extrair arquivos de arquivos ZIP existentes e atualizar arquivos ZIP com versões mais recentes dos arquivos compactados neles.
- Um novo módulo, PackageManagement, permite descobrir e instalar pacotes de software na Internet. O módulo PackageManagement (conhecido anteriormente como OneGet) é um gerenciador ou multiplexador de gerenciadores de pacotes existentes (também chamados de provedores de pacote) que unifica o gerenciamento de pacotes do Windows com uma única interface do Windows PowerShell.
- Um novo módulo, PowerShellGet, permite localizar, instalar, publicar e atualizar módulos e recursos de DSC na [Galeria do PowerShell](https://www.powershellgallery.com/) ou em um repositório de módulos interno que você pode configurar executando o cmdlet Register-PSRepository.
- Uma nova palavra-chave de linguagem, **Hidden**, foi adicionada para especificar que um membro (uma propriedade ou um método) não é exibido por padrão nos resultados de Get-Member (a menos que você adicione o parâmetro -Force). Propriedades ou métodos que foram marcados como ocultos também não aparecem nos resultados do IntelliSense, a menos que você esteja em um contexto em que o membro deve ser visível; por exemplo, a variável automática $This deve mostrar membros ocultos no método da classe.
- New-Item, Remove-Item e Get-ChildItem foram aprimorados para dar suporte à criação e ao gerenciamento de [links simbólicos](https://en.wikipedia.org/wiki/Symbolic_link). O parâmetro **ItemType** para New-Item aceita um novo valor, **SymbolicLink**. Agora, é possível criar links simbólicos em uma única linha simples com o cmdlet New-Item.
- Get-ChildItem também tem um novo parâmetro, -Depth, que você pode usar com o parâmetro -Recurse para limitar a recursão. Por exemplo, Get-ChildItem -Recurse -Depth 2 retorna resultados da pasta atual, todas as pastas filho dentro da pasta atual e todas as pastas dentro das pastas filho.
- Copy-Item agora permite copiar arquivos ou pastas de uma sessão do Windows PowerShell para outra, o que significa que você pode copiar arquivos para sessões que estão conectadas a computadores remotos (incluindo computadores que executam o [Windows Nano Server](https://blogs.technet.com/b/windowsserver/archive/2015/04/08/microsoft-announces-nano-server-for-modern-apps-and-cloud.aspx) e, portanto, não têm nenhuma outra interface). Para copiar os arquivos, especifique as IDs de PSSession como o valor dos novos parâmetros -FromSession e -ToSession e adicione -Path e -Destination para especificar o caminho de origem e o destino, respectivamente. Por exemplo, Copy-Item -Path c:\\myFile.txt -ToSession $s -Destination d:\\destinationFolder.
- A transcrição do Windows PowerShell foi aperfeiçoada para ser aplicada a todos os aplicativos de hospedagem (como o ISE do Windows PowerShell), além do host do console (**powershell.exe**). As opções de transcrição (incluindo a habilitação de uma transcrição geral do sistema) podem ser configuradas habilitando a configuração Política de Grupo de **Ativar Transcrição do PowerShell** encontrada em Modelos Administrativos/Componentes do Windows/Windows PowerShell.
- O novo recurso de rastreamento de script detalhado permite habilitar o acompanhamento detalhado e a análise de uso de scripts do Windows PowerShell em um sistema. Depois de habilitar o rastreamento de script detalhado, o Windows PowerShell registra em log todos os blocos de script no log de eventos do ETW (Rastreamento de Eventos para Windows), **Microsoft-Windows-PowerShell/Operational**.
- No Windows PowerShell 5.0 os cmdlets da Sintaxe de Mensagem Criptografada dão suporte à criptografia e decriptografia de conteúdo usando o formato padrão da IETF para proteger as mensagens criptograficamente, conforme documentado pelo [RFC5652](https://tools.ietf.org/html/rfc5652). Os cmdlets Get-CmsMessage, Protect-CmsMessage e Unprotect-CmsMessage foram adicionados ao módulo [Microsoft.PowerShell.Security](https://technet.microsoft.com/library/hh849807.aspx).
- Os novos cmdlets no módulo do [Microsoft.PowerShell.Utility](https://technet.microsoft.com/library/hh849958.aspx), Get-Runspace, Debug-Runspace, Get-RunspaceDebug, Enable-RunspaceDebug e Disable-RunspaceDebug, permitem definir opções de depuração em um runspace e iniciar e parar a depuração em um runspace. Para depurar runspaces arbitrários (isto é, runspaces que não são o runspace padrão para um console do Windows PowerShell ou uma sessão do ISE do Windows PowerShell), o Windows PowerShell permite definir pontos de interrupção em um script e, tendo adicionado pontos de interrupção, impede que o script seja executado até que você possa anexar um depurador para depurar o script de runspace. Suporte à depuração aninhada de runspaces arbitrários foi adicionado ao depurador de script do Windows PowerShell para runspaces.
- Um novo cmdlet Format-Hex foi adicionado ao módulo [Microsoft.PowerShell.Utility](https://technet.microsoft.com/library/hh849958.aspx). Format-Hex permite exibir texto ou dados binários em formato hexadecimal.
- Os cmdlets Get-Clipboard e Set-Clipboard foram adicionados ao módulo [Microsoft.PowerShell.Utility](https://technet.microsoft.com/library/hh849958.aspx); eles facilitam a transferência de conteúdo de e para uma sessão do Windows PowerShell. Os cmdlets Clipboard dão suporte a imagens, arquivos de áudio, listas de arquivo e texto.
- Um novo cmdlet, Clear-RecycleBin, foi adicionado ao módulo [Microsoft.PowerShell.Management](https://technet.microsoft.com/library/hh849827(v=wps.640).aspx); esse cmdlet esvazia a Lixeira de uma unidade fixa, incluindo unidades externas. Por padrão, você é solicitado a confirmar um comando Clear-RecycleBin, pois a propriedade ConfirmImpact do cmdlet é definida como ConfirmImpact.High.
- Um novo cmdlet, New-TemporaryFile, permite criar um arquivo temporário como parte do script. Por padrão, o novo arquivo temporário é criado em ```C:\Users\<user name>\AppData\Local\Temp```.
- Os cmdlets Out-File, Add-Content e Set-Content agora têm um novo parâmetro -NoNewline, que omite uma nova linha após a saída.
- O cmdlet New-Guid aproveita a nova classe Guid do .NET Framework para gerar um GUID, o que é útil quando você está escrevendo scripts ou recursos de DSC.
- Como as informações de versão de arquivo podem ser enganosas, principalmente depois que um arquivo é corrigido, novas propriedades de script FileVersionRaw e ProductVersionRaw estão disponíveis para os objetos FileInfo. Por exemplo, você pode executar o comando a seguir para exibir os valores dessas propriedades para powershell.exe, em que $pid contém a ID de processo para uma sessão em execução do Windows PowerShell: ```Get-Process -Id $pid -FileVersionInfo | Format-List *version* -Force```
- Os novos cmdlets Enter-PSHostProcess e Exit-PSHostProcess permitem depurar scripts do Windows PowerShell em processos separados do processo atual que está sendo executado no console do Windows PowerShell. Execute Enter-PSHostProcess para inserir ou anexar a uma ID de processo específica, em seguida, execute Get-Runspace para retornar os runspaces ativos dentro do processo. Execute Exit-PSHostProcess para desanexar do processo quando tiver terminado de depurar o script dentro do processo.
- Um novo cmdlet Wait-Debugger foi adicionado ao módulo [Microsoft.PowerShell.Utility](https://technet.microsoft.com/library/hh849958.aspx). Você pode executar o Wait-Debugger para interromper um script no depurador antes de executar a próxima instrução no script.
- O depurador de fluxo de trabalho do Windows PowerShell agora dá suporte ao preenchimento com Tab ou comando e você pode depurar funções de fluxo de trabalho aninhadas. Você agora pode pressionar **Ctrl+Break** para inserir o depurador em um script em execução, em sessões tanto locais quanto remotas, e em um script de fluxo de trabalho.
- Um cmdlet de Debug-Job foi adicionado ao módulo [Microsoft.PowerShell.Core](https://technet.microsoft.com/library/hh849695.aspx) para depurar a execução de scripts de trabalho para o Fluxo de Trabalho do Windows PowerShell, a tela de fundo e trabalhos em execução em sessões remotas.
- Um novo estado, AtBreakpoint, foi adicionado a trabalhos do Windows PowerShell. O estado AtBreakpoint aplica-se quando um trabalho está executando um script que inclui definir pontos de interrupção e o script atingiu um ponto de interrupção. Quando um trabalho é interrompido em um ponto de interrupção de depuração, você deve depurar o trabalho executando o cmdlet Debug-Job.
- O Windows PowerShell 5.0 implementa o suporte a várias versões de um único módulo do Windows PowerShell na mesma pasta em $PSModulePath. Uma propriedade RequiredVersion foi adicionada à classe ModuleSpecification para ajudar a que obter a versão desejada de um módulo; essa propriedade é mutuamente exclusiva com relação à propriedade ModuleVersion. Agora há suporte para RequiredVersion como parte do valor do parâmetro FullyQualifiedName dos cmdlets Get-Module, Import-Module e Remove-Module.
- Agora é possível realizar a validação da versão do módulo executando o cmdlet Test-ModuleManifest.
- Resultados do cmdlet Get-Command agora exibem uma coluna Version; uma nova propriedade Version foi adicionada à classe CommandInfo. Get-Command mostra os comandos de várias versões do mesmo módulo. A propriedade Version também faz parte de classes derivadas de CmdletInfo: CmdletInfo e ApplicationInfo.
- Get-Command tem um novo parâmetro, -ShowCommandInfo, que retorna informações de ShowCommand como PSObjects. Essa é uma funcionalidade especialmente útil quando Show-Command é executado no ISE do Windows PowerShell usando a comunicação remota do Windows PowerShell. O parâmetro -ShowCommandInfo substitui a função Get-SerializedCommand existente no módulo Microsoft.PowerShell.Utility, mas o script Get-SerializedCommand ainda está disponível para dar suporte a scripts de nível inferior.
- Um novo cmdlet Get-ItemPropertyValue permite obter o valor de uma propriedade sem usar a notação de ponto. Por exemplo, nas versões mais antigas do Windows PowerShell, você pode executar o comando a seguir para obter o valor da propriedade Base do Aplicativo da chave do Registro do PowerShellEngine: **(Get-ItemProperty -Path HKLM:\\SOFTWARE\\Microsoft\\PowerShell\\3\\PowerShellEngine -Name ApplicationBase).ApplicationBase**. No Windows PowerShell 5.0, você pode executar **Get-ItemPropertyValue -Path HKLM:\\SOFTWARE\\Microsoft\\PowerShell\\3\\PowerShellEngine -Name ApplicationBase**.
- Agora, o console do Windows PowerShell usa da coloração de sintaxe, assim como o ISE do Windows PowerShell.
- O novo módulo NetworkSwitch contém cmdlets que permitem habilitar a configuração de comutador, VLAN (LAN virtual) e porta de comutador de rede de Camada 2 básica a comutadores de rede certificados com o logotipo Windows Server 2012 R2.
- O parâmetro FullyQualifiedName foi adicionado aos cmdlets Import-Module e Remove-Module para dar suporte ao armazenamento de várias versões de um único módulo.
- Save-Help, Update-Help, Import-PSSession, Export-PSSession e Get-Command têm um novo parâmetro, FullyQualifiedModule, do tipo ModuleSpecification. Adicione este parâmetro para especificar um módulo pelo nome totalmente qualificado.
- O valor de **$PSVersionTable.PSVersion** foi atualizado para 5.0.
- O WMF 5.0 (PowerShell 5.0) inclui o módulo **Pester**.  O Pester é uma estrutura de teste de unidade para o PowerShell. Ele fornece algumas palavras-chave simples de usar que permitem criar testes para seus scripts.

### <a name="new-features-in-windows-powershell-desired-state-configuration"></a>Novos recursos na Configuração de Estado Desejado do Windows PowerShell

- Os aprimoramentos de linguagem do Windows PowerShell permitem que você defina recursos da DSC (Configuração de Estado Desejado) do Windows PowerShell usando classes. Import-DscResource agora é uma palavra-chave realmente dinâmica; o Windows PowerShell analisa o módulo raiz do módulo especificado, pesquisando classes que contêm o atributo DscResource. Agora você pode usar classes para definir recursos de DSC, nos quais não é necessária um arquivo MOF nem uma subpasta DSCResource da pasta de módulo. Um arquivo de módulo do Windows PowerShell pode conter várias classes de recursos de DSC.
- Foi adicionado um novo parâmetro, ThrottleLimit, para os seguintes cmdlets no módulo PSDesiredStateConfiguration. Adicione o parâmetro ThrottleLimit para especificar o número de computadores de destino ou dispositivos nos quais você deseja que o comando trabalhe ao mesmo tempo.
  - Get-DscConfiguration
  - Get-DscConfigurationStatus
  - Get-DscLocalConfigurationManager
  - Restore-DscConfiguration
  - Test-DscConfiguration
  - Compare-DscConfiguration
  - Publish-DscConfiguration
  - Set-DscLocalConfigurationManager
  - Start-DscConfiguration
  - Update-DscConfiguration
- Com os relatórios de erro centralizados de DSC, as informações de erros não são registradas apenas no evento de log, mas podem ser enviadas para um local central para análise posterior. Você pode usar esse local central para armazenar os erros de configuração de DSC que ocorreram para qualquer servidor em seu ambiente. Depois que o servidor de relatório for definido na metaconfiguração, todos os erros serão enviados para o servidor de relatório e armazenados em um banco de dados. Você pode configurar essa funcionalidade independentemente de um nó de destino estar ou não configurado para receber as configurações de um servidor de pull.
- Aprimoramentos para o ISE do Windows PowerShell a fim de facilitar a criação de recursos de DSC. Agora você pode fazer o seguinte.
  - Liste todos os recursos de DSC dentro de um bloco de **configuração** ou de **nó** inserindo **Ctrl+Espaço** em uma linha em branco no bloco.
  - O preenchimento automático das propriedades de recurso é do tipo **enumeração**.
  - O preenchimento automático da propriedade **DependsOn** dos recursos DSC baseia-se em outras instâncias de recurso na configuração.
  - Preenchimento com tab dos valores de propriedade de recurso aprimorado.
- Agora um usuário pode executar um recurso em um conjunto específico de credenciais, adicionando o **PSDscRunAsCredential** a um bloco de nó de atributo. Por exemplo, PSDscRunAsCredential = Get-Credential Contoso\\DscUser. Essa funcionalidade é útil para criar configurações que executam o Windows Installer e instaladores executáveis, acessar o hive de Registro por usuário ou executar outras tarefas fora do contexto do usuário atual.
- Suporte a 32 bits (x86) adicionado à palavra-chave **Configuration**.
- O Windows PowerShell agora inclui suporte para ajuda personalizada para configurações da DSC, definidas pela adição de \[CmdletBinding()] à função de configuração gerada.
- Um novo atributo **DscLocalConfigurationManager** designa um bloco de configuração como uma metaconfiguração, que é usada para configurar o Gerenciador de Configurações Local da DSC. Esse atributo restringe uma configuração para que ela contenha somente os itens que configuram o Gerenciador de Configurações Local do DSC. Durante o processamento, essa configuração gera um arquivo \*.meta.mof que é enviado para os nós de destino apropriados executando o cmdlet Set-DscLocalConfigurationManager.
- Configurações parciais agora são permitidas no Windows PowerShell 5.0. É possível entregar documentos de configuração para um nó em fragmentos. Para que um nó receba vários fragmentos de um documento de configuração, o Gerenciador de Configurações Local do nó deve ser definido para especificar os fragmentos esperados
- Sincronização entre computadores é a novidade na DSC no Windows PowerShell 5.0. Com os recursos internos WaitFor\* (**WaitForAll**, **WaitForAny** e **WaitForSome**), agora é possível especificar dependências entre computadores durante execuções de configuração, sem a orquestração externa. Estes recursos fornecem sincronização de nó para nó usando conexões CIM por meio do protocolo WS-Man. Uma configuração pode esperar que o estado de recurso específico de outro computador mude.
- JEA (Just Enough Administration), um novo recurso de segurança de delegação, aproveita a DSC e os runspaces restritos do Windows PowerShell para ajudar a proteger as empresas contra perda de dados ou o comprometimento pelos funcionários, intencional ou não. Para obter mais informações sobre o JEA, incluindo onde você pode baixar o recurso xJEA DSC, consulte [Just Enough Administration passo a passo](https://blogs.technet.com/b/privatecloud/archive/2014/05/14/just-enough-administration-step-by-step.aspx).
- Os seguintes cmdlets novos foram adicionados ao módulo PSDesiredStateConfiguration.
  - Um novo cmdlet Get-DscConfigurationStatus obtém informações gerais sobre o status de configuração de um nó de destino. Você pode obter o status do última ou de todas as configurações.
  - Um novo cmdlet Compare-DscConfiguration compara uma configuração especificada com o estado real de um ou mais nós de destino.
  - Um cmdlet Publish-DscConfiguration copia um arquivo MOF de configuração em um nó de destino, mas não aplica a configuração. A configuração é aplicada durante a próxima passagem de consistência ou na execução do cmdlet Update-DscConfiguration.
  - Um novo cmdlet Test-DscConfiguration permite que você verifique se uma configuração resultante corresponde à configuração desejada, retornando True se a configuração corresponder à configuração desejada ou False se a configuração real não coincidir com a configuração desejada.
  - Um novo cmdlet Update-DscConfiguration força uma configuração a ser processada. Se o Gerenciador de Configurações Local estiver no modo pull, o cmdlet obterá a configuração do servidor pull antes de aplicá-la.

### <a name="new-features-in-windows-powershell-ise"></a>Novos recursos no ISE do Windows PowerShell

- Agora, você pode editar scripts e arquivos remotos do Windows PowerShell em uma cópia local do ISE do Windows PowerShell, executando Enter-PSSession para iniciar uma sessão remota no computador que está armazenando os arquivos que você quer editar e executando **PSEdit \<caminho e nome do arquivo no computador remoto\>** . Esse recurso facilita a edição de arquivos Windows PowerShell que são armazenados na opção de instalação Server Core do Windows Server, em que o ISE do Windows PowerShell não pode ser executado.
- Agora há suporte para o cmdlet Start-Transcript no ISE do Windows PowerShell.
- Agora você pode depurar scripts remotos no ISE do Windows PowerShell.
- Um novo comando de menu, **Interromper Tudo** (Ctrl+B), interrompe o depurador de scripts em execução local e remota.

### <a name="new-features-in-windows-powershell-web-services-management-odata-iis-extension"></a>Novos recursos nos Serviços Web do Windows PowerShell (Extensão do IIS do Management OData)

- Iniciando do Windows PowerShell 5.0, você pode gerar um conjunto de cmdlets do Windows PowerShell com base na funcionalidade exposta por um determinado ponto de extremidade de OData, executando o cmdlet Export-ODataEndpointProxy, encontrado no novo módulo [Microsoft.PowerShell.OdataUtils](https://technet.microsoft.com/library/dn818507(v=wps.640).aspx).

### <a name="notable-bug-fixes-in-windows-powershell-50"></a>Correções de bugs notáveis no Windows PowerShell 5.0

- O Windows PowerShell 5.0 inclui uma nova implementação de COM, que proporciona melhorias significativas no desempenho quando você estiver trabalhando com objetos COM. Para ver uma demonstração em vídeo do efeito, consulte [Com_Perf_Improvements](https://1drv.ms/1qu3UPZ).
- Foram feitas melhorias significativas de desempenho para o preenchimento com Tab na sessão do Windows PowerShell, reduzindo o tempo do preenchimento com Tab em quase 500 ms.

## <a name="new-features-in-windows-powershell-40"></a>Novos recursos no Windows PowerShell 4.0

O Windows PowerShell 4.0 é compatível com versões anteriores. Os cmdlets, provedores, módulos, snap-ins, scripts, funções e perfis que foram criados para o Windows PowerShell 3.0 e o Windows PowerShell 2.0 geralmente funcionam no Windows PowerShell 4.0 sem alterações.

O Windows PowerShell 4.0 está instalado por padrão no Windows 8.1 e no Windows Server 2012 R2. Para instalar o Windows PowerShell 4.0 no Windows 7 com SP1 ou Windows Server 2008 R2, baixe e instale o [Windows Management Framework 4.0](https://www.microsoft.com/download/details.aspx?id=40855). Certifique-se de ler os detalhes de download e atender a todos os requisitos de sistema antes de instalar o Windows Management Framework 4.0.

- [Novos recursos no Windows PowerShell](#new-features-in-windows-powershell-1)
- [Novos recursos no ISE (Ambiente de Script Integrado) do Windows PowerShell](#new-features-in-windows-powershell-integrated-scripting-environment-ise)
- [Novos recursos no fluxo de trabalho do Windows PowerShell](#new-features-in-windows-powershell-workflow)
- [Novos recursos nos Serviços Web do Windows PowerShell](#new-features-in-windows-powershell-web-services)
- [Novos recursos no Windows PowerShell Web Access](#new-features-in-windows-powershell-web-access)
- [Correções de bugs importantes no Windows PowerShell 4.0](#notable-bug-fixes-in-windows-powershell-40)

O Windows PowerShell 4.0 inclui os seguintes novos recursos.

### <a name="a-namenew-features-in-windows-powershell-1-new-features-in-windows-powershell"></a><a name="new-features-in-windows-powershell-1" />Novos recursos no Windows PowerShell

- A **DSC (Configuração de Estado Desejado) do Windows PowerShell** é uma nova plataforma de gerenciamento no Windows PowerShell 4.0 que permite a implantação e o gerenciamento de dados de configuração de serviços de software e o ambiente no qual esses serviços são executados. Para obter mais informações sobre o DSC, consulte [Introdução à Configuração de Estado Desejado do Windows PowerShell](https://technet.microsoft.com/library/c134aa32-b085-4656-9a89-955d8ff768d0).
- **Save-Help** agora permite salvar ajuda para módulos instalados em computadores remotos. Você pode usar Save-Help para baixar o módulo da Ajuda de um cliente conectado à Internet (nos quais nem todos os módulos para o qual você deseja obter ajuda estão necessariamente instalados) e copiar a Ajuda salva em uma pasta compartilhada remota ou um computador remoto que não tem acesso à Internet.
- O depurador do Windows PowerShell foi aprimorado para permitir a depuração de fluxos de trabalho do Windows PowerShell, bem como scripts que são executados em computadores remotos. Os fluxos de trabalho do Windows PowerShell agora podem ser depurados no nível de script da linha de comando do Windows PowerShell ou do ISE do Windows PowerShell. Scripts do Windows PowerShell, incluindo fluxos de trabalho de script, agora podem ser depurados em sessões remotas. Sessões de depuração remota são salvas sobre as sessões remotas do Windows PowerShell, que são desconectadas e reconectadas posteriormente.
- Um parâmetro **RunNow** do **Register-ScheduledJob** e **Set-ScheduledJob** elimina a necessidade de definir uma data e hora de início imediato para trabalhos usando o parâmetro **Trigger**.
- **Invoke-RestMethod** e **Invoke-WebRequest** agora permitem definir todos os cabeçalhos usando o parâmetro Headers. Embora esse parâmetro sempre tenha existido, ele era um dos diversos parâmetros dos cmdlets Web que resultavam em erros ou exceções.
- **Get-Module** agora tem um novo parâmetro, o **FullyQualifiedName**, do tipo **ModuleSpecification\[]** . O parâmetro **FullyQualifiedName** do Get-Module agora permite especificar um módulo, usando o nome, a versão e, opcionalmente, o GUID do módulo.
- A configuração de política de execução padrão no Windows Server 2012 R2 é **RemoteSigned**. No Windows 8.1, não há nenhuma alteração da configuração padrão.
- No Windows PowerShell 4.0 há suporte para a invocação de método usando nomes de método dinâmico. Você pode usar uma variável para armazenar um nome de método e, em seguida, chamar o método dinamicamente ao chamar a variável.
- Trabalhos de fluxo de trabalho assíncrono não são mais excluídos quando o período de tempo limite especificado pelo parâmetro **PSElapsedTimeoutSec** comum de fluxo de trabalho é atingido.
- Um novo parâmetro, **RepeatIndefinitely**, foi adicionado aos cmdlets **New-JobTrigger** e **Set-JobTrigger**. Esse parâmetro elimina a necessidade de especificar um valor **TimeSpan.MaxValue** para o parâmetro **RepetitionDuration** para executar um trabalho agendado repetidamente por um período indefinido.
- Um parâmetro **Passthru** foi adicionado aos cmdlets **Enable-JobTrigger** e **Disable-JobTrigger**. O parâmetro Passthru exibe todos os objetos que são criados ou modificados por seu comando.
- Os nomes de parâmetro para especificar um grupo de trabalho nos cmdlets **Add-Computer** e **Remove-Computer** agora são consistentes. Ambos os cmdlets agora usam o parâmetro **WorkgroupName**.
- Um novo parâmetro comum, o **PipelineVariable**, foi adicionado. O PipelineVariable permite salvar os resultados de um comando canalizado (ou parte de um comando canalizado) como uma variável que pode ser passada através do restante do pipeline.
- Agora há suporte para a filtragem de coleta usando uma sintaxe de método. Isso significa que agora você pode filtrar uma coleção de objetos usando sintaxe simplificada, semelhante ao Where() ou Where-Object, formatada como uma chamada de método. Veja este exemplo: (Get-Process).where({$_.Name -match 'powershell'})
- O cmdlet **Get-Process** tem um novo parâmetro de opção, o **IncludeUserName**.
- Um novo cmdlet, o **Get-FileHash**, que retorna um hash de arquivo em vários formatos para um arquivo especificado, foi adicionado.
- No Windows PowerShell 4.0, se um módulo usar a chave **DefaultCommandPrefix** em seu manifesto ou se o usuário importar um módulo com o parâmetro **Prefix**, a propriedade **ExportedCommands** do módulo mostrará os comandos no módulo com o prefixo. Quando você executa os comandos usando a sintaxe qualificada por módulo, ModuleName\\CommandName, os nomes de comando devem incluir o prefixo.
- O valor de **$PSVersionTable.PSVersion** foi atualizado para 4.0.
- O comportamento do operador **Where()** foi alterado. Não há mais suporte para o `Collection.Where('property -match name')` aceitar uma expressão de cadeia de caracteres no formato `"Property -CompareOperator Value"`. No entanto, o operador **Where()** aceita expressões de cadeia de caracteres no formato de um scriptblock; ainda há suporte para isso.

### <a name="new-features-in-windows-powershell-integrated-scripting-environment-ise"></a>Novos recursos no Ambiente de Script Integrado (ISE) do Windows PowerShell

- O ISE do Windows PowerShell dá suporte a depuração de fluxo de trabalho do Windows PowerShell e depuração de script remoto.
- Foi adicionado suporte ao IntelliSense para as configurações e provedores de Configuração de Estado Desejado do Windows PowerShell.

### <a name="new-features-in-windows-powershell-workflow"></a>Novos recursos no Fluxo de Trabalho do Windows PowerShell

- Foi adicionado suporte a um novo parâmetro comum **PipelineVariable** no contexto de pipelines iterativos, como os usados pelo System Center Orchestrator, ou seja, pipelines que executam comandos simplesmente da esquerda para a direita, em vez de intercalados em execução usando streaming.
- A associação de parâmetros foi aprimorada significativamente para trabalhar fora de cenários de preenchimento de guias, como com os comandos que não existem no runspace atual.
- O suporte para atividades de contêiner personalizado foi adicionado ao fluxo de trabalho do Windows PowerShell. Se um parâmetro de atividade for dos tipos **Activity**, **Activity\[]** (ou for uma coleção genérica de atividades) e o usuário fornecer um bloco de script como argumento, o fluxo de trabalho do Windows PowerShell converterá o bloco de script para XAML, assim como na compilação de fluxo de trabalho para script normal do Windows PowerShell.
- Após uma falha, o fluxo de trabalho do Windows PowerShell se reconecta a nós gerenciados.
- Agora você pode restringir instruções da atividade **Foreach -Parallel** usando a propriedade **ThrottleLimit**.
- O parâmetro comum **ErrorAction** tem um novo valor válido, **Suspend**, que é exclusivo para fluxos de trabalho.
- Um ponto de extremidade do fluxo de trabalho agora fecha automaticamente se não houver nenhuma sessão ativa, nem trabalhos em andamento ou pendentes. Esse recurso preserva os recursos no computador que está atuando como servidor de fluxo de trabalho quando as condições de fechamento automático são atendidas.

### <a name="new-features-in-windows-powershell-web-services"></a>Novos recursos no Windows PowerShell Web Services

- Quando ocorre um erro nos PSWS (Serviços Web do Windows PowerShell, também chamado de Extensão do IIS do Management OData) durante a execução de um cmdlet, mais detalhes das mensagens de erro serão retornados ao chamador. Além disso, os códigos de erro seguem as [diretrizes de código de erro da API REST do Microsoft Azure](https://msdn.microsoft.com/library/windowsazure/dd179357.aspx).
- Um ponto de extremidade agora pode definir a versão da API, bem como impor o uso de uma versão específica de API. Sempre que ocorrer incompatibilidade de versão entre cliente e servidor, os erros são exibidos para o cliente e para o servidor.
- O gerenciamento do esquema de expedição foi simplificado ao gerar automaticamente valores para os campos ausentes no esquema. A geração ocorre, como ponto de partida útil, mesmo se o esquema de distribuição não existir.
- A manipulação de tipos no PSWS foi aprimorada para dar suporte aos tipos que usam um construtor diferente do construtor padrão, comportando-se da mesma forma que o **PSTypeConverter** no Windows PowerShell. Isso permite usar tipos complexos com o PSWS.
- O PSWS agora permite expandir uma instância associada ao executar uma consulta. Para grandes conteúdos binários (como imagens, áudio ou vídeo), o custo da transferência é significativo e é melhor transferir dados binários sem codificação. O PSWS usa fluxos de recurso nomeados para transferir sem codificação. O fluxo de recurso nomeado é uma propriedade de uma entidade do tipo **Edm.Stream**. Cada fluxo de recurso nomeado tem um URI separado para operações GET ou UPDATE.
- Agora, as ações de OData fornecem um mecanismo para invocar métodos de não-CRUD (criar, ler, atualizar e excluir) em um recurso. Você pode chamar uma ação enviando uma solicitação HTTP POST para o URI definido para a ação. Os parâmetros da ação são definidos no corpo da solicitação POST.
- Para ser consistente com as diretrizes do Microsoft Azure, todas as URLs devem ser simplificadas. Uma mudança incluída no **Key As Segment** permite que chaves únicas sejam representadas como segmentos. Observe que as referências que usam vários valores de chave exigem valores separados por vírgulas em notação entre parênteses, como antes.
- Antes desta versão do PSWS, a única maneira de realizar operações de Criar, Atualizar ou Excluir era invocar Postar, Colocar ou Excluir em um recurso de nível superior. Novidades nesta versão do PSWS incluem operações de recursos contidos que permitem aos usuários obter os mesmos resultados, atingindo o mesmo recurso menos diretamente, abordando como se esses recursos estivessem contidos.

### <a name="new-features-in-windows-powershell-web-access"></a>Novos recursos no Windows PowerShell Web Access

- Você pode se desconectar das sessões existentes, e se reconectar, no console baseado na Web do Windows PowerShell Web Access. Um botão **Salvar** no console baseado na Web permite desconectar-se de uma sessão sem excluí-la e reconectar-se à sessão outra vez.
- Os parâmetros padrão podem ser exibidos na página de entrada. Para exibir os parâmetros padrão, defina valores para todas as configurações exibidas na área da página de entrada **Configurações de Conexão Opcional** em um arquivo chamado **web.config**. Você pode usar o arquivo **web.config** para definir todas as configurações de conexão opcionais, exceto de um conjunto de credenciais alternativa ou secundário.
- No Windows Server 2012 R2, você pode gerenciar remotamente as regras de autorização do Windows PowerShell Web Access. Os cmdlets **Add-PswaAuthorizationRule** e **Test-PswaAuthorizationRule** agora incluem um parâmetro Credential que permite aos administradores gerenciar as regras de autorização de um computador remoto ou em uma sessão do Windows PowerShell Web Access.
- Agora você pode ter várias sessões do Windows PowerShell Web Access em uma única sessão de navegador usando uma nova guia do navegador para cada sessão. Você não precisa mais abrir uma nova sessão do navegador para se conectar a uma nova sessão no console baseado na Web do Windows PowerShell.

### <a name="notable-bug-fixes-in-windows-powershell-40"></a>Correções importantes no Windows PowerShell 4.0

- **Get-Counter** agora pode retornar os contadores que contêm um caractere apóstrofe em edições em francês do Windows.
- Agora você pode exibir o método **GetType** em objetos desserializados.
- A instrução **#Requires** agora permite que os usuários solicitem direitos de acesso de Administrador, se necessário.
- O cmdlet **Import-Csv** agora ignora linhas em branco.
- Foi corrigido um problema no qual o ISE do Windows PowerShell usava muita memória ao executar um comando **Invoke-WebRequest**.
- **Get-Module** agora exibe versões de módulo em uma coluna **Version**.
- Remove-Item -Recurse agora remove itens de subpastas conforme o esperado.
- Uma propriedade **UserName** foi adicionada aos objetos de saída de **Get-Process**.
- O cmdlet **Invoke-RestMethod** agora retorna todos os resultados disponíveis.
- **Add-Member** agora entra em vigor em tabelas de hash, mesmo que elas ainda não tenham sido acessadas.
- **Select-Object -Expand** não vai mais falhar nem gerar uma exceção se o valor da propriedade for nulo ou vazio.
- **Get-Process** agora pode ser usado em um pipeline com outros comandos que obtêm a propriedade **ComputerName** de objetos.
- **ConvertTo-Json** e **ConvertFrom-Json** agora podem aceitar termos entre aspas duplas e suas mensagens de erro agora são localizáveis.
- **Get-Job** agora retorna os trabalhos agendados concluídos, mesmo em novas sessões.
- Foram corrigidos problemas com a montagem e desmontagem de VHDs usando o provedor **FileSystem** no Windows PowerShell 4.0. Agora o Windows PowerShell é capaz de detectar novas unidades montados na mesma sessão.
- Você não precisa mais carregar explicitamente os módulos **ScheduledJob** ou **Workflow** para trabalhar com seus tipos de trabalho.
- Foram feitas melhorias no desempenho para o processo de importação de fluxos de trabalho que definem os fluxos de trabalho aninhados. Agora, esse processo é mais rápido.

## <a name="new-features-in-windows-powershell-30"></a>Novos recursos no Windows PowerShell 3.0

O Windows PowerShell 3.0 inclui os seguintes novos recursos.

- [Fluxo de trabalho do Windows PowerShell](#windows-powershell-workflow)
- [Windows PowerShell Web Access](#windows-powershell-web-access)
- [Novos recursos do ISE do Windows PowerShell](#new-windows-powershell-ise-features)
- [Suporte para o Microsoft .NET Framework 4.0](#support-for-microsoft-net-framework-4)
- [Suporte para o Ambiente de Pré-Instalação do Windows](#support-for-windows-preinstallation-environment)
- [Sessões desconectadas](#disconnected-sessions)
- [Conectividade robusta de sessão](#robust-session-connectivity)
- [Sistema de ajuda atualizável](#updatable-help-system)
- [Ajuda online avançada](#enhanced-online-help)
- [Integração do CIM](#cim-integration)
- [Arquivos de configuração de sessão](#session-configuration-files)
- [Integração do Agendador de Tarefas e trabalhos agendados](#scheduled-jobs-and-task-scheduler-integration)
- [Melhorias da linguagem do Windows PowerShell](#windows-powershell-language-enhancements)
- [Novos cmdlets principais](#new-core-cmdlets)
- [Aprimoramentos nos cmdlets e nos provedores principais existentes](#improvements-to-existing-core-cmdlets-and-providers)
- [Importação e descoberta de módulo remoto](#remote-module-import-and-discovery)
- [Preenchimento com Tab avançado](#enhanced-tab-completion)
- [Módulo de carregamento automático](#module-auto-loading)
- [Aprimoramentos da experiência do módulo](#module-experience-improvements)
- [Descoberta de comando simplificada](#simplified-command-discovery)
- [Suporte aprimorado a registro em log, a diagnósticos e à Política de Grupo](#improved-logging-diagnostics-and-group-policy-support)
- [Aprimoramentos de saída e de formatação](#formatting-and-output-improvements)
- [Experiência de host de console avançada](#enhanced-console-host-experience)
- [Novas APIs de cmdlet e de hospedagem](#new-cmdlet-and-hosting-apis)
- [Aprimoramentos de desempenho](#performance-improvements)
- [Suporte a Host Compartilhado e a Executar como](#runas-and-shared-host-support)
- [Aprimoramentos no tratamento de caracteres especiais](#special-character-handling-improvements)

### <a name="windows-powershell-workflow"></a>Fluxo de trabalho do Windows PowerShell

O fluxo de trabalho do Windows PowerShell traz a potência do Windows Workflow Foundation para o Windows PowerShell. Você pode escrever fluxos de trabalho em XAML ou na linguagem do Windows PowerShell e executá-los exatamente como você executaria um cmdlet. O cmdlet [Get-Command](https://technet.microsoft.com/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad) obtém comandos de fluxo de trabalho e o cmdlet [Get-Help](https://technet.microsoft.com/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a) obtém ajuda para fluxos de trabalho.

Fluxos de trabalho são sequências de atividades de gerenciamento demoradas, repetíveis, frequentes, frequentes, paralelizáveis, passível de interrupção, passível de suspensão e reiniciáveis. Fluxos de trabalho podem ser reiniciados com uma interrupção acidental ou intencional, como uma interrupção da rede, uma reinicialização do Windows ou uma falha de energia.

Os fluxos de trabalho também são migráveis, eles podem ser exportados ou importados como arquivos XAML. Você pode criar configurações de sessão personalizadas que permitem que o fluxo de trabalho ou atividades em um fluxo de trabalho sejam executados por usuários delegados ou subordinados.

A seguir estão os benefícios do fluxo de trabalho do Windows PowerShell

- Automação de tarefas sequenciadas de longa duração.
- **Monitoramento remoto de tarefas de execução longa**. O status e progresso das atividades são visíveis a qualquer momento.
- **Gerenciamento de vários computadores.** Executar tarefas como fluxos de trabalho simultaneamente em centenas de nós gerenciados. O Fluxo de Trabalho do Windows PowerShell inclui uma biblioteca integrada de parâmetros comuns de gerenciamento, como o **PSComputerName**, que permitem cenários de gerenciamento de vários computadores.
- **Execução de tarefa única de processos complexos.** Você pode combinar scripts relacionados que implementam um cenário inteiro ponta a ponta em um único fluxo de trabalho.
- **Persistência**: um fluxo de trabalho é salvo (ou verificado) em determinados pontos definidos por seu autor para que você possa retomar o fluxo de trabalho da última tarefa (ou ponto de verificação) persistida, em vez de reiniciá-lo desde o início.
- **Robustez.** Recuperação de falhas automatizada. Fluxos de trabalho sobrevivem a reinicializações planejadas e não planejadas. Você pode suspender a execução do fluxo de trabalho e depois retomar o fluxo de trabalho a partir do último ponto de persistência. Os autores de fluxo de trabalho podem designar atividades específicas para serem executadas novamente em caso de falha em um ou mais nós gerenciados.
- **Capacidade de desconectar, reconectar e executar em sessões desconectadas.** Os usuários podem se conectar e desconectar do servidor, mas o fluxo de trabalho permanece em execução. Saia do computador cliente ou reinicie-o e monitore a execução do fluxo de trabalho de outro computador sem interromper o fluxo de trabalho.
- **Agendamento.** As tarefas de fluxo de trabalho podem ser agendadas como qualquer cmdlet ou script Windows PowerShell.
- **Limitação de conexão e de fluxo de trabalho.** Execução de fluxo de trabalho e conexões para nós podem ser aceleradas, permitindo cenários de escalabilidade e alta disponibilidade.

### <a name="windows-powershell-web-access"></a>Windows PowerShell Web Access

O Windows PowerShell Web Access é um recurso do Windows Server 2012 que permite aos usuários executar comandos e scripts do Windows PowerShell em um console baseado na Web. Dispositivos que usam o console baseado na Web não exigem o Windows PowerShell, o software de gerenciamento remoto nem as instalações de plug-in de navegador. Basta um gateway do Windows PowerShell Web Access devidamente configurado e um navegador de dispositivo cliente que dê suporte a JavaScript e aceite cookies.

Para obter mais informações, consulte [Implantar o Windows PowerShell Web Access](https://go.microsoft.com/fwlink/p/?LinkID=221050).

### <a name="new-windows-powershell-ise-features"></a>Novos recursos do Windows PowerShell ISE

Para o Windows PowerShell 3.0, o ISE (Ambiente de Script Integrado) do Windows PowerShell tem muitos recursos novos, incluindo IntelliSense, janela Show-Command, um painel de console unificado, snippets, correspondência de colchetes, seções expandir-recolher, salvamento automático, lista de itens recentes, cópia avançada, cópia do bloco e suporte completo para escrever fluxos de trabalho de script do Windows PowerShell. Para obter mais informações, consulte [about_Windows_PowerShell_ISE [v3]](https://technet.microsoft.com/library/dfa54d47-60c6-4fff-8197-c747e8d411bb).

### <a name="support-for-microsoft-net-framework-4"></a>Suporte para o Microsoft .NET Framework 4

O Windows PowerShell foi desenvolvido com o Common Language Runtime 4.0. Autores de cmdlet, script e fluxo de trabalho podem usar as novas classes do Microsoft .NET Framework 4 no Windows PowerShell, com recursos que incluem a Implantação e Compatibilidade do Aplicativo, Managed Extensibility Framework, Computação Paralela, Rede, Windows Communication Foundation e Windows Workflow Foundation.

### <a name="support-for-windows-preinstallation-environment"></a>Suporte para o Ambiente de Pré-Instalação do Windows

O Windows PowerShell 3.0 é um componente opcional do Ambiente de Pré-Instalação do Windows (Windows PE) 4.0 para o Windows 8. O Windows PE é um sistema operacional mínimo que inicia um computador que não tem sistema operacional e o prepara para a instalação do Windows. O Windows PE pode ser usado para particionar e formatar discos rígidos, copiar imagens de disco para um computador e iniciar a Instalação do Windows por meio de um compartilhamento de rede. O Windows PowerShell 3.0 pode ser usado no Windows PE para gerenciar a implantação, diagnósticos e cenários de recuperação.

### <a name="disconnected-sessions"></a>Sessões desconectadas

A partir do Windows PowerShell 3.0, sessões persistentes gerenciadas pelo usuário ("PSSessions") que você cria usando o cmdlet New-PSSession são salvas no computador remoto. Elas não dependem mais da sessão na qual foram criadas.

Agora você pode desconectar-se de uma sessão sem interromper os comandos que são executados nela. Você pode fechar a sessão e desligar o computador. Posteriormente, você pode se reconectar à sessão de uma sessão diferente no mesmo computador ou em um computador diferente.

O parâmetro **ComputerName** do cmdlet [Get-PSSession](https://technet.microsoft.com/library/b2b10531-d0df-4746-b877-e75c09955cb6) agora obtém todas as sessões do usuário que se conectam ao computador, mesmo se elas foram iniciadas em uma sessão diferente em outro computador. Você pode se conectar às sessões, obter os resultados dos comandos, iniciar novos comandos e desconectar a sessão.

Foram adicionados novos cmdlets para dar suporte ao recurso de Sessões Desconectadas, incluindo [Disconnect-PSSession](https://technet.microsoft.com/library/f8f95111-612f-4cba-9098-77904b0473d8), [Connect-PSSession](https://technet.microsoft.com/library/b803dd29-f208-4079-80d4-db04d778f060) e Receive-PSSession, além de novos parâmetros adicionados aos cmdlets que gerenciam as PSSessions, como o parâmetro **InDisconnectedSession** do cmdlet [Invoke-Command](https://technet.microsoft.com/library/906b4b41-7da8-4330-9363-e7164e5e6970).

O recurso de sessões desconectadas é suportado apenas quando os computadores em ambas as extremidades de origem ("cliente") e de destino ("servidor") estão executando o Windows PowerShell 3.0.

### <a name="robust-session-connectivity"></a>Conectividade robusta de sessão

O Windows PowerShell 3.0 detecta perdas inesperadas de conectividade entre o cliente e servidor e tenta restabelecer a conectividade e retomar a execução automaticamente. Se a conexão entre o cliente e o servidor não puder ser restabelecida no tempo definido, o usuário será notificado e a sessão será desconectada. Durante a tentativa de reconexão, o Windows PowerShell fornece comentários contínuos para o usuário.

Se a sessão desconectada foi iniciada usando o InvokeCommand, o Windows PowerShell cria um trabalho para a sessão desconectada para tornar mais fácil a reconexão e retomar a execução.

Esses recursos fornecem uma experiência de comunicação remota mais confiável e recuperável, permitindo que os usuários executem tarefas de longa duração que exigem sessões robustas, como fluxos de trabalho.

### <a name="updatable-help-system"></a>Sistema de Ajuda Atualizável

Agora você pode baixar arquivos de Ajuda atualizados para os cmdlets nos seus módulos. O cmdlet [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) identifica os arquivos de ajuda mais recentes, baixa da Internet, descompacta, valida e instala eles no diretório específico do idioma correto para o módulo.

Para usar os arquivos de ajuda atualizados, basta digitar `Get-Help`. Não é necessário reiniciar o Windows ou o Windows PowerShell. Para atualizar a ajuda para os módulos no diretório $pshome, inicie o Windows PowerShell com a opção "Executar como administrador".

Para dar suporte a usuários que não têm acesso à Internet e usuários atrás de firewalls, o novo cmdlet [Save-Help](https://technet.microsoft.com/library/aed94f90-b73f-4e25-a25d-7c18d9f161fa) baixa os arquivos de ajuda para um diretório de sistema de arquivos, como um compartilhamento de arquivos. Os usuários poderão então usar o cmdlet [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) para obter os arquivos de ajuda atualizados no compartilhamento de arquivos.

Você pode usar o cmdlet [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) para atualizar os arquivos da ajuda para todos os módulos ou alguns específicos em todas a culturas de interface do usuário com suporte. Você pode até mesmo colocar um comando [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) no seu perfil do Windows PowerShell. Por padrão, o Windows PowerShell baixará os arquivos de ajuda de um módulo, no máximo, uma vez por dia.

Os módulos do Windows 8 e Windows Server 2012 não incluem arquivos de ajuda. Para baixar os arquivos de ajuda mais recentes, digite `Update-Help`. Para obter mais informações, digite `Get-Help` (sem parâmetros) ou consulte [About_Updatable_Help](https://technet.microsoft.com/library/10bba75c-f4ac-4ca1-bbf3-8f34dd521ffe).

Quando os arquivos de ajuda para um cmdlet não estão instalados no computador, o cmdlet [Get-Help](https://technet.microsoft.com/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a) agora exibe a ajuda gerada automaticamente. A Ajuda gerada automaticamente inclui a sintaxe de comando e instruções sobre como usar o cmdlet [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) para baixar arquivos de Ajuda.

Qualquer autor de módulo pode suportar a ajuda atualizável para seu módulo. Você pode incluir arquivos de Ajuda no módulo e usar a Ajuda Atualizável para atualizá-los ou omitir os arquivos da Ajuda e usar a Ajuda Atualizável para instalá-los. Para obter mais informações sobre como dar suporte à Ajuda Atualizável, consulte [Dar suporte à Ajuda Atualizável](https://go.microsoft.com/FWLink/?LinkID=242129) no MSDN.

### <a name="enhanced-online-help"></a>Ajuda Online Avançada

A ajuda online do Windows PowerShell é um recurso valioso para todos os usuários, mas é especialmente importante para usuários que não podem instalar os arquivos da ajuda atualizados.

Para obter ajuda online para qualquer cmdlet do Windows PowerShell, digite:

```
Get-Help <cmdlet-name> -Online
```

O Windows PowerShell abre a versão online do tópico da ajuda no navegador de Internet padrão.

O recurso **Get-Help -Online** no Windows PowerShell 3.0 é ainda mais potente, pois funciona mesmo quando os arquivos da ajuda para o cmdlet em questão não estão instalados no computador. O recurso **Get-Help -Online** obtém o URI para o tópico da ajuda online da propriedade HelpUri de cmdlets e funções avançadas.

```
PS C:\>(Get-Command Get-ScheduledJob).HelpUri
https://go.microsoft.com/fwlink/?LinkID=223923
```

Começando no Windows PowerShell 3.0, autores de cmdlets do C# podem preencher a propriedade **HelpUri** criando um atributo **HelpUri** na classe do cmdlet. Autores de funções avançadas podem definir uma propriedade **HelpUri** no atributo **CmdletBinding**. O valor da propriedade **HelpUri** deve começar com "http" ou "https".

Você também pode incluir um valor de **HelpUri** no primeiro link relacionado de um arquivo de ajuda do cmdlet baseado em XML ou a diretiva .Link de ajuda baseados em comentário em uma função.

Para obter mais informações sobre como dar suporte à ajuda online, confira [Dar suporte à Ajuda online](/powershell/developer/module/supporting-online-help) no Microsoft Docs.

### <a name="cim-integration"></a>Integração do CIM

O Windows PowerShell 3.0 inclui suporte para as informações do modelo CIM, que fornece definições comuns de informações de gerenciamento de sistemas, redes, aplicativos e serviços, permitindo a troca de informações de gerenciamento entre sistemas heterogêneos. O suporte para CIM no Windows PowerShell 3.0, incluindo a capacidade de criar cmdlets do Windows PowerShell com base em classes CIM novas ou existentes, comandos baseados em arquivos XML de definição de cmdlet e suporte para CIM .NET Framework. API, cmdlets de gerenciamento de CIM e provedores de WMI 2.0.

### <a name="session-configuration-files"></a>Arquivos de configuração de sessão

No Windows PowerShell 3.0 você pode criar uma configuração de sessão personalizada usando um arquivo. O arquivo de configuração da nova sessão permite determinar o ambiente de sessões que usam a configuração de sessão, incluindo quais módulos, scripts e formato de arquivos são carregados nas sessões, quais elementos de linguagem e cmdlets os usuários podem usar, quais módulos e scripts eles podem ser executar e quais variáveis podem ver.

Você pode criar uma sessão na qual os usuários podem executar apenas os cmdlets de um módulo específico ou uma sessão na qual os usuários têm acesso a scripts que executam tarefas avançadas, acesso a todos os módulos e todos os idiomas.

Nas versões anteriores do Windows PowerShell, o controle nesse nível estava disponível somente para aqueles que sabiam escrever um programa em C# ou um script de inicialização complexo. Agora, qualquer membro do grupo Administradores no computador pode personalizar uma configuração de sessão usando um arquivo de configuração.

Para criar um arquivo de configuração de sessão, use o cmdlet [New-PSSessionConfigurationFile](https://technet.microsoft.com/library/5f3e3633-6e90-479c-aea9-ba45a1954866). Para aplicar o arquivo de configuração de sessão a uma configuração de sessão, use os cmdlets [Register-PSSessionConfiguration](https://technet.microsoft.com/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea) ou [Set-PSSessionConfiguration](https://technet.microsoft.com/library/b21fbad3-1759-4260-b206-dcb8431cd6ea).

Para obter mais informações, consulte [about_Session_Configuration_Files](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_session_configuration_files?view=powershell-5.0) e [New-PSSessionConfigurationFile](https://technet.microsoft.com/library/5f3e3633-6e90-479c-aea9-ba45a1954866).

### <a name="scheduled-jobs-and-task-scheduler-integration"></a>Trabalhos Agendados e Integração do Agendador de Tarefas

Agora você pode agendar trabalhos em segundo plano do Windows PowerShell e gerenciá-los no Windows PowerShell e no Agendador de Tarefas.

Trabalhos agendados do Windows PowerShell são um híbrido útil entre trabalhos em segundo plano do Windows PowerShell e tarefas do Agendador de Tarefas.

Como os trabalhos em segundo plano do Windows PowerShell, os trabalhos agendados são executados de forma assíncrona em segundo plano. As instâncias de trabalhos agendados concluídas podem ser gerenciadas usando cmdlets de trabalho, tais como [Start-Job](https://technet.microsoft.com/library/2bc04935-0deb-4ec0-b856-d7290cca6442) e [Get-Job](https://technet.microsoft.com/library/1352c534-7193-46ca-9ab1-0c5219a661ad).

Assim como tarefas do Agendador de Tarefas, você pode executar trabalhos agendados em uma agenda única ou recorrente ou em resposta a um evento ou ação. Você pode exibir e gerenciar trabalhos agendados no Agendador de Tarefas, habilitar e desabilitá-los conforme necessário, executá-los ou usá-los como modelos e definir as condições sob as quais os trabalhos devem iniciar.

Além disso, os trabalhos agendados são fornecidos com um conjunto personalizado de cmdlets para gerenciá-las. Os cmdlets permitem criar, editar, gerenciar, desabilitar e habilitar novamente os trabalhos agendados, criar disparadores de trabalho agendado e definir opções de trabalho agendado.

Para obter mais informações sobre os trabalhos agendados, consulte [about_Scheduled_Jobs](https://technet.microsoft.com/library/3b546629-703c-4939-b44f-52dd567bce92).

### <a name="windows-powershell-language-enhancements"></a>Aprimoramentos da Linguagem do Windows PowerShell

O Windows PowerShell 3.0 inclui muitos recursos que foram projetados para tornar sua linguagem mais simples e mais fácil de usar e evitar erros comuns. As melhorias incluem propriedades de enumeração, contagem e tamanho de propriedade em objetos escalares, novos operadores de redirecionamento, o modificador de escopo $Using, PSItem automático variável e formatação de script flexível, atributos de variáveis, argumentos de atributo simplificados, nomes de comandos numéricos, operador de análise de parada, nivelamento de matriz aprimorado, novos operadores de bit, dicionários ordenados, conversão de PSCustomObject e ajuda aprimorada baseada em comentário.

### <a name="new-core-cmdlets"></a>Novos cmdlets principais

Foram adicionados novos cmdlets à instalação do Windows PowerShell Core, incluindo cmdlets para gerenciar trabalhos agendados, sessões desconectadas, integração de CIM e o sistema de Ajuda Atualizável.

|||
|-|-|
|Add-JobTrigger|New-JobTrigger|
|Connect-PSSession|New-PSSessionConfigurationFile|
|ConvertFrom-Json|New-PSTransportOption|
|ConvertTo-Json|New-PSWorkflowExecutionOption|
|Disable-JobTrigger|New-PSWorkflowSession|
|Disable-ScheduledJob|New-ScheduledJobOption|
|Disconnect-PSSession|New-WinEvent|
|Enable-JobTrigger|Receive-PSSession|
|Enable-ScheduledJob|Register-CimIndicationEvent|
|Get-CimAssociatedInstance|Register-ScheduledJob|
|Get-CimClass|Remove-CimInstance|
|Get-CimInstance|Remove-CimSession|
|Get-CimSession|Remove-TypeData|
|Get-ControlPanelItem|Rename-Computer|
|Get-IseSnippet|Resume-Job|
|Get-JobTrigger|Save-Help|
|Get-ScheduledJob|Set-CimInstance|
|Get-ScheduledJobOption|Set-JobTrigger|
|Get-TypeData|Set-ScheduledJob|
|Import-IseSnippet|Set-ScheduledJobOption|
|Invoke-AsWorkflow|Show-Command|
|Invoke-CimMethod|Show-ControlPanelItem|
|Invoke-RestMethod|Suspend-Job|
|Invoke-WebRequest|Test-PSSessionConfigurationFile|
|New-CimInstance|Unblock-File|
|New-CimSession|Unregister-ScheduledJob|
|New-CimSessionOption|Update-Help|
|New-IseSnippet||

### <a name="improvements-to-existing-core-cmdlets-and-providers"></a>Aprimoramentos em cmdlets e provedores principais existentes

O Windows PowerShell 3.0 inclui novos recursos para os cmdlets existentes, incluindo sintaxe simplificada e novos parâmetros para os seguintes cmdlets: Cmdlets Computer, CSV, Get-ChildItem, Get-Command, Get-Content, Get-History, Measure-Object, cmdlets Security, Select-Object, Select-String, Split-Path, Start-Process, Tee-Object, Test-Connection, Add-Member e cmdlets WMI.

Os provedores do Windows PowerShell também foram aprimorados significativamente, incluindo o suporte para provedor de certificados para gerenciar certificados Secure Socket Layer (SSL) para hospedagem na web, suporte para credenciais, unidades de rede persistente e fluxos de dados alternados em unidades de sistema de arquivos.

### <a name="remote-module-import-and-discovery"></a>Importação e descoberta de módulo remoto

O Windows PowerShell 3.0 estende os recursos de comunicação remota implícita, de descoberta e importação em computadores remotos. Os cmdlets Module obtém módulos em computadores remotos e importam os módulos para o computador local ou remoto usando o Windows PowerShell remotamente. Novo suporte de sessão CIM permite usar o CIM e o WMI para gerenciar computadores sem Windows importando comandos no computador local implicitamente executados no computador remoto.

Para obter mais informações, consulte os tópicos de ajuda para os cmdlets [Get-Module](https://technet.microsoft.com/library/2cccd4c4-9a21-4c77-b691-984ee57242e1) e [Import-Module](https://technet.microsoft.com/library/af616c24-e122-4098-930e-1e3ea2080ade).

### <a name="enhanced-tab-completion"></a>Preenchimento de tabela avançado

O preenchimento com Tab no console do Windows PowerShell agora preenche os nomes de cmdlets, parâmetros, valores de parâmetro, enumerações, tipos de .NET Frameworks, objetos COM, diretórios e muito mais. O recurso de preenchimento de guia foi completamente reescrito com base em um novo analisador e uma árvore de sintaxe abstrata para dar suporte a mais cenários, incluindo árvores de análise na memória e preenchimento de guias medianas.

### <a name="module-auto-loading"></a>Módulo de carregamento automático

O cmdlet [Get-Command](https://technet.microsoft.com/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad) agora obterá todos os cmdlets e funções de todos os módulos instalados no computador, mesmo se o módulo não for importado para a sessão atual.

Ao obter o cmdlet que você precisa, você pode usá-lo imediatamente sem importar os módulos. Agora, os módulos do Windows PowerShell são importados automaticamente quando você usa qualquer cmdlet no módulo. Você não precisa mais pesquisar o módulo e importá-lo para usar seus cmdlets.

A importação automática de módulos é acionada usando o cmdlet em um comando, executando o **Get-Command** para um cmdlet sem curingas ou o [Get-Help](https://technet.microsoft.com/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a) para um cmdlet sem curingas.

Você pode habilitar, desabilitar e configurar a importação automática de módulos usando a variável de preferência **$PSModuleAutoLoadingPreference**.

Para obter mais informações, consulte [about_Modules](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_modules?view=powershell-5.0), [about_Preference_Variables [v4]](https://technet.microsoft.com/library/31344314-be29-4286-b039-afa5460cbe8b) e os tópicos da Ajuda para os cmdlets [Get-Command](https://technet.microsoft.com/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad) e [Import-Module](https://technet.microsoft.com/library/af616c24-e122-4098-930e-1e3ea2080ade).

### <a name="module-experience-improvements"></a>Aprimoramentos da experiência do módulo

O Windows PowerShell 3.0 oferece suporte a recursos avançados para módulos, incluindo os seguintes recursos novos.

1. Log de módulo para os módulos individuais (LogPipelineExecutionDetails) e a nova configuração de política de grupo "Ativar registro em log do modulo"
2. Módulo objetos estendidos que expõem os valores do manifesto de módulo
3. Nova propriedade de módulos **ExportedCommands**, incluindo módulos aninhados que combinam os comandos de todos os tipos
4. Descoberta aprimorada de módulos disponíveis (não importados), incluindo permitir os parâmetros **Path** e **ListAvailable** no mesmo comando
5. Nova chave **DefaultCommandPrefix** nos manifestos de módulo que evita conflitos de nomes sem alterar o código do módulo.
6. Requisitos de módulo aprimorados, incluindo módulos necessários totalmente qualificado com versão e GUID, bem como importação automática de módulos necessários
7. Operação mais discreta e simplificada do cmdlet [New-ModuleManifest](https://technet.microsoft.com/library/512adced-f42f-4e88-ba7c-834fc9e5d047).
8. Novo parâmetro **Module** para #Requires
9. O cmdlet [Import-Module](https://technet.microsoft.com/library/af616c24-e122-4098-930e-1e3ea2080ade) foi aprimorado com ambos os parâmetros **MinimumVersion** e **RequiredVersion**.

### <a name="simplified-command-discovery"></a>Descoberta de comando simplificada

Você não precisa mais importar todos os módulos para descobrir os comandos disponíveis para sua sessão. No Windows PowerShell 3.0, o cmdlet [Get-Command](https://technet.microsoft.com/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad) obtém todos os comandos de todos os módulos instalados. E, se você usar um comando, o módulo que o exporta é importado automaticamente para a sessão.

O novo cmdlet [Show-Command](https://technet.microsoft.com/library/65bba50b-91a8-49d5-80a2-a30fc684ba41) foi desenvolvido especialmente para iniciantes. É possível procurar comandos em uma janela. Você pode exibir todos os comandos ou filtrar por módulo, importar um módulo clicando em um botão, usar as caixas de texto e listas suspensas para construir um comando válido e copiar ou executar o comando sem sair da janela.

### <a name="improved-logging-diagnostics-and-group-policy-support"></a>Suporte aprimorado ao registro em log, diagnósticos e políticas de grupo

O Windows PowerShell 3.0 melhora o registro em log e o suporte de rastreamento para comandos e módulos com suporte ao Rastreamento de Eventos para Windows (ETW) em logs, uma propriedade editável de módulos **LogPipelineExecutionDetails** e a configuração de política de grupo "Ativar registro em log do módulo". Agora você pode obter valores de parâmetro dos detalhes do log exibindo as propriedades de log.

### <a name="formatting-and-output-improvements"></a>Aprimoramentos de saída e formatação

A nova formatação e aprimoramentos na saída melhoram a eficiência de todos os usuários do Windows PowerShell. Os aprimoramentos incluem o redirecionamento de saída para todos os fluxos, um cmdlet Update-Type aprimorado que adiciona tipos dinamicamente sem arquivos Format.ps1xml, quebra automática de linha na saída, propriedades de formatação padrão de objetos personalizados, o tipo **PSCustomObject**, formatação aprimorada para objetos WMI e objetos heterogêneos, bem como suporte para descobrir as sobrecargas de método.

### <a name="enhanced-console-host-experience"></a>Experiência de host de console aprimorada

O programa do host do console do Windows PowerShell tem novos recursos no Windows PowerShell 3.0, incluindo Single Threaded Apartment por padrão. A nova opção "Executar com o PowerShell" no Explorador de Arquivos permite executar scripts em uma sessão irrestrita com apenas um clique. A nova lógica de inicialização de host do console inicia o Windows PowerShell mais rápido e as novas fontes permitem personalizar a experiência da conhecida janela do console.

Para obter mais informações, consulte [about_Run_With_PowerShell](https://technet.microsoft.com/library/c9d9ca5f-eff9-4409-be9d-e43b5b4087eb).

### <a name="new-cmdlet-and-hosting-apis"></a>Novas APIs de cmdlet e hospedagem

As novas API de Cmdlet e API de hospedagem incluem APIs da árvore de sintaxe avançada pública APIs (AST) e APIs para paginação de pipeline, pipelines aninhados, preenchimento de guias de pools de runspace, Windows RT, atributo do cmdlets Obsolete e propriedades Verb e Noun do objeto FunctionInfo.

### <a name="performance-improvements"></a>Aprimoramento de desempenho

As melhorias de desempenho significativas no Windows PowerShell são graças ao novo analisador de linguagem, que é criado em Dynamic Runtime Language (DLR) no .NET Framework 4., juntamente com a compilação de script de tempo de execução, melhorias de confiabilidade do mecanismo e as alterações no algoritmo do [Get-ChildItem](https://technet.microsoft.com/library/75cf79bb-4db6-4a67-8c36-3d20754e2190) que melhoram seu desempenho, especialmente ao pesquisar os compartilhamentos de rede.

### <a name="runas-and-shared-host-support"></a>Executar como e suporte de host compartilhado

O Windows PowerShell 3.0 inclui suporte para os recursos Executar Como e Host Compartilhado.

O recurso *Executar como*, projetado para o Fluxo de Trabalho do Windows PowerShell, permite que os usuários de uma configuração de sessão criem sessões executadas com a permissão de uma conta de usuário compartilhada. Isso permite que os usuários com menos privilégios executem determinados comandos e scripts com permissões de administrador e reduz a necessidade de adicionar usuários mais inexperientes ao grupo Administradores.

O recurso **SharedHost** permite que vários usuários em vários computadores conectem-se a uma sessão de fluxo de trabalho simultaneamente e monitorem o progresso de um fluxo de trabalho. Os usuários podem iniciar um fluxo de trabalho em um computador e conectar-se à sessão de fluxo de trabalho em outro computador sem desconectar a sessão do computador original. Os usuários devem ter as mesmas permissões e usar a mesma configuração de sessão. Para obter mais informações, consulte "Executando um Fluxo de Trabalho do Windows PowerShell" na Introdução ao Fluxo de Trabalho do Windows PowerShell.

### <a name="special-character-handling-improvements"></a>Aprimoramentos na manipulação de caracteres especiais

Para melhorar a capacidade do Windows PowerShell 3.0 de interpretar e manipular corretamente caracteres especiais, o parâmetro **LiteralPath**, que manipula caracteres especiais em caminhos, é válido para quase todos os cmdlets que têm um parâmetro **Path**, incluindo os novos cmdlets [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) e [Save-Help](https://technet.microsoft.com/library/aed94f90-b73f-4e25-a25d-7c18d9f161fa). O analisador também inclui uma lógica especial para melhorar o manipulador do caractere de acento grave (\`) e colchetes em nomes de arquivo e caminhos.

## <a name="see-also"></a>Consulte Também

- [about_Windows_PowerShell_5.0](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_windows_powershell_5.0?view=powershell-5.0)
- [Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=107116)
