---
ms.date: 06/05/2017
keywords: powershell, cmdlet
title: Trabalhando com entradas do Registro
ms.openlocfilehash: c1fd6f57f13240eb2039f2d5756796678800aee0
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2020
ms.locfileid: "67030722"
---
# <a name="working-with-registry-entries"></a><span data-ttu-id="33337-103">Trabalhando com entradas do Registro</span><span class="sxs-lookup"><span data-stu-id="33337-103">Working with Registry Entries</span></span>

<span data-ttu-id="33337-104">Como entradas do registro são propriedades de chaves e, como tal, não podem ser navegadas diretamente, precisamos usar uma abordagem ligeiramente diferente ao trabalhar com elas.</span><span class="sxs-lookup"><span data-stu-id="33337-104">Because registry entries are properties of keys and, as such, cannot be directly browsed, we need to take a slightly different approach when working with them.</span></span>

## <a name="listing-registry-entries"></a><span data-ttu-id="33337-105">Listando as entradas do registro</span><span class="sxs-lookup"><span data-stu-id="33337-105">Listing Registry Entries</span></span>

<span data-ttu-id="33337-106">Há diversas maneiras de examinar as entradas do registro.</span><span class="sxs-lookup"><span data-stu-id="33337-106">There are many different ways to examine registry entries.</span></span> <span data-ttu-id="33337-107">A maneira mais simples é obter os nomes de propriedade associados a uma chave.</span><span class="sxs-lookup"><span data-stu-id="33337-107">The simplest way is to get the property names associated with a key.</span></span> <span data-ttu-id="33337-108">Por exemplo, para ver os nomes das entradas na chave do registro `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion`, use `Get-Item`.</span><span class="sxs-lookup"><span data-stu-id="33337-108">For example, to see the names of the entries in the registry key `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion`, use `Get-Item`.</span></span> <span data-ttu-id="33337-109">Chaves do registro possuem uma propriedade com o nome genérico de "Property", que é uma lista de entradas do registro na chave.</span><span class="sxs-lookup"><span data-stu-id="33337-109">Registry keys have a property with the generic name of "Property" that is a list of registry entries in the key.</span></span>
<span data-ttu-id="33337-110">O comando a seguir seleciona a propriedade Property e expande os itens para que eles sejam exibidos em uma lista:</span><span class="sxs-lookup"><span data-stu-id="33337-110">The following command selects the Property property and expands the items so that they are displayed in a list:</span></span>

```powershell
Get-Item -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion |
  Select-Object -ExpandProperty Property
```

```Output
DevicePath
MediaPathUnexpanded
ProgramFilesDir
CommonFilesDir
ProductId
```

<span data-ttu-id="33337-111">Para exibir as entradas do Registro em um formato mais legível, use `Get-ItemProperty`:</span><span class="sxs-lookup"><span data-stu-id="33337-111">To view the registry entries in a more readable form, use `Get-ItemProperty`:</span></span>

```powershell
Get-ItemProperty -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
```

```Output
PSPath              : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SO
                      FTWARE\Microsoft\Windows\CurrentVersion
PSParentPath        : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SO
                      FTWARE\Microsoft\Windows
PSChildName         : CurrentVersion
PSDrive             : HKLM
PSProvider          : Microsoft.PowerShell.Core\Registry
DevicePath          : C:\WINDOWS\inf
MediaPathUnexpanded : C:\WINDOWS\Media
ProgramFilesDir     : C:\Program Files
CommonFilesDir      : C:\Program Files\Common Files
ProductId           : 76487-338-1167776-22465
WallPaperDir        : C:\WINDOWS\Web\Wallpaper
MediaPath           : C:\WINDOWS\Media
ProgramFilesPath    : C:\Program Files
PF_AccessoriesName  : Accessories
(default)           :
```

<span data-ttu-id="33337-112">Todas as propriedades relacionadas ao Windows PowerShell para a chave são precedidas por "PS", tal como **PSPath**, **PSParentPath**, **PSChildName** e **PSProvider**.</span><span class="sxs-lookup"><span data-stu-id="33337-112">The Windows PowerShell-related properties for the key are all prefixed with "PS", such as **PSPath**, **PSParentPath**, **PSChildName**, and **PSProvider**.</span></span>

