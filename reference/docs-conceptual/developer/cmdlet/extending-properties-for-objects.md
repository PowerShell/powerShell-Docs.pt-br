---
title: Estendendo propriedades para objetos | Microsoft Docs
ms.custom: ''
ms.date: 08/21/2019
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f33ff3e9-213c-44aa-92ab-09450e65c676
caps.latest.revision: 11
ms.openlocfilehash: 3b14007384cca0d0cfa35655aee437adf73b1ff0
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72364445"
---
# <a name="extending-properties-for-objects"></a><span data-ttu-id="e3f34-102">Estender as propriedades para objetos</span><span class="sxs-lookup"><span data-stu-id="e3f34-102">Extending Properties for Objects</span></span>

<span data-ttu-id="e3f34-103">Ao estender .NET Framework objetos, você pode adicionar propriedades de alias, propriedades de código, propriedades de observação, propriedades de script e conjuntos de propriedades aos objetos.</span><span class="sxs-lookup"><span data-stu-id="e3f34-103">When you extend .NET Framework objects, you can add alias properties, code properties, note properties, script properties, and property sets to the objects.</span></span> <span data-ttu-id="e3f34-104">O XML que define essas propriedades é descrito nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="e3f34-104">The XML that defines these properties is described in the following sections.</span></span>

> [!NOTE]
> <span data-ttu-id="e3f34-105">Os exemplos nas seções a seguir são do arquivo de tipos `Types.ps1xml` padrão no diretório de instalação do PowerShell (`$PSHOME`).</span><span class="sxs-lookup"><span data-stu-id="e3f34-105">The examples in the following sections are from the default `Types.ps1xml` types file in the PowerShell installation directory (`$PSHOME`).</span></span> <span data-ttu-id="e3f34-106">Para obter mais informações, consulte [sobre tipos. ps1xml](/powershell/module/microsoft.powershell.core/about/about_types.ps1xml).</span><span class="sxs-lookup"><span data-stu-id="e3f34-106">For more information, see [About Types.ps1xml](/powershell/module/microsoft.powershell.core/about/about_types.ps1xml).</span></span>

## <a name="alias-properties"></a><span data-ttu-id="e3f34-107">Propriedades do alias</span><span class="sxs-lookup"><span data-stu-id="e3f34-107">Alias properties</span></span>

<span data-ttu-id="e3f34-108">Uma propriedade de alias define um novo nome para uma propriedade existente.</span><span class="sxs-lookup"><span data-stu-id="e3f34-108">An alias property defines a new name for an existing property.</span></span>

<span data-ttu-id="e3f34-109">No exemplo a seguir, a propriedade **Count** é adicionada ao tipo [System. array](/dotnet/api/System.Array) .</span><span class="sxs-lookup"><span data-stu-id="e3f34-109">In the following example, the **Count** property is added to the [System.Array](/dotnet/api/System.Array) type.</span></span> <span data-ttu-id="e3f34-110">O elemento [AliasProperty](/dotnet/api/system.management.automation.psaliasproperty) define a propriedade estendida como uma propriedade de alias.</span><span class="sxs-lookup"><span data-stu-id="e3f34-110">The [AliasProperty](/dotnet/api/system.management.automation.psaliasproperty) element defines the extended property as an alias property.</span></span> <span data-ttu-id="e3f34-111">O elemento [Name](/dotnet/api/system.management.automation.psmemberinfo.name) especifica o novo nome.</span><span class="sxs-lookup"><span data-stu-id="e3f34-111">The [Name](/dotnet/api/system.management.automation.psmemberinfo.name) element specifies the new name.</span></span> <span data-ttu-id="e3f34-112">E, o elemento [ReferencedMemberName](/dotnet/api/system.management.automation.psaliasproperty.referencedmembername) especifica a propriedade existente que é referenciada pelo alias.</span><span class="sxs-lookup"><span data-stu-id="e3f34-112">And, the [ReferencedMemberName](/dotnet/api/system.management.automation.psaliasproperty.referencedmembername) element specifies the existing property that is referenced by the alias.</span></span> <span data-ttu-id="e3f34-113">Você também pode adicionar o elemento `AliasProperty` aos membros do elemento [MemberSets](/dotnet/api/system.management.automation.psmemberset) .</span><span class="sxs-lookup"><span data-stu-id="e3f34-113">You can also add the `AliasProperty` element to the members of the [MemberSets](/dotnet/api/system.management.automation.psmemberset) element.</span></span>

```xml
<Type>
  <Name>System.Array</Name>
  <Members>
    <AliasProperty>
      <Name>Count</Name>
      <ReferencedMemberName>Length</ReferencedMemberName>
    </AliasProperty>
  </Members>
</Type>
```

