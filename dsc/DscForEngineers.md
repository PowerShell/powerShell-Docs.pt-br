# <a name="desired-state-configuration-overview-for-engineers"></a>Visão Geral da Configuração de Estado Desejado para Engenheiros #

Elaboramos este documento para que as equipes de operações e os desenvolvedores possam compreender os benefícios da DSC (Configuração de Estado Desejado) do PowerShell.
Para obter uma ideia mais abrangente do valor que a DSC fornece, confira o tópico [Visão Geral da Configuração de Estado Desejado para Tomadores de Decisão](decisionMaker.md)

## <a name="benefits-of-desired-state-configuration"></a>Benefícios da Configuração de Estado Desejado

A DSC existe para:
- Diminuir a complexidade da criação de scripts no Windows
- Aumentar a velocidade de iteração

O conceito de "implantação contínua" está se tornando mais importante. Implantação contínua significa a capacidade de implantar com frequência, possivelmente, várias vezes por dia.
A finalidade dessas implantações não é corrigir algo, mas sim publicar conteúdo rapidamente.
Ao lançar novos recursos do desenvolvimento para as operações da forma mais tranquila e confiável possível, você aumenta o rendimento da nova lógica de negócios.

Existem duas tendências em jogo que aumentam essa necessidade de avançar rapidamente. O avanço para a computação em nuvem implica uma mudança rápida, em escala, com uma ameaça constante de fracasso.
Em virtude dessas implicações, é necessário aumentar a automação.
A criação da mentalidade "DevOps" é a solução para essas mudanças. 


A DSC é uma plataforma que fornece implantação, configuração e conformidade declarativas, autônomas e idempotentes (repetível).
Na plataforma DSC, você garante que os componentes do datacenter tenham a configuração correta, evitando erros e falhas de implantação dispendiosas.
A DSC permite a implantação contínua, tratando as configurações DSC como parte do código do aplicativo.
A configuração DSC deve ser atualizada como parte do aplicativo, garantindo que o conhecimento necessário para implantá-lo esteja sempre atualizado e pronto para uso.


## <a name="i-have-powershell-why-do-i-need-desired-state-configuration"></a>"Eu tenho o PowerShell, por que preciso da Configuração de Estado Desejado?"

As configurações DSC separam finalidade (ou seja, "o que eu quero fazer") de execução (isto é, "de que maneira eu quero fazê-lo").
Isso significa que a lógica de execução está incluída nos recursos.
Os usuários não precisam saber como implementar ou implantar um recurso quando um recurso DSC para este recurso está disponível.
Dessa forma, os usuários podem se concentrar na estrutura da implantação deles.

Por exemplo, os scripts do PowerShell devem ter a seguinte aparência:
```powershell
# Create a share in Windows Server 8
New-SmbShare -Name MyShare -Path C:\Demo\Temp -FullAccess Alice -ReadAccess Bob
```
Esse script é fácil, simples e direto. No entanto, se tentar colocar o script em produção, você enfrentará vários problemas.
O que acontece se o script for executado duas vezes seguidas?
O que acontece se Diogo já tinha acesso completo ao compartilhamento? 

Para compensar esses problemas, uma versão "real" do script será mais parecida com a seguinte:
```powershell
# But actually creating a share in an idempotent way would be

$shareExists = $false
$smbShare = Get-SmbShare -Name $Name -ErrorAction SilentlyContinue
if($smbShare -ne $null)
{
    Write-Verbose -Message "Share with name $Name exists"
    $shareExists = $true
}

if ($shareExists -eq $false)
{
    Write-Verbose "Creating share $Name to ensure it is Present"
    New-SmbShare @psboundparameters
}
else
{
    # Need to call either Set-SmbShare or *ShareAccess cmdlets
    if ($psboundparameters.ContainsKey("ChangeAccess"))
    {
       #...etc, etc, etc
    }
}
```

Esse script é mais complexo, com muita lógica e tratamento de erros.
O script é mais complexo porque você não informa mais o que pretende fazer, e sim *como fazê-lo*.

Na DSC, você pode informar o que pretende fazer e a lógica subjacente é simplificada.

```powershell
# A configuration is a special kind of PowerShell function
Configuration Sample_Share
{
   Import-DscResource -Module xSmbShare
   # Nodes are the endpoint we wish to configure
   # A Configuration block can have zero or more Node blocks
   Node $NodeName
   {
      # Next, specify one or more resource blocks
      # Resources are simply PowerShell modules that
      # implement the logic of "how" to execute a task
      xSmbShare MySMBShare
      {
          Ensure      = "Present" 
          Name        = "MyShare"
          Path        = "C:\Demo\Temp"  
          ReadAccess  = "Alice"
          FullAccess  = "Bob"
          Description = "This is an updated description for this share"
      }
   }
} 
#Run the function to compile the configuration
Sample_Share
#Pass the configuration to the nodes we defined and configure them
Start-DscConfiguration Sample_Share
```

Este script tem um formato simples e é fácil de ler.
Os caminhos lógicos e o tratamento de erros continuam presentes na implementação [resource](resources.md), embora sejam invisíveis para o autor do script. 



## <a name="separating-environment-from-structure"></a>Separando ambiente de estrutura

Um padrão comum na DevOps é usar vários ambientes de implantação. Por exemplo, pode haver um ambiente de "desenvolvimento" para criar o protótipo de um novo código rapidamente.
O código do ambiente de "desenvolvimento" passa por um ambiente de "teste", no qual outras pessoas verificam a funcionalidade.
Por fim, o código passa para a "produção" ou o ambiente de produção de site ativo.

As configurações DSC acomodam esse pipeline de desenvolvimento/teste/produção, por meio do uso de [dados da configuração](configData.md).
Isso simplifica ainda mais a diferença entre a estrutura da configuração e os nós gerenciados.
Por exemplo, você pode definir uma configuração que requer um SQL Server, um Servidor IIS e um servidor de camada intermediária. Independentemente de quais nós recebem as diferentes partes dessa configuração, esses três elementos estarão sempre presentes.
Você pode usar dados de configuração para apontar todos os três elementos para o mesmo computador em um ambiente de desenvolvimento, separar os três elementos para três computadores diferentes em um ambiente de teste e, por fim, apontá-los para todos os servidores de produção no ambiente de produção.
Para implantar em diferentes ambientes, você pode invocar `Start-DscConfiguration` com os dados de configuração corretos para o ambiente de destino. 

## <a name="see-also"></a>Consulte Também

[Configurações](configurations.md)

[Dados da Configuração](configData.md)

[Recursos](resources.md)