<span data-ttu-id="33337-113">Você pode usar a notação `*.*` para se referir ao local atual.</span><span class="sxs-lookup"><span data-stu-id="33337-113">You can use the `*.*` notation for referring to the current location.</span></span> <span data-ttu-id="33337-114">Você pode usar `Set-Location` para primeiro mudar para o contêiner do registro **CurrentVersion**:</span><span class="sxs-lookup"><span data-stu-id="33337-114">You can use `Set-Location` to change to the **CurrentVersion** registry container first:</span></span>

```powershell
Set-Location -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
```

<span data-ttu-id="33337-115">Como alternativa, você pode usar o HKLM PSDrive interno com `Set-Location`:</span><span class="sxs-lookup"><span data-stu-id="33337-115">Alternatively, you can use the built-in HKLM PSDrive with `Set-Location`:</span></span>

```powershell
Set-Location -Path hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion
```

<span data-ttu-id="33337-116">Você pode então usar a notação `*.*` para o local atual listar as propriedades sem especificar um caminho completo:</span><span class="sxs-lookup"><span data-stu-id="33337-116">You can then use the `*.*` notation for the current location to list the properties without specifying a full path:</span></span>

```powershell
Get-ItemProperty -Path .
```

```Output
...
DevicePath          : C:\WINDOWS\inf
MediaPathUnexpanded : C:\WINDOWS\Media
ProgramFilesDir     : C:\Program Files
...
```

<span data-ttu-id="33337-117">A expansão de caminho funciona da mesma maneira que no sistema de arquivos e, portanto, nesse local, é possível obter a listagem de **ItemProperty** para `HKLM:\SOFTWARE\Microsoft\Windows\Help` usando `Get-ItemProperty -Path ..\Help`.</span><span class="sxs-lookup"><span data-stu-id="33337-117">Path expansion works the same as it does within the file system, so from this location you can get the **ItemProperty** listing for `HKLM:\SOFTWARE\Microsoft\Windows\Help` by using `Get-ItemProperty -Path ..\Help`.</span></span>

## <a name="getting-a-single-registry-entry"></a><span data-ttu-id="33337-118">Obtendo uma única entrada de registro</span><span class="sxs-lookup"><span data-stu-id="33337-118">Getting a Single Registry Entry</span></span>

<span data-ttu-id="33337-119">Se você desejar obter uma entrada específica de uma chave do registro, poderá usar várias abordagens.</span><span class="sxs-lookup"><span data-stu-id="33337-119">If you want to retrieve a specific entry in a registry key, you can use one of several possible approaches.</span></span> <span data-ttu-id="33337-120">Este exemplo localiza o valor de **DevicePath** em `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion`.</span><span class="sxs-lookup"><span data-stu-id="33337-120">This example finds the value of **DevicePath** in `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion`.</span></span>

<span data-ttu-id="33337-121">Com `Get-ItemProperty`, use o parâmetro **Path** para especificar o nome da chave e o parâmetro **Name** para especificar o nome da entrada **DevicePath**.</span><span class="sxs-lookup"><span data-stu-id="33337-121">Using `Get-ItemProperty`, use the **Path** parameter to specify the name of the key, and the **Name** parameter to specify the name of the **DevicePath** entry.</span></span>

```powershell
Get-ItemProperty -Path HKLM:\Software\Microsoft\Windows\CurrentVersion -Name DevicePath
```

```Output
PSPath       : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\
               Microsoft\Windows\CurrentVersion
PSParentPath : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\
               Microsoft\Windows
PSChildName  : CurrentVersion
PSDrive      : HKLM
PSProvider   : Microsoft.PowerShell.Core\Registry
DevicePath   : C:\WINDOWS\inf
```

<span data-ttu-id="33337-122">Esse comando retorna as propriedades padrão do Windows PowerShell, bem como a propriedade **DevicePath**.</span><span class="sxs-lookup"><span data-stu-id="33337-122">This command returns the standard Windows PowerShell properties as well as the **DevicePath** property.</span></span>

> [!NOTE]
> <span data-ttu-id="33337-123">Embora `Get-ItemProperty` tenha os parâmetros **Filter**, **Include** e **Exclude**, eles não podem ser usados para filtrar pelo nome da propriedade.</span><span class="sxs-lookup"><span data-stu-id="33337-123">Although `Get-ItemProperty` has **Filter**, **Include**, and **Exclude** parameters, they cannot be used to filter by property name.</span></span> <span data-ttu-id="33337-124">Esses parâmetros se referem às chaves do registro, que são caminhos de item e não entradas do registro.</span><span class="sxs-lookup"><span data-stu-id="33337-124">These parameters refer to registry keys, which are item paths and not registry entries.</span></span> <span data-ttu-id="33337-125">Entradas de registro são propriedades do item.</span><span class="sxs-lookup"><span data-stu-id="33337-125">Registry entries which are item properties.</span></span>