## <a name="code-properties"></a><span data-ttu-id="e3f34-114">Propriedades do código</span><span class="sxs-lookup"><span data-stu-id="e3f34-114">Code properties</span></span>

<span data-ttu-id="e3f34-115">Uma propriedade de código faz referência a uma propriedade estática de um objeto .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="e3f34-115">A code property references a static property of a .NET Framework object.</span></span>

<span data-ttu-id="e3f34-116">No exemplo a seguir, a propriedade **Mode** é adicionada ao tipo [System. IO. DirectoryInfo](/dotnet/api/System.IO.DirectoryInfo) .</span><span class="sxs-lookup"><span data-stu-id="e3f34-116">In the following example, the **Mode** property is added to the [System.IO.DirectoryInfo](/dotnet/api/System.IO.DirectoryInfo) type.</span></span> <span data-ttu-id="e3f34-117">O elemento [CodeProperty](/dotnet/api/system.management.automation.pscodeproperty) define a propriedade estendida como uma propriedade de código.</span><span class="sxs-lookup"><span data-stu-id="e3f34-117">The [CodeProperty](/dotnet/api/system.management.automation.pscodeproperty) element defines the extended property as a code property.</span></span> <span data-ttu-id="e3f34-118">O elemento [Name](/dotnet/api/system.management.automation.psmemberinfo.name) especifica o nome da propriedade estendida.</span><span class="sxs-lookup"><span data-stu-id="e3f34-118">The [Name](/dotnet/api/system.management.automation.psmemberinfo.name) element specifies the name of the extended property.</span></span> <span data-ttu-id="e3f34-119">E, o elemento [GetCodeReference](/dotnet/api/system.management.automation.pscodeproperty.gettercodereference) define o método estático que é referenciado pela propriedade estendida.</span><span class="sxs-lookup"><span data-stu-id="e3f34-119">And, the [GetCodeReference](/dotnet/api/system.management.automation.pscodeproperty.gettercodereference) element defines the static method that is referenced by the extended property.</span></span> <span data-ttu-id="e3f34-120">Você também pode adicionar o elemento `CodeProperty` aos membros do elemento [MemberSets](/dotnet/api/system.management.automation.psmemberset) .</span><span class="sxs-lookup"><span data-stu-id="e3f34-120">You can also add the `CodeProperty` element to the members of the [MemberSets](/dotnet/api/system.management.automation.psmemberset) element.</span></span>

```xml
<Type>
  <Name>System.IO.DirectoryInfo</Name>
  <Members>
    <CodeProperty>
      <Name>Mode</Name>
      <GetCodeReference>
        <TypeName>Microsoft.PowerShell.Commands.FileSystemProvider</TypeName>
        <MethodName>Mode</MethodName>
      </GetCodeReference>
    </CodeProperty>
  </Members>
</Type>
```

## <a name="note-properties"></a><span data-ttu-id="e3f34-121">Propriedades da observação</span><span class="sxs-lookup"><span data-stu-id="e3f34-121">Note properties</span></span>

<span data-ttu-id="e3f34-122">Uma propriedade Note define uma propriedade que tem um valor estático.</span><span class="sxs-lookup"><span data-stu-id="e3f34-122">A note property defines a property that has a static value.</span></span>

<span data-ttu-id="e3f34-123">No exemplo a seguir, a propriedade **status** , cujo valor é sempre **êxito**, é adicionada ao tipo [System. IO. DirectoryInfo](/dotnet/api/System.IO.DirectoryInfo) .</span><span class="sxs-lookup"><span data-stu-id="e3f34-123">In the following example, the **Status** property, whose value is always **Success**, is added to the [System.IO.DirectoryInfo](/dotnet/api/System.IO.DirectoryInfo) type.</span></span> <span data-ttu-id="e3f34-124">O elemento [NoteProperty](/dotnet/api/system.management.automation.psnoteproperty) define a propriedade estendida como uma propriedade de observação.</span><span class="sxs-lookup"><span data-stu-id="e3f34-124">The [NoteProperty](/dotnet/api/system.management.automation.psnoteproperty) element defines the extended property as a note property.</span></span> <span data-ttu-id="e3f34-125">O elemento [Name](/dotnet/api/system.management.automation.psmemberinfo.name) especifica o nome da propriedade estendida.</span><span class="sxs-lookup"><span data-stu-id="e3f34-125">The [Name](/dotnet/api/system.management.automation.psmemberinfo.name) element specifies the name of the extended property.</span></span> <span data-ttu-id="e3f34-126">O elemento [Value](/dotnet/api/system.management.automation.psnoteproperty.value) especifica o valor estático da propriedade estendida.</span><span class="sxs-lookup"><span data-stu-id="e3f34-126">The [Value](/dotnet/api/system.management.automation.psnoteproperty.value) element specifies the static value of the extended property.</span></span> <span data-ttu-id="e3f34-127">O elemento `NoteProperty` também pode ser adicionado aos membros do elemento [MemberSets](/dotnet/api/system.management.automation.psmemberset) .</span><span class="sxs-lookup"><span data-stu-id="e3f34-127">The `NoteProperty` element can also be added to the members of the [MemberSets](/dotnet/api/system.management.automation.psmemberset) element.</span></span>

