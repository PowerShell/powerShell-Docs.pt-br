---
title: Início rápido do provedor do Windows PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3e879ba7-c334-460b-94a1-3e9b63d3d8de
caps.latest.revision: 5
ms.openlocfilehash: 949c0d63b1e5bca1bfe670362df4297c29e98fcc
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72359915"
---
# <a name="windows-powershell-provider-quickstart"></a><span data-ttu-id="6f60f-102">Início rápido do provedor do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f60f-102">Windows PowerShell Provider Quickstart</span></span>

<span data-ttu-id="6f60f-103">Este tópico explica como criar um provedor do Windows PowerShell que tem a funcionalidade básica de criar uma nova unidade.</span><span class="sxs-lookup"><span data-stu-id="6f60f-103">This topic explains how to create a Windows PowerShell provider that has basic functionality of creating a new drive.</span></span> <span data-ttu-id="6f60f-104">Para obter informações gerais sobre provedores, consulte [visão geral do provedor do Windows PowerShell](./windows-powershell-provider-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6f60f-104">For general information about providers, see [Windows PowerShell Provider Overview](./windows-powershell-provider-overview.md).</span></span> <span data-ttu-id="6f60f-105">Para obter exemplos de provedores com funcionalidade mais completa, consulte [exemplos de provedor](./provider-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6f60f-105">For examples of providers with more complete functionality, see [Provider Samples](./provider-samples.md).</span></span>

## <a name="writing-a-basic-provider"></a><span data-ttu-id="6f60f-106">Escrevendo um provedor básico</span><span class="sxs-lookup"><span data-stu-id="6f60f-106">Writing a basic provider</span></span>

<span data-ttu-id="6f60f-107">A funcionalidade mais básica de um provedor do Windows PowerShell é criar e remover unidades.</span><span class="sxs-lookup"><span data-stu-id="6f60f-107">The most basic functionality of a Windows PowerShell provider is to create and remove drives.</span></span> <span data-ttu-id="6f60f-108">Neste exemplo, implementamos os métodos [System. Management. Automation. Provider. Drivecmdletprovider. NewDrive \*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) e [System. Management. Automation. Provider. Drivecmdletprovider. Removedrive \*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) do [ Classe System. Management. Automation. Provider. Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) .</span><span class="sxs-lookup"><span data-stu-id="6f60f-108">In this example, we implement the [System.Management.Automation.Provider.Drivecmdletprovider.Newdrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) and [System.Management.Automation.Provider.Drivecmdletprovider.Removedrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) methods of the [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) class.</span></span> <span data-ttu-id="6f60f-109">Você também verá como declarar uma classe de provedor.</span><span class="sxs-lookup"><span data-stu-id="6f60f-109">You will also see how to declare a provider class.</span></span>

<span data-ttu-id="6f60f-110">Ao escrever um provedor, você pode especificar unidades-unidades padrão que são criadas automaticamente quando o provedor está disponível.</span><span class="sxs-lookup"><span data-stu-id="6f60f-110">When you write a provider, you can specify default drives-drives that are created automatically when the provider is available.</span></span> <span data-ttu-id="6f60f-111">Você também define um método para criar novas unidades que usam esse provedor.</span><span class="sxs-lookup"><span data-stu-id="6f60f-111">You also define a method to create new drives that use that provider.</span></span>

<span data-ttu-id="6f60f-112">Os exemplos fornecidos neste tópico baseiam-se no exemplo [AccessDBProviderSample02](./accessdbprovidersample02.md) , que faz parte de um exemplo maior que representa um banco de dados do Access como uma unidade do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f60f-112">The examples provided in this topic are based on the [AccessDBProviderSample02](./accessdbprovidersample02.md) sample, which is part of a larger sample that represents an Access database as a Windows PowerShell drive.</span></span>

### <a name="setting-up-the-project"></a><span data-ttu-id="6f60f-113">Configurando o projeto</span><span class="sxs-lookup"><span data-stu-id="6f60f-113">Setting up the project</span></span>

<span data-ttu-id="6f60f-114">No Visual Studio, crie um projeto de biblioteca de classes chamado AccessDBProviderSample.</span><span class="sxs-lookup"><span data-stu-id="6f60f-114">In Visual Studio, create a Class Library project named AccessDBProviderSample.</span></span> <span data-ttu-id="6f60f-115">Conclua as etapas a seguir para configurar seu projeto para que o Windows PowerShell seja iniciado e o provedor seja carregado na sessão, quando você compilar e iniciar o projeto.</span><span class="sxs-lookup"><span data-stu-id="6f60f-115">Complete the following steps to configure your project so that Windows PowerShell will start, and the provider will be loaded into the session, when you build and start your project.</span></span>

##### <a name="configure-the-provider-project"></a><span data-ttu-id="6f60f-116">Configurar o projeto do provedor</span><span class="sxs-lookup"><span data-stu-id="6f60f-116">Configure the provider project</span></span>

1. <span data-ttu-id="6f60f-117">Adicione o assembly System. Management. Automation como uma referência ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="6f60f-117">Add the System.Management.Automation assembly as a reference to your project.</span></span>

2. <span data-ttu-id="6f60f-118">Clique em **projeto > Propriedades de AccessDBProviderSample > depurar**.</span><span class="sxs-lookup"><span data-stu-id="6f60f-118">Click **Project > AccessDBProviderSample Properties > Debug**.</span></span> <span data-ttu-id="6f60f-119">Em **Iniciar projeto**, clique em **Iniciar programa externo**e navegue até o executável do Windows PowerShell (normalmente c:\windows\system32\windowspowershell\ v1.0\\.powershell.exe).</span><span class="sxs-lookup"><span data-stu-id="6f60f-119">In **Start project**, click **Start external program**, and navigate to the Windows PowerShell executable (typically c:\Windows\System32\WindowsPowerShell\v1.0\\.powershell.exe).</span></span>

3. <span data-ttu-id="6f60f-120">Em **Opções de início**, insira o seguinte na caixa **argumentos de linha de comando** : `-noexit -command "[reflection.assembly]::loadFrom(AccessDBProviderSample.dll' ) | import-module"`</span><span class="sxs-lookup"><span data-stu-id="6f60f-120">Under **Start Options**, enter the following into the **Command line arguments** box: `-noexit -command "[reflection.assembly]::loadFrom(AccessDBProviderSample.dll' ) | import-module"`</span></span>

### <a name="declaring-the-provider-class"></a><span data-ttu-id="6f60f-121">Declarando a classe do provedor</span><span class="sxs-lookup"><span data-stu-id="6f60f-121">Declaring the provider class</span></span>

<span data-ttu-id="6f60f-122">Nosso provedor deriva da classe [System. Management. Automation. Provider. Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) .</span><span class="sxs-lookup"><span data-stu-id="6f60f-122">Our provider derives from the [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) class.</span></span> <span data-ttu-id="6f60f-123">A maioria dos provedores que fornecem funcionalidade real (acessando e manipulando itens, navegando no armazenamento de dados e obtendo e definindo o conteúdo dos itens) deriva da classe [System. Management. Automation. Provider. Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) .</span><span class="sxs-lookup"><span data-stu-id="6f60f-123">Most providers that provide real functionality (accessing and manipulating items, navigating the data store, and getting and setting content of items) derive from the [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) class.</span></span>

<span data-ttu-id="6f60f-124">Além de especificar que a classe deriva de [System. Management. Automation. Provider. Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider), você deve decorar com o [System. Management. Automation. Provider. Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) , conforme mostrado no exemplo .</span><span class="sxs-lookup"><span data-stu-id="6f60f-124">In addition to specifying that the class derives from [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider), you must decorate it with the [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) as shown in the example.</span></span>

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

### <a name="implementing-newdrive"></a><span data-ttu-id="6f60f-125">Implementando NewDrive</span><span class="sxs-lookup"><span data-stu-id="6f60f-125">Implementing NewDrive</span></span>

<span data-ttu-id="6f60f-126">O método [System. Management. Automation. Provider. Drivecmdletprovider. NewDrive \*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) é chamado pelo mecanismo do Windows PowerShell quando um usuário chama o cmdlet [Microsoft. PowerShell. Commands. NewPSDriveCommand](/dotnet/api/Microsoft.PowerShell.Commands.Newpsdrivecommand) especificando o nome do seu operador.</span><span class="sxs-lookup"><span data-stu-id="6f60f-126">The [System.Management.Automation.Provider.Drivecmdletprovider.Newdrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) method is called by the Windows PowerShell engine when a user calls the [Microsoft.PowerShell.Commands.NewPSDriveCommand](/dotnet/api/Microsoft.PowerShell.Commands.Newpsdrivecommand) cmdlet specifying the name of your provider.</span></span> <span data-ttu-id="6f60f-127">O parâmetro PSDriveInfo é passado pelo mecanismo do Windows PowerShell e o método retorna a nova unidade para o mecanismo do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f60f-127">The PSDriveInfo parameter is passed by the Windows PowerShell engine, and the method returns the new drive to the Windows PowerShell engine.</span></span> <span data-ttu-id="6f60f-128">Esse método deve ser declarado dentro da classe criada acima.</span><span class="sxs-lookup"><span data-stu-id="6f60f-128">This method must be declared within the class created above.</span></span>

<span data-ttu-id="6f60f-129">O método primeiro verifica se o objeto da unidade e a raiz da unidade que foram passados existem, retornando `null`, caso não haja nenhum.</span><span class="sxs-lookup"><span data-stu-id="6f60f-129">The method first checks to make sure both the drive object and the drive root that were passed in exist, returning `null` if either of them do not.</span></span> <span data-ttu-id="6f60f-130">Em seguida, ele usa um construtor da classe interna AccessDBPSDriveInfo para criar uma nova unidade e uma conexão com o banco de dados do Access que a unidade representa.</span><span class="sxs-lookup"><span data-stu-id="6f60f-130">It then uses a constructor of the internal class AccessDBPSDriveInfo to create a new drive and a connection to the Access database the drive represents.</span></span>

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

<span data-ttu-id="6f60f-131">A seguir está a classe interna AccessDBPSDriveInfo que inclui o construtor usado para criar uma nova unidade e contém as informações de estado para a unidade.</span><span class="sxs-lookup"><span data-stu-id="6f60f-131">The following is the AccessDBPSDriveInfo internal class that includes the constructor used to create a new drive, and contains the state information for the drive.</span></span>

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

### <a name="implementing-removedrive"></a><span data-ttu-id="6f60f-132">Implementando RemoveDrive</span><span class="sxs-lookup"><span data-stu-id="6f60f-132">Implementing RemoveDrive</span></span>

<span data-ttu-id="6f60f-133">O método [System. Management. Automation. Provider. Drivecmdletprovider. Removedrive \*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) é chamado pelo mecanismo do Windows PowerShell quando um usuário chama o cmdlet [Microsoft. PowerShell. Commands. RemovePSDriveCommand](/dotnet/api/Microsoft.PowerShell.Commands.removepsdrivecommand) .</span><span class="sxs-lookup"><span data-stu-id="6f60f-133">The [System.Management.Automation.Provider.Drivecmdletprovider.Removedrive\*](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) method is called by the Windows PowerShell engine when a user calls the [Microsoft.PowerShell.Commands.RemovePSDriveCommand](/dotnet/api/Microsoft.PowerShell.Commands.removepsdrivecommand) cmdlet.</span></span> <span data-ttu-id="6f60f-134">O método nesse provedor fecha a conexão com o banco de dados do Access.</span><span class="sxs-lookup"><span data-stu-id="6f60f-134">The method in this provider closes the connection to the Access database.</span></span>

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