<span data-ttu-id="33337-126">Outra opção é usar a ferramenta de linha de comando Reg.exe.</span><span class="sxs-lookup"><span data-stu-id="33337-126">Another option is to use the Reg.exe command line tool.</span></span> <span data-ttu-id="33337-127">Para obter ajuda com reg.exe, digite `reg.exe /?` em um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="33337-127">For help with reg.exe, type `reg.exe /?` at a command prompt.</span></span> <span data-ttu-id="33337-128">Para localizar a entrada DevicePath, use reg.exe, conforme mostrado no comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="33337-128">To find the DevicePath entry, use reg.exe as shown in the following command:</span></span>

```powershell
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion /v DevicePath
```

```Output
! REG.EXE VERSION 3.0

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
    DevicePath  REG_EXPAND_SZ   %SystemRoot%\inf
```

<span data-ttu-id="33337-129">Você também pode usar o objeto COM **WshShell** para localizar algumas entradas do registro, embora esse método não funcione com dados binários grandes ou nomes de entrada do Registro que incluam caracteres como "\\").</span><span class="sxs-lookup"><span data-stu-id="33337-129">You can also use the **WshShell** COM object as well to find some registry entries, although this method does not work with large binary data or with registry entry names that include characters such as "\\").</span></span> <span data-ttu-id="33337-130">Acrescente o nome da propriedade ao caminho do item com um separador \\:</span><span class="sxs-lookup"><span data-stu-id="33337-130">Append the property name to the item path with a \\ separator:</span></span>

```powershell
(New-Object -ComObject WScript.Shell).RegRead("HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\DevicePath")
```

```Output
%SystemRoot%\inf
```

## <a name="setting-a-single-registry-entry"></a><span data-ttu-id="33337-131">Configuração de uma única entrada de registro</span><span class="sxs-lookup"><span data-stu-id="33337-131">Setting a Single Registry Entry</span></span>

<span data-ttu-id="33337-132">Se você quiser obter uma entrada específica em uma chave do registro, pode usar várias abordagens.</span><span class="sxs-lookup"><span data-stu-id="33337-132">If you want to change a specific entry in a registry key, you can use one of several possible approaches.</span></span> <span data-ttu-id="33337-133">Este exemplo modifica a entrada **Path** em `HKEY_CURRENT_USER\Environment`.</span><span class="sxs-lookup"><span data-stu-id="33337-133">This example modifies the **Path** entry under `HKEY_CURRENT_USER\Environment`.</span></span> <span data-ttu-id="33337-134">A entrada **Path** especifica onde localizar os arquivos executáveis.</span><span class="sxs-lookup"><span data-stu-id="33337-134">The **Path** entry specifies where to find executable files.</span></span>

1. <span data-ttu-id="33337-135">Recupere o valor atual da entrada **Path** usando `Get-ItemProperty`.</span><span class="sxs-lookup"><span data-stu-id="33337-135">Retrieve the current value of the **Path** entry using `Get-ItemProperty`.</span></span>
2. <span data-ttu-id="33337-136">Adicionar o novo valor, separando-o com um `;`.</span><span class="sxs-lookup"><span data-stu-id="33337-136">Add the new value, separating it with a `;`.</span></span>
3. <span data-ttu-id="33337-137">Use `Set-ItemProperty` com a chave especificada, o nome da entrada e o valor para modificar a entrada do registro.</span><span class="sxs-lookup"><span data-stu-id="33337-137">Use `Set-ItemProperty` with the specified key, entry name, and value to modify the registry entry.</span></span>

```powershell
$value = Get-ItemProperty -Path HKCU:\Environment -Name Path
$newpath = $value.Path += ";C:\src\bin\"
Set-ItemProperty -Path HKCU:\Environment -Name Path -Value $newpath
```