```xml
<Type>
  <Name>System.IO.DirectoryInfo</Name>
  <Members>
    <NoteProperty>
      <Name>Status</Name>
      <Value>Success</Value>
    </NoteProperty>
  </Members>
</Type>
```

## <a name="script-properties"></a><span data-ttu-id="e3f34-128">Propriedades do script</span><span class="sxs-lookup"><span data-stu-id="e3f34-128">Script properties</span></span>

<span data-ttu-id="e3f34-129">Uma propriedade de script define uma propriedade cujo valor é a saída de um script.</span><span class="sxs-lookup"><span data-stu-id="e3f34-129">A script property defines a property whose value is the output of a script.</span></span>

<span data-ttu-id="e3f34-130">No exemplo a seguir, a propriedade **VERSIONINFO** é adicionada ao tipo [System. IO. FileInfo](/dotnet/api/System.IO.FileInfo) .</span><span class="sxs-lookup"><span data-stu-id="e3f34-130">In the following example, the **VersionInfo** property is added to the [System.IO.FileInfo](/dotnet/api/System.IO.FileInfo) type.</span></span> <span data-ttu-id="e3f34-131">O elemento [ScriptProperty](/dotnet/api/system.management.automation.psscriptproperty) define a propriedade estendida como uma propriedade de script.</span><span class="sxs-lookup"><span data-stu-id="e3f34-131">The [ScriptProperty](/dotnet/api/system.management.automation.psscriptproperty) element defines the extended property as a script property.</span></span> <span data-ttu-id="e3f34-132">O elemento [Name](/dotnet/api/system.management.automation.psmemberinfo.name) especifica o nome da propriedade estendida.</span><span class="sxs-lookup"><span data-stu-id="e3f34-132">The [Name](/dotnet/api/system.management.automation.psmemberinfo.name) element specifies the name of the extended property.</span></span> <span data-ttu-id="e3f34-133">E, o elemento [getscriptblock](/dotnet/api/system.management.automation.psscriptproperty.getterscript) especifica o script que gera o valor da propriedade.</span><span class="sxs-lookup"><span data-stu-id="e3f34-133">And, the [GetScriptBlock](/dotnet/api/system.management.automation.psscriptproperty.getterscript) element specifies the script that generates the property value.</span></span> <span data-ttu-id="e3f34-134">Você também pode adicionar o elemento `ScriptProperty` aos membros do elemento [MemberSets](/dotnet/api/system.management.automation.psmemberset) .</span><span class="sxs-lookup"><span data-stu-id="e3f34-134">You can also add the `ScriptProperty` element to the members of the [MemberSets](/dotnet/api/system.management.automation.psmemberset) element.</span></span>

```xml
<Type>
  <Name>System.IO.FileInfo</Name>
  <Members>
    <ScriptProperty>
      <Name>VersionInfo</Name>
      <GetScriptBlock>
        [System.Diagnostics.FileVersionInfo]::GetVersionInfo($this.FullName)
      </GetScriptBlock>
    </ScriptProperty>
  </Members>
</Type>
```

## <a name="property-sets"></a><span data-ttu-id="e3f34-135">Conjuntos de propriedades</span><span class="sxs-lookup"><span data-stu-id="e3f34-135">Property sets</span></span>

<span data-ttu-id="e3f34-136">Um conjunto de propriedades define um grupo de propriedades estendidas que podem ser referenciadas pelo nome do conjunto.</span><span class="sxs-lookup"><span data-stu-id="e3f34-136">A property set defines a group of extended properties that can be referenced by the name of the set.</span></span>
<span data-ttu-id="e3f34-137">Por exemplo, o parâmetro de**Propriedade** [Format-Table](/powershell/module/Microsoft.PowerShell.Utility/Format-Table)
 pode especificar um conjunto de propriedades específico a ser exibido.</span><span class="sxs-lookup"><span data-stu-id="e3f34-137">For example, the [Format-Table](/powershell/module/Microsoft.PowerShell.Utility/Format-Table)
**Property** parameter can specify a specific property set to be displayed.</span></span> <span data-ttu-id="e3f34-138">Quando um conjunto de propriedades é especificado, somente as propriedades que pertencem ao conjunto são exibidas.</span><span class="sxs-lookup"><span data-stu-id="e3f34-138">When a property set is specified, only those properties that belong to the set are displayed.</span></span>

