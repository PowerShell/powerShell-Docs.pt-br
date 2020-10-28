---
ms.date: 06/05/2017
keywords: powershell, cmdlet
title: Manipulando itens diretamente
description: O PowerShell fornece vários cmdlets que ajudam a gerenciar itens em computadores locais e remotos. Os itens são objetos expostos por provedores do PowerShell, como o sistema de arquivos, o Registro, os certificados e outros.
ms.openlocfilehash: 20132b63a8ff4ef24b1d8346066315dbb053e59c
ms.sourcegitcommit: 9080316e3ca4f11d83067b41351531672b667b7a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/24/2020
ms.locfileid: "92500310"
---
# <a name="manipulating-items-directly"></a><span data-ttu-id="46905-105">Manipulando itens diretamente</span><span class="sxs-lookup"><span data-stu-id="46905-105">Manipulating Items Directly</span></span>

<span data-ttu-id="46905-106">Os elementos exibidos em unidades do Windows PowerShell, como os arquivos e pastas em unidades de sistema de arquivos e as chaves do registro nas unidades do registro do Windows PowerShell, são chamados de *itens* no Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="46905-106">The elements that you see in Windows PowerShell drives, such as the files and folders in the file system drives, and the registry keys in the Windows PowerShell registry drives, are called *items* in Windows PowerShell.</span></span> <span data-ttu-id="46905-107">Os cmdlets para trabalhar com eles item possuem o substantivo **Item** em seus nomes.</span><span class="sxs-lookup"><span data-stu-id="46905-107">The cmdlets for working with them item have the noun **Item** in their names.</span></span>

<span data-ttu-id="46905-108">O resultado do comando **Get-Command -Noun Item** mostra que existem nove cmdlets de itens do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="46905-108">The output of the **Get-Command -Noun Item** command shows that there are nine Windows PowerShell item cmdlets.</span></span>

```
PS> Get-Command -Noun Item

CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Clear-Item                      Clear-Item [-Path] <String[]...
Cmdlet          Copy-Item                       Copy-Item [-Path] <String[]>...
Cmdlet          Get-Item                        Get-Item [-Path] <String[]> ...
Cmdlet          Invoke-Item                     Invoke-Item [-Path] <String[...
Cmdlet          Move-Item                       Move-Item [-Path] <String[]>...
Cmdlet          New-Item                        New-Item [-Path] <String[]> ...
Cmdlet          Remove-Item                     Remove-Item [-Path] <String[...
Cmdlet          Rename-Item                     Rename-Item [-Path] <String>...
Cmdlet          Set-Item                        Set-Item [-Path] <String[]> ...
```

## <a name="creating-new-items-new-item"></a><span data-ttu-id="46905-109">Criando novos itens (New-Item)</span><span class="sxs-lookup"><span data-stu-id="46905-109">Creating New Items (New-Item)</span></span>

<span data-ttu-id="46905-110">Para criar um novo item no sistema de arquivos, use o cmdlet **New-Item** .</span><span class="sxs-lookup"><span data-stu-id="46905-110">To create a new item in the file system, use the **New-Item** cmdlet.</span></span> <span data-ttu-id="46905-111">Inclua o parâmetro **Path** com o caminho para o item e o parâmetro **ItemType** com um valor de "file" ou "directory".</span><span class="sxs-lookup"><span data-stu-id="46905-111">Include the **Path** parameter with path to the item, and the **ItemType** parameter with a value of "file" or "directory".</span></span>

<span data-ttu-id="46905-112">Por exemplo, para criar um novo diretório chamado “New.Directory” no diretório C:\\Temp, digite:</span><span class="sxs-lookup"><span data-stu-id="46905-112">For example, to create a new directory named "New.Directory"in the C:\\Temp directory,  type:</span></span>

```
PS> New-Item -Path c:\temp\New.Directory -ItemType Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  11:29 AM            New.Directory
```