> [!NOTE]
> <span data-ttu-id="33337-138">Embora `Set-ItemProperty` tenha os parâmetros **Filter**, **Include** e **Exclude**, eles não podem ser usados para filtrar pelo nome da propriedade.</span><span class="sxs-lookup"><span data-stu-id="33337-138">Although `Set-ItemProperty` has **Filter**, **Include**, and **Exclude** parameters, they cannot be used to filter by property name.</span></span> <span data-ttu-id="33337-139">Esses parâmetros se referem às chaves do registro, (que são caminhos de item e não entradas do registro) que são propriedades do item.</span><span class="sxs-lookup"><span data-stu-id="33337-139">These parameters refer to registry keys—which are item paths—and not registry entries—which are item properties.</span></span>

<span data-ttu-id="33337-140">Outra opção é usar a ferramenta de linha de comando Reg.exe.</span><span class="sxs-lookup"><span data-stu-id="33337-140">Another option is to use the Reg.exe command line tool.</span></span> <span data-ttu-id="33337-141">Para obter ajuda com reg.exe, digite **reg.exe /?**</span><span class="sxs-lookup"><span data-stu-id="33337-141">For help with reg.exe, type **reg.exe /?**</span></span>
<span data-ttu-id="33337-142">em um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="33337-142">at a command prompt.</span></span>

<span data-ttu-id="33337-143">O exemplo a seguir altera a entrada **Path** ao remover o caminho adicionado no exemplo acima.</span><span class="sxs-lookup"><span data-stu-id="33337-143">The following example changes the **Path** entry by removing the path added in the example above.</span></span>
<span data-ttu-id="33337-144">`Get-ItemProperty` ainda é usado para recuperar o valor atual para evitar ter que analisar a cadeia de caracteres retornada de `reg query`.</span><span class="sxs-lookup"><span data-stu-id="33337-144">`Get-ItemProperty` is still used to retrieve the current value to avoid having to parse the string returned from `reg query`.</span></span> <span data-ttu-id="33337-145">Os métodos **SubString** e **LastIndexOf** são usados para recuperar o último caminho adicionado à entrada **Path**.</span><span class="sxs-lookup"><span data-stu-id="33337-145">The **SubString** and **LastIndexOf** methods are used to retrieve the last path added to the **Path** entry.</span></span>

```powershell
$value = Get-ItemProperty -Path HKCU:\Environment -Name Path
$newpath = $value.Path.SubString(0, $value.Path.LastIndexOf(';'))
reg add HKCU\Environment /v Path /d $newpath /f
```

```Output
The operation completed successfully.
```

## <a name="creating-new-registry-entries"></a><span data-ttu-id="33337-146">Criando novas entradas do registro</span><span class="sxs-lookup"><span data-stu-id="33337-146">Creating New Registry Entries</span></span>

<span data-ttu-id="33337-147">Para adicionar uma nova entrada denominada "PowerShellPath" à chave **CurrentVersion**, use `New-ItemProperty` com o caminho para a chave, o nome da entrada e o valor da entrada.</span><span class="sxs-lookup"><span data-stu-id="33337-147">To add a new entry named "PowerShellPath" to the **CurrentVersion** key, use `New-ItemProperty` with the path to the key, the entry name, and the value of the entry.</span></span> <span data-ttu-id="33337-148">Neste exemplo, obtemos o valor da variável `$PSHome` do Windows PowerShell, que armazena o caminho para o diretório de instalação do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33337-148">For this example, we will take the value of the Windows PowerShell variable `$PSHome`, which stores the path to the installation directory for Windows PowerShell.</span></span>

<span data-ttu-id="33337-149">Você pode adicionar a nova entrada à chave usando o seguinte comando, e ele também retorna informações sobre a nova entrada:</span><span class="sxs-lookup"><span data-stu-id="33337-149">You can add the new entry to the key by using the following command, and the command also returns information about the new entry:</span></span>

```powershell
New-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -PropertyType String -Value $PSHome
```

```Output
PSPath         : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
PSParentPath   : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows
PSChildName    : CurrentVersion
PSDrive        : HKLM
PSProvider     : Microsoft.PowerShell.Core\Registry
PowerShellPath : C:\Program Files\Windows PowerShell\v1.0
```

<span data-ttu-id="33337-150">O **PropertyType** deve ter o mesmo nome de um membro da enumeração **Microsoft.Win32.RegistryValueKind** da tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="33337-150">The **PropertyType** must be the name of a **Microsoft.Win32.RegistryValueKind** enumeration member from the following table:</span></span>