<span data-ttu-id="e3f34-139">Não há restrição quanto ao número de conjuntos de propriedades que podem ser definidos para um objeto.</span><span class="sxs-lookup"><span data-stu-id="e3f34-139">There's no restriction on the number of property sets that can be defined for an object.</span></span> <span data-ttu-id="e3f34-140">No entanto, os conjuntos de propriedades usados para definir as propriedades de exibição padrão de um objeto devem ser especificados dentro do conjunto de membros **PSStandardMembers** .</span><span class="sxs-lookup"><span data-stu-id="e3f34-140">However, the property sets used to define the default display properties of an object must be specified within the **PSStandardMembers** member set.</span></span> <span data-ttu-id="e3f34-141">No arquivo de tipos `Types.ps1xml`, os nomes de conjunto de propriedades padrão incluem **DefaultDisplayProperty**, **DefaultDisplayPropertySet**e **DefaultKeyPropertySet**.</span><span class="sxs-lookup"><span data-stu-id="e3f34-141">In the `Types.ps1xml` types file, the default property set names include **DefaultDisplayProperty**, **DefaultDisplayPropertySet**, and **DefaultKeyPropertySet**.</span></span> <span data-ttu-id="e3f34-142">Todos os conjuntos de propriedades adicionais que você adicionar ao conjunto de membros **PSStandardMembers** serão ignorados.</span><span class="sxs-lookup"><span data-stu-id="e3f34-142">Any additional property sets that you add to the **PSStandardMembers** member set are ignored.</span></span>

<span data-ttu-id="e3f34-143">No exemplo a seguir, o conjunto de propriedades **DefaultDisplayPropertySet** é adicionado ao conjunto de membros **PSStandardMembers** do tipo [System. ServiceProcess. ServiceController](/dotnet/api/System.ServiceProcess.ServiceController) .</span><span class="sxs-lookup"><span data-stu-id="e3f34-143">In the following example, the **DefaultDisplayPropertySet** property set is added to the **PSStandardMembers** member set of the [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) type.</span></span> <span data-ttu-id="e3f34-144">O elemento [PropertySet](/dotnet/api/system.management.automation.pspropertyset) define o grupo de propriedades.</span><span class="sxs-lookup"><span data-stu-id="e3f34-144">The [PropertySet](/dotnet/api/system.management.automation.pspropertyset) element defines the group of properties.</span></span> <span data-ttu-id="e3f34-145">O elemento [Name](/dotnet/api/system.management.automation.psmemberinfo.name) especifica o nome do conjunto de propriedades.</span><span class="sxs-lookup"><span data-stu-id="e3f34-145">The [Name](/dotnet/api/system.management.automation.psmemberinfo.name) element specifies the name of the property set.</span></span> <span data-ttu-id="e3f34-146">E, o elemento [referenciaproperties](/dotnet/api/system.management.automation.pspropertyset.referencedpropertynames) especifica as propriedades do conjunto.</span><span class="sxs-lookup"><span data-stu-id="e3f34-146">And, the [ReferencedProperties](/dotnet/api/system.management.automation.pspropertyset.referencedpropertynames) element specifies the properties of the set.</span></span> <span data-ttu-id="e3f34-147">Você também pode adicionar o elemento `PropertySet` aos membros do elemento [Type](/dotnet/api/system.management.automation.pstypename) .</span><span class="sxs-lookup"><span data-stu-id="e3f34-147">You can also add the `PropertySet` element to the members of the [Type](/dotnet/api/system.management.automation.pstypename) element.</span></span>

```xml
<Type>
  <Name>System.ServiceProcess.ServiceController</Name>
  <Members>
    <MemberSet>
      <Name>PSStandardMembers</Name>
      <Members>
        <PropertySet>
           <Name>DefaultDisplayPropertySet</Name>
           <ReferencedProperties>
            <Name>Status</Name
            <Name>Name</Name>
            <Name>DisplayName</Name>
          </ReferencedProperties>
        </PropertySet>
      </Members>
    </MemberSet>
  </Members>
</Type>
```

## <a name="see-also"></a><span data-ttu-id="e3f34-148">Consulte também</span><span class="sxs-lookup"><span data-stu-id="e3f34-148">See also</span></span>

[<span data-ttu-id="e3f34-149">Sobre os tipos. ps1xml</span><span class="sxs-lookup"><span data-stu-id="e3f34-149">About Types.ps1xml</span></span>](/powershell/module/microsoft.powershell.core/about/about_types.ps1xml)

[<span data-ttu-id="e3f34-150">System. Management. Automation</span><span class="sxs-lookup"><span data-stu-id="e3f34-150">System.Management.Automation</span></span>](/dotnet/api/System.Management.Automation)

<span data-ttu-id="e3f34-151">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md) (Escrevendo um Cmdlet do Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="e3f34-151">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md)</span></span>