<span data-ttu-id="46905-113">Para criar um arquivo, altere o valor do parâmetro **ItemType** para "file".</span><span class="sxs-lookup"><span data-stu-id="46905-113">To create a file, change the value of the **ItemType** parameter to "file".</span></span> <span data-ttu-id="46905-114">Por exemplo, para criar um arquivo chamado "file1.txt" no diretório New.Directory, digite:</span><span class="sxs-lookup"><span data-stu-id="46905-114">For example, to create a file named "file1.txt" in the New.Directory directory, type:</span></span>

```
PS> New-Item -Path C:\temp\New.Directory\file1.txt -ItemType file

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

<span data-ttu-id="46905-115">Você pode usar a mesma técnica para criar uma nova chave do registro.</span><span class="sxs-lookup"><span data-stu-id="46905-115">You can use the same technique to create a new registry key.</span></span> <span data-ttu-id="46905-116">Na verdade, uma chave do registro é mais fácil de criar porque o único tipo de item no registro do Windows é uma chave.</span><span class="sxs-lookup"><span data-stu-id="46905-116">In fact, a registry key is easier to create because the only item type in the Windows registry is a key.</span></span> <span data-ttu-id="46905-117">(Entradas do Registro são *propriedades* do item.) Por exemplo, para criar uma chave chamada "_Test" na subchave CurrentVersion, digite:</span><span class="sxs-lookup"><span data-stu-id="46905-117">(Registry entries are item *properties* .) For example, to create a key named "_Test" in the CurrentVersion subkey, type:</span></span>

```
PS> New-Item -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion_Test

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion

SKC  VC Name                           Property
---  -- ----                           --------
  0   0 _Test                          {}
```

<span data-ttu-id="46905-118">Ao digitar um caminho do registro, certifique-se de incluir os dois-pontos ( **:** ) nos nomes de unidades do Windows PowerShell, HKLM: e HKCU:.</span><span class="sxs-lookup"><span data-stu-id="46905-118">When typing a registry path, be sure to include the colon ( **:** ) in the Windows PowerShell drive names, HKLM: and HKCU:.</span></span> <span data-ttu-id="46905-119">Sem os dois pontos, o Windows PowerShell não reconhece o nome de unidade no caminho.</span><span class="sxs-lookup"><span data-stu-id="46905-119">Without the colon, Windows PowerShell does not recognize the drive name in the path.</span></span>

## <a name="why-registry-values-are-not-items"></a><span data-ttu-id="46905-120">Por que os valores do registro não são itens</span><span class="sxs-lookup"><span data-stu-id="46905-120">Why Registry Values are not Items</span></span>

<span data-ttu-id="46905-121">Ao usar o cmdlet **Get-ChildItem** para localizar os itens em uma chave do registro, você nunca verá entradas reais do registro ou seus valores.</span><span class="sxs-lookup"><span data-stu-id="46905-121">When you use the **Get-ChildItem** cmdlet to find the items in a registry key, you will never see actual registry entries or their values.</span></span>

<span data-ttu-id="46905-122">Por exemplo, a chave do Registro **HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Run** geralmente contém várias entradas do Registro que representam aplicativos executados quando o sistema é iniciado.</span><span class="sxs-lookup"><span data-stu-id="46905-122">For example, the registry key **HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Run** usually contains several registry entries that represent applications that run when the system starts.</span></span>

<span data-ttu-id="46905-123">No entanto, ao usar **Get-ChildItem** para procurar itens filhos na chave, tudo o que você verá é a subchave **OptionalComponents** da chave:</span><span class="sxs-lookup"><span data-stu-id="46905-123">However, when you use **Get-ChildItem** to look for child items in the key, all you will see is the **OptionalComponents** subkey of the key:</span></span>

```
PS> Get-ChildItem HKLM:\Software\Microsoft\Windows\CurrentVersion\Run

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\Micros
oft\Windows\CurrentVersion\Run
SKC  VC Name                           Property
---  -- ----                           --------
  3   0 OptionalComponents             {}