|<span data-ttu-id="33337-151">Valor de PropertyType</span><span class="sxs-lookup"><span data-stu-id="33337-151">PropertyType Value</span></span>|<span data-ttu-id="33337-152">Significado</span><span class="sxs-lookup"><span data-stu-id="33337-152">Meaning</span></span>|
|----------------------|-----------|
|<span data-ttu-id="33337-153">Binário</span><span class="sxs-lookup"><span data-stu-id="33337-153">Binary</span></span>|<span data-ttu-id="33337-154">Dados binários</span><span class="sxs-lookup"><span data-stu-id="33337-154">Binary data</span></span>|
|<span data-ttu-id="33337-155">DWord</span><span class="sxs-lookup"><span data-stu-id="33337-155">DWord</span></span>|<span data-ttu-id="33337-156">Um número UInt32 válido</span><span class="sxs-lookup"><span data-stu-id="33337-156">A number that is a valid UInt32</span></span>|
|<span data-ttu-id="33337-157">ExpandString</span><span class="sxs-lookup"><span data-stu-id="33337-157">ExpandString</span></span>|<span data-ttu-id="33337-158">Uma cadeia de caracteres que pode conter variáveis de ambiente que são expandidos dinamicamente</span><span class="sxs-lookup"><span data-stu-id="33337-158">A string that can contain environment variables that are dynamically expanded</span></span>|
|<span data-ttu-id="33337-159">MultiString</span><span class="sxs-lookup"><span data-stu-id="33337-159">MultiString</span></span>|<span data-ttu-id="33337-160">Uma cadeia de caracteres de várias linhas</span><span class="sxs-lookup"><span data-stu-id="33337-160">A multiline string</span></span>|
|<span data-ttu-id="33337-161">String</span><span class="sxs-lookup"><span data-stu-id="33337-161">String</span></span>|<span data-ttu-id="33337-162">Qualquer valor de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="33337-162">Any string value</span></span>|
|<span data-ttu-id="33337-163">QWord</span><span class="sxs-lookup"><span data-stu-id="33337-163">QWord</span></span>|<span data-ttu-id="33337-164">8 bytes de dados binários</span><span class="sxs-lookup"><span data-stu-id="33337-164">8 bytes of binary data</span></span>|

> [!NOTE]
> <span data-ttu-id="33337-165">Você pode adicionar uma entrada de Registro em vários locais, especificando uma matriz de valores para o parâmetro **Path**:</span><span class="sxs-lookup"><span data-stu-id="33337-165">You can add a registry entry to multiple locations by specifying an array of values for the **Path** parameter:</span></span>

```powershell
New-ItemProperty -Name PowerShellPath -PropertyType String -Value $PSHome `
  -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion, HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion
```

<span data-ttu-id="33337-166">Você também pode substituir um valor de entrada do registro pré-existente adicionando o parâmetro **Force** a qualquer comando `New-ItemProperty`.</span><span class="sxs-lookup"><span data-stu-id="33337-166">You can also overwrite a pre-existing registry entry value by adding the **Force** parameter to any `New-ItemProperty` command.</span></span>

## <a name="renaming-registry-entries"></a><span data-ttu-id="33337-167">Renomeando entradas do registro</span><span class="sxs-lookup"><span data-stu-id="33337-167">Renaming Registry Entries</span></span>

<span data-ttu-id="33337-168">Para renomear a entrada **PowerShellPath** como "PSHome", use `Rename-ItemProperty`:</span><span class="sxs-lookup"><span data-stu-id="33337-168">To rename the **PowerShellPath** entry to "PSHome," use `Rename-ItemProperty`:</span></span>

```powershell
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome
```

<span data-ttu-id="33337-169">Para exibir o valor renomeado, adicione o parâmetro **PassThru** ao comando.</span><span class="sxs-lookup"><span data-stu-id="33337-169">To display the renamed value, add the **PassThru** parameter to the command.</span></span>

```powershell
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome -passthru
```

## <a name="deleting-registry-entries"></a><span data-ttu-id="33337-170">Excluindo entradas do registro</span><span class="sxs-lookup"><span data-stu-id="33337-170">Deleting Registry Entries</span></span>

<span data-ttu-id="33337-171">Para excluir as duas entradas do registro PSHome e PowerShellPath, use `Remove-ItemProperty`:</span><span class="sxs-lookup"><span data-stu-id="33337-171">To delete both the PSHome and PowerShellPath registry entries, use `Remove-ItemProperty`:</span></span>

```powershell
Remove-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PSHome
Remove-ItemProperty -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath
```
