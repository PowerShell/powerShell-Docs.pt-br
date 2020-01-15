---
ms.date: 12/31/2019
keywords: powershell, cmdlet
title: O objeto ISEMenuItem
ms.openlocfilehash: c3ffe6e8f0b28987543fe0a873c552292dc5158a
ms.sourcegitcommit: 058a6e86eac1b27ca57a11687019df98709ed709
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2020
ms.locfileid: "75736974"
---
# <a name="the-isemenuitem-object"></a><span data-ttu-id="7e485-103">O objeto ISEMenuItem</span><span class="sxs-lookup"><span data-stu-id="7e485-103">The ISEMenuItem Object</span></span>

<span data-ttu-id="7e485-104">Um objeto **ISEMenuItem** é uma instância da classe **Microsoft.PowerShell.Host.ISE.ISEMenuItem**.</span><span class="sxs-lookup"><span data-stu-id="7e485-104">An **ISEMenuItem** object is an instance of the **Microsoft.PowerShell.Host.ISE.ISEMenuItem** class.</span></span>
<span data-ttu-id="7e485-105">Todos os objetos de menu **Complementos** são instância da classe **Microsoft.PowerShell.Host.ISE.ISEMenuItem**.</span><span class="sxs-lookup"><span data-stu-id="7e485-105">All menu objects on the **Add-ons** menu are instances of the **Microsoft.PowerShell.Host.ISE.ISEMenuItem** class.</span></span>

## <a name="properties"></a><span data-ttu-id="7e485-106">Propriedades</span><span class="sxs-lookup"><span data-stu-id="7e485-106">Properties</span></span>

### <a name="displayname"></a><span data-ttu-id="7e485-107">DisplayName</span><span class="sxs-lookup"><span data-stu-id="7e485-107">DisplayName</span></span>

<span data-ttu-id="7e485-108">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="7e485-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7e485-109">A propriedade somente leitura que obtém o nome de exibição do item de menu.</span><span class="sxs-lookup"><span data-stu-id="7e485-109">The read-only property that gets the display name of the menu item.</span></span>

```powershell
# Get the display name of the Add-ons menu item
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.DisplayName
```

### <a name="action"></a><span data-ttu-id="7e485-110">Ação</span><span class="sxs-lookup"><span data-stu-id="7e485-110">Action</span></span>

<span data-ttu-id="7e485-111">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="7e485-111">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7e485-112">A propriedade somente leitura que obtém o bloco de script.</span><span class="sxs-lookup"><span data-stu-id="7e485-112">The read-only property that gets the block of script.</span></span> <span data-ttu-id="7e485-113">Quando você clicar no item de menu, ele chama a ação.</span><span class="sxs-lookup"><span data-stu-id="7e485-113">It invokes the action when you click the menu item.</span></span>

```powershell
# Get the action associated with the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action

# Invoke the script associated with the first submenu item
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action.Invoke()
```

### <a name="shortcut"></a><span data-ttu-id="7e485-114">Atalho</span><span class="sxs-lookup"><span data-stu-id="7e485-114">Shortcut</span></span>

<span data-ttu-id="7e485-115">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="7e485-115">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7e485-116">A propriedade somente leitura que obtém o atalho de teclado de entrada do Windows do item de menu.</span><span class="sxs-lookup"><span data-stu-id="7e485-116">The read-only property that gets the Windows input keyboard shortcut for the menu item.</span></span>

```powershell
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

### <a name="submenus"></a><span data-ttu-id="7e485-117">Submenus</span><span class="sxs-lookup"><span data-stu-id="7e485-117">Submenus</span></span>

<span data-ttu-id="7e485-118">Suportado no Windows PowerShell ISE 2.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="7e485-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7e485-119">A propriedade somente leitura que obtém a [lista de submenus](The-ISEMenuItemCollection-Object.md) do item de menu.</span><span class="sxs-lookup"><span data-stu-id="7e485-119">The read-only property that gets the [list of submenus](The-ISEMenuItemCollection-Object.md) of the menu item.</span></span>

```powershell
# List the submenus of the Add-ons menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus
```

## <a name="scripting-example"></a><span data-ttu-id="7e485-120">Exemplo de script</span><span class="sxs-lookup"><span data-stu-id="7e485-120">Scripting example</span></span>

<span data-ttu-id="7e485-121">Para entender melhor o uso do menu Complementos e suas propriedades programáveis, leia o exemplo de script a seguir.</span><span class="sxs-lookup"><span data-stu-id="7e485-121">To better understand the use of the Add-ons menu and its scriptable properties, read through the following scripting example.</span></span>

```powershell
# This is a scripting example that shows the use of the Add-ons menu.
# Clear the Add-ons menu if any entries currently exist
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()

# Add an Add-ons menu item with an shortcut and fast access key.
# Note the use of “_”  as opposed to the “&” for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add('_Process', {Get-Process}, 'Alt+P')
# Add a nested menu - a parent and a child submenu item.
$parentAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('Parent', $null, $null)
$parentAdded.SubMenus.Add('_Dir', {dir}, 'Alt+D')
```

## <a name="see-also"></a><span data-ttu-id="7e485-122">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="7e485-122">See Also</span></span>

- [<span data-ttu-id="7e485-123">O objeto ISEMenuItemCollection</span><span class="sxs-lookup"><span data-stu-id="7e485-123">The ISEMenuItemCollection Object</span></span>](The-ISEMenuItemCollection-Object.md)
- [<span data-ttu-id="7e485-124">Objetivo do modelo de objeto de script do ISE do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e485-124">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="7e485-125">A hierarquia de modelo de objeto do ISE</span><span class="sxs-lookup"><span data-stu-id="7e485-125">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