```

<span data-ttu-id="46905-124">Embora seria algo conveniente tratar as entradas do registro como itens, não é possível você especificar um caminho para uma entrada de registro de uma maneira que garanta que ele seja exclusivo.</span><span class="sxs-lookup"><span data-stu-id="46905-124">Although it would be convenient to treat registry entries as items, you cannot specify a path to a registry entry in a way that ensures that it is unique.</span></span> <span data-ttu-id="46905-125">A notação de caminho não faz distinção entre a subchave do Registro chamada **Run** e a entrada do Registro **(Default)** na subchave **Run** .</span><span class="sxs-lookup"><span data-stu-id="46905-125">The path notation does not distinguish between the registry subkey named **Run** and the **(Default)** registry entry in the **Run** subkey.</span></span> <span data-ttu-id="46905-126">Além disso, como nomes de entrada do Registro podem conter o caractere de barra invertida ( **\\** ), se as entradas de Registro fossem itens, você não poderia usar a notação de caminho para distinguir uma entrada do Registro denominada **Windows\\CurrentVersion\\Run** da subchave localizada nesse caminho.</span><span class="sxs-lookup"><span data-stu-id="46905-126">Furthermore, because registry entry names can contain the backslash character ( **\\** ), if registry entries were items, then you could not use the path notation to distinguish a registry entry named **Windows\\CurrentVersion\\Run** from the subkey that is located in that path.</span></span>

## <a name="renaming-existing-items-rename-item"></a><span data-ttu-id="46905-127">Renomeando itens existentes (Rename-Item)</span><span class="sxs-lookup"><span data-stu-id="46905-127">Renaming Existing Items (Rename-Item)</span></span>

<span data-ttu-id="46905-128">Para alterar o nome de uma configuração de sessão, use o cmdlet **Rename-Item** .</span><span class="sxs-lookup"><span data-stu-id="46905-128">To change the name of a file or folder, use the **Rename-Item** cmdlet.</span></span> <span data-ttu-id="46905-129">O comando a seguir altera o nome do arquivo **file1.txt** para **fileOne.txt** .</span><span class="sxs-lookup"><span data-stu-id="46905-129">The following command changes the name of the **file1.txt** file to **fileOne.txt** .</span></span>

```powershell
Rename-Item -Path C:\temp\New.Directory\file1.txt fileOne.txt
```

<span data-ttu-id="46905-130">O cmdlet **Rename-Item** pode alterar o nome de um arquivo ou uma pasta, mas não pode mover um item.</span><span class="sxs-lookup"><span data-stu-id="46905-130">The **Rename-Item** cmdlet can change the name of a file or a folder, but it cannot move an item.</span></span> <span data-ttu-id="46905-131">O comando a seguir falhará porque ele tenta mover o arquivo da pasta New.Directory para o diretório Temp.</span><span class="sxs-lookup"><span data-stu-id="46905-131">The following command fails because it attempts to move the file from the New.Directory directory to the Temp directory.</span></span>

```
PS> Rename-Item -Path C:\temp\New.Directory\fileOne.txt c:\temp\fileOne.txt
Rename-Item : Cannot rename because the target specified is not a path.
At line:1 char:12
+ Rename-Item  <<<< -Path C:\temp\New.Directory\fileOne c:\temp\fileOne.txt
```

## <a name="moving-items-move-item"></a><span data-ttu-id="46905-132">Movendo itens (Move Item)</span><span class="sxs-lookup"><span data-stu-id="46905-132">Moving Items (Move-Item)</span></span>

<span data-ttu-id="46905-133">Para mover um arquivo ou pasta, use o cmdlet **Move-Item** .</span><span class="sxs-lookup"><span data-stu-id="46905-133">To move a file or folder, use the **Move-Item** cmdlet.</span></span>

<span data-ttu-id="46905-134">Por exemplo, o comando a seguir move o diretório New.Directory do diretório C:\\temp para a raiz da unidade C:.</span><span class="sxs-lookup"><span data-stu-id="46905-134">For example, the following command moves the New.Directory directory from the C:\\temp directory to the root of the C: drive.</span></span> <span data-ttu-id="46905-135">Para confirmar que o item foi movido, inclua o parâmetro **PassThru** do cmdlet **Move-Item** .</span><span class="sxs-lookup"><span data-stu-id="46905-135">To verify that the item was moved, include the **PassThru** parameter of the **Move-Item** cmdlet.</span></span> <span data-ttu-id="46905-136">Sem o **Passthru** , o cmdlet **Move-Item** não exibirá nenhum resultado.</span><span class="sxs-lookup"><span data-stu-id="46905-136">Without **Passthru** , the **Move-Item** cmdlet does not display any results.</span></span>

```
PS> Move-Item -Path C:\temp\New.Directory -Destination C:\ -PassThru

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  12:14 PM            New.Directory
```

## <a name="copying-items-copy-item"></a><span data-ttu-id="46905-137">Copiando itens (Copy-Item)</span><span class="sxs-lookup"><span data-stu-id="46905-137">Copying Items (Copy-Item)</span></span>

<span data-ttu-id="46905-138">Se você estiver familiarizado com as operações de cópia em outros shells, poderá achar o comportamento do cmdlet **Copy-Item** do Windows PowerShell um tanto incomum.</span><span class="sxs-lookup"><span data-stu-id="46905-138">If you are familiar with the copy operations in other shells, you might find the behavior of the **Copy-Item** cmdlet in Windows PowerShell to be unusual.</span></span> <span data-ttu-id="46905-139">Quando você copia um item de um local para outro, o Copy-Item não copia o conteúdo por padrão.</span><span class="sxs-lookup"><span data-stu-id="46905-139">When you copy an item from one location to another, Copy-Item does not copy its contents by default.</span></span>

<span data-ttu-id="46905-140">Por exemplo, se você copiar o diretório **New.Directory** da unidade C: para o diretório C:\\temp, o comando será executado com êxito, mas os arquivos no diretório New.Directory não serão copiados.</span><span class="sxs-lookup"><span data-stu-id="46905-140">For example, if you copy the **New.Directory** directory from the C: drive to the C:\\temp directory, the command succeeds, but the files in the New.Directory directory are not copied.</span></span>

```powershell
Copy-Item -Path C:\New.Directory -Destination C:\temp
```

<span data-ttu-id="46905-141">Se você exibir o conteúdo do **C:\\temp\\New.Directory** , verá que ele não contém nenhum arquivo:</span><span class="sxs-lookup"><span data-stu-id="46905-141">If you display the contents of **C:\\temp\\New.Directory** , you will find that it contains no files:</span></span>

```
PS> Get-ChildItem -Path C:\temp\New.Directory
PS>
```

<span data-ttu-id="46905-142">Por que o cmdlet **Copy-Item** não copia o conteúdo para um novo local?</span><span class="sxs-lookup"><span data-stu-id="46905-142">Why doesn't the **Copy-Item** cmdlet copy the contents to the new location?</span></span>

<span data-ttu-id="46905-143">O cmdlet **Copy-Item** foi projetado para ser genérico, não apenas para copiar arquivos e pastas.</span><span class="sxs-lookup"><span data-stu-id="46905-143">The **Copy-Item** cmdlet was designed to be generic; it is not just for copying files and folders.</span></span> <span data-ttu-id="46905-144">Além disso, mesmo ao copiar arquivos e pastas, convém copiar apenas o contêiner e não os itens dentro dela.</span><span class="sxs-lookup"><span data-stu-id="46905-144">Also, even when copying files and folders, you might want to copy only the container and not the items within it.</span></span>

<span data-ttu-id="46905-145">Para copiar todo o conteúdo de uma pasta, inclua o parâmetro **Recurse** do cmdlet **Copy-Item** no comando.</span><span class="sxs-lookup"><span data-stu-id="46905-145">To copy all of the contents of a folder, include the **Recurse** parameter of the **Copy-Item** cmdlet in the command.</span></span> <span data-ttu-id="46905-146">Se você já copiou o diretório sem o seu conteúdo, adicione o parâmetro **Force** , que permite substituir a pasta vazia.</span><span class="sxs-lookup"><span data-stu-id="46905-146">If you have already copied the directory without its contents, add the **Force** parameter, which allows you to overwrite the empty folder.</span></span>

```
PS> Copy-Item -Path C:\New.Directory -Destination C:\temp -Recurse -Force -Passthru

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18   1:53 PM            New.Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

