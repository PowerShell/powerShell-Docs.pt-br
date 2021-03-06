---
ms.date: 09/13/2016
ms.topic: reference
title: Início rápido do provedor do Windows PowerShell
description: Início rápido do provedor do Windows PowerShell
ms.openlocfilehash: f0fe0ad60e9d10efd505cda60af995c597226b92
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "92664345"
---
# <a name="windows-powershell-provider-quickstart"></a>Início rápido do provedor do Windows PowerShell

Este tópico explica como criar um provedor do Windows PowerShell que tem a funcionalidade básica de criar uma nova unidade. Para obter informações gerais sobre provedores, consulte [visão geral do provedor do Windows PowerShell](./windows-powershell-provider-overview.md). Para obter exemplos de provedores com funcionalidade mais completa, consulte [exemplos de provedor](./provider-samples.md).

## <a name="writing-a-basic-provider"></a>Escrevendo um provedor básico

A funcionalidade mais básica de um provedor do Windows PowerShell é criar e remover unidades. Neste exemplo, implementamos os métodos [System. Management. Automation. Provider. Drivecmdletprovider. NewDrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) e [System. Management. Automation. Provider. Drivecmdletprovider. Removedrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) da classe [System. Management. Automation. Provider. Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) . Você também verá como declarar uma classe de provedor.

Ao escrever um provedor, você pode especificar unidades-unidades padrão que são criadas automaticamente quando o provedor está disponível. Você também define um método para criar novas unidades que usam esse provedor.

Os exemplos fornecidos neste tópico baseiam-se no exemplo [AccessDBProviderSample02](./accessdbprovidersample02.md) , que faz parte de um exemplo maior que representa um banco de dados do Access como uma unidade do Windows PowerShell.

### <a name="setting-up-the-project"></a>Configurando o projeto

No Visual Studio, crie um projeto de biblioteca de classes chamado AccessDBProviderSample. Conclua as etapas a seguir para configurar seu projeto para que o Windows PowerShell seja iniciado e o provedor seja carregado na sessão, quando você compilar e iniciar o projeto.

##### <a name="configure-the-provider-project"></a>Configurar o projeto do provedor

1. Adicione o assembly System. Management. Automation como uma referência ao seu projeto.

2. Clique em **projeto > Propriedades de AccessDBProviderSample > depurar**. Em **Iniciar projeto**, clique em **Iniciar programa externo** e navegue até o executável do Windows PowerShell (normalmente c:\Windows\system32\WindowsPowerShell\v1.0 \\.powershell.exe).

3. Em **Opções de início**, insira o seguinte na caixa **argumentos de linha de comando** : `-noexit -command "[reflection.assembly]::loadFrom(AccessDBProviderSample.dll' ) | import-module"`

### <a name="declaring-the-provider-class"></a>Declarando a classe do provedor

Nosso provedor deriva da classe [System. Management. Automation. Provider. Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) . A maioria dos provedores que fornecem funcionalidade real (acessando e manipulando itens, navegando no armazenamento de dados e obtendo e definindo o conteúdo dos itens) deriva da classe [System. Management. Automation. Provider. Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) .

Além de especificar que a classe deriva de [System. Management. Automation. Provider. Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider), você deve decorar isso com o [System. Management. Automation. Provider. Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) , conforme mostrado no exemplo.

```csharp
namespace Microsoft.Samples.PowerShell.Providers
{
  using System;
  using System.Data;
  using System.Data.Odbc;
  using System.IO;
  using System.Management.Automation;
  using System.Management.Automation.Provider;

  #region AccessDBProvider

  [CmdletProvider("AccessDB", ProviderCapabilities.None)]
  public class AccessDBProvider : DriveCmdletProvider
  {

}
}
```

### <a name="implementing-newdrive"></a>Implementando NewDrive