## <a name="deleting-items-remove-item"></a><span data-ttu-id="46905-147">Excluindo itens (Remove-Item)</span><span class="sxs-lookup"><span data-stu-id="46905-147">Deleting Items (Remove-Item)</span></span>

<span data-ttu-id="46905-148">Para excluir arquivos ou pastas, use o cmdlet **Remove-Item** .</span><span class="sxs-lookup"><span data-stu-id="46905-148">To delete files and folders, use the **Remove-Item** cmdlet.</span></span> <span data-ttu-id="46905-149">Cmdlets do Windows PowerShell, como o **Remove-Item** , que podem executar alterações significativas e irreversíveis, geralmente solicitarão confirmação quando você inserir seus comandos.</span><span class="sxs-lookup"><span data-stu-id="46905-149">Windows PowerShell cmdlets, such as **Remove-Item** , that can make significant, irreversible changes will often prompt for confirmation when you enter its commands.</span></span> <span data-ttu-id="46905-150">Por exemplo, se você tentar remover a pasta **New.Directory** , será solicitado a confirmar o comando, pois a pasta contém arquivos:</span><span class="sxs-lookup"><span data-stu-id="46905-150">For example, if you try to remove the **New.Directory** folder, you will be prompted to confirm the command, because the folder contains files:</span></span>

```
PS> Remove-Item C:\New.Directory

Confirm
The item at C:\temp\New.Directory has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
 sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

<span data-ttu-id="46905-151">Como **Sim** é a resposta padrão, para excluir a pasta e seus arquivos, pressione a tecla **Enter** .</span><span class="sxs-lookup"><span data-stu-id="46905-151">Because **Yes** is the default response, to delete the folder and its files, press the **Enter** key.</span></span> <span data-ttu-id="46905-152">Para remover a pasta sem confirmar, use o parâmetro **-Recurse** .</span><span class="sxs-lookup"><span data-stu-id="46905-152">To remove the folder without confirming, use the **-Recurse** parameter.</span></span>

```powershell
Remove-Item C:\temp\New.Directory -Recurse
```

## <a name="executing-items-invoke-item"></a><span data-ttu-id="46905-153">Executando itens (Invoke-Item)</span><span class="sxs-lookup"><span data-stu-id="46905-153">Executing Items (Invoke-Item)</span></span>

<span data-ttu-id="46905-154">O Windows PowerShell usa o cmdlet **Invoke-Item** para executar uma ação padrão para um arquivo ou pasta.</span><span class="sxs-lookup"><span data-stu-id="46905-154">Windows PowerShell uses the **Invoke-Item** cmdlet to perform a default action for a file or folder.</span></span> <span data-ttu-id="46905-155">Essa ação padrão é determinada pelo manipulador de aplicativo padrão no registro. O efeito é o mesmo que clicar duas vezes o item no Explorador de arquivos.</span><span class="sxs-lookup"><span data-stu-id="46905-155">This default action is determined by the default application handler in the registry; the effect is the same as if you double-click the item in File Explorer.</span></span>

<span data-ttu-id="46905-156">Por exemplo, suponha que você execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="46905-156">For example, suppose you run the following command:</span></span>

```powershell
Invoke-Item C:\WINDOWS
```

<span data-ttu-id="46905-157">Aparece uma janela do Explorer localizada em C:\\Windows, como se você tivesse clicado duas vezes na pasta C:\\Windows.</span><span class="sxs-lookup"><span data-stu-id="46905-157">An Explorer window that is located in C:\\Windows appears, just as if you had double-clicked the C:\\Windows folder.</span></span>

<span data-ttu-id="46905-158">Se você chamar o arquivo **Boot.ini** em um sistema anterior ao Windows Vista:</span><span class="sxs-lookup"><span data-stu-id="46905-158">If you invoke the **Boot.ini** file on a system prior to Windows Vista:</span></span>

```powershell
Invoke-Item C:\boot.ini
```

<span data-ttu-id="46905-159">Se o tipo de arquivo .ini estiver associado ao Bloco de Notas, o arquivo Boot.ini é aberto nele.</span><span class="sxs-lookup"><span data-stu-id="46905-159">If the .ini file type is associated with Notepad, the boot.ini file opens in Notepad.</span></span>