O método [System. Management. Automation. Provider. Drivecmdletprovider. NewDrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) é chamado pelo mecanismo do Windows PowerShell quando um usuário chama o cmdlet [Microsoft. PowerShell. Commands. NewPSDriveCommand](/dotnet/api/Microsoft.PowerShell.Commands.Newpsdrivecommand) especificando o nome do seu provedor. O parâmetro PSDriveInfo é passado pelo mecanismo do Windows PowerShell e o método retorna a nova unidade para o mecanismo do Windows PowerShell. Esse método deve ser declarado dentro da classe criada acima.

O método primeiro verifica se o objeto da unidade e a raiz da unidade que foram passados existem, retornando `null` se um deles não faz isso. Em seguida, ele usa um construtor da classe interna AccessDBPSDriveInfo para criar uma nova unidade e uma conexão com o banco de dados do Access que a unidade representa.

```csharp
protected override PSDriveInfo NewDrive(PSDriveInfo drive)
    {
      // Check if the drive object is null.
      if (drive == null)
      {
        WriteError(new ErrorRecord(
                   new ArgumentNullException("drive"),
                   "NullDrive",
                   ErrorCategory.InvalidArgument,
                   null));

        return null;
      }

      // Check if the drive root is not null or empty
      // and if it is an existing file.
      if (String.IsNullOrEmpty(drive.Root) || (File.Exists(drive.Root) == false))
      {
        WriteError(new ErrorRecord(
                   new ArgumentException("drive.Root"),
                   "NoRoot",
                   ErrorCategory.InvalidArgument,
                   drive));

        return null;
      }

      // Create a new drive and create an ODBC connection to the new drive.
      AccessDBPSDriveInfo accessDBPSDriveInfo = new AccessDBPSDriveInfo(drive);
      OdbcConnectionStringBuilder builder = new OdbcConnectionStringBuilder();

      builder.Driver = "Microsoft Access Driver (*.mdb)";
      builder.Add("DBQ", drive.Root);

      OdbcConnection conn = new OdbcConnection(builder.ConnectionString);
      conn.Open();
      accessDBPSDriveInfo.Connection = conn;

      return accessDBPSDriveInfo;
    }
```

A seguir está a classe interna AccessDBPSDriveInfo que inclui o construtor usado para criar uma nova unidade e contém as informações de estado para a unidade.

```csharp
internal class AccessDBPSDriveInfo : PSDriveInfo
  {
    /// <summary>
    /// A reference to the connection to the database.
    /// </summary>
    private OdbcConnection connection;

    /// <summary>
    /// Initializes a new instance of the AccessDBPSDriveInfo class.
    /// The constructor takes a single argument.
    /// </summary>
    /// <param name="driveInfo">Drive defined by this provider</param>
    public AccessDBPSDriveInfo(PSDriveInfo driveInfo)
           : base(driveInfo)
    {
    }

    /// <summary>
    /// Gets or sets the ODBC connection information.
    /// </summary>
    public OdbcConnection Connection
    {
        get { return this.connection; }
        set { this.connection = value; }
    }
  }
```

### <a name="implementing-removedrive"></a>Implementando RemoveDrive

O método [System. Management. Automation. Provider. Drivecmdletprovider. Removedrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) é chamado pelo mecanismo do Windows PowerShell quando um usuário chama o cmdlet [Microsoft. PowerShell. Commands. RemovePSDriveCommand](/dotnet/api/Microsoft.PowerShell.Commands.removepsdrivecommand) . O método nesse provedor fecha a conexão com o banco de dados do Access.

```csharp
protected override PSDriveInfo RemoveDrive(PSDriveInfo drive)
    {
      // Check if drive object is null.
      if (drive == null)
      {
        WriteError(new ErrorRecord(
                   new ArgumentNullException("drive"),
                   "NullDrive",
                   ErrorCategory.InvalidArgument,
                   drive));

        return null;
      }

      // Close the ODBC connection to the drive.
      AccessDBPSDriveInfo accessDBPSDriveInfo = drive as AccessDBPSDriveInfo;

      if (accessDBPSDriveInfo == null)
      {
         return null;
      }

      accessDBPSDriveInfo.Connection.Close();

      return accessDBPSDriveInfo;
    }
```
