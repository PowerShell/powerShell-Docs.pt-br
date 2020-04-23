---
ms.date: 06/05/2017
keywords: powershell, cmdlet
title: Caixas de listagem de seleção múltipla
ms.openlocfilehash: dcfa43ac8e7cc4ba6147f71791edbf7989af3583
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2020
ms.locfileid: "67030104"
---
# <a name="multiple-selection-list-boxes"></a><span data-ttu-id="c36a0-103">Caixas de listagem de seleção múltipla</span><span class="sxs-lookup"><span data-stu-id="c36a0-103">Multiple-selection List Boxes</span></span>

<span data-ttu-id="c36a0-104">Use o Windows PowerShell 3.0 e versões posteriores para criar um controle de caixa de listagem de seleção múltipla em um formulário personalizado do Windows.</span><span class="sxs-lookup"><span data-stu-id="c36a0-104">Use Windows PowerShell 3.0 and later releases to create a multiple-selection list box control in a custom Windows Form.</span></span>

## <a name="create-list-box-controls-that-allow-multiple-selections"></a><span data-ttu-id="c36a0-105">Criar controles de caixa de listagem que permitem seleção múltipla</span><span class="sxs-lookup"><span data-stu-id="c36a0-105">Create list box controls that allow multiple selections</span></span>

<span data-ttu-id="c36a0-106">Copie e cole o seguinte no Windows PowerShell ISE e salve-o como um script do Windows PowerShell (.ps1).</span><span class="sxs-lookup"><span data-stu-id="c36a0-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

```powershell
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object System.Windows.Forms.Form
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'

$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)

$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)

$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please make a selection from the list below:'
$form.Controls.Add($label)

$listBox = New-Object System.Windows.Forms.Listbox
$listBox.Location = New-Object System.Drawing.Point(10,40)
$listBox.Size = New-Object System.Drawing.Size(260,20)

$listBox.SelectionMode = 'MultiExtended'

[void] $listBox.Items.Add('Item 1')
[void] $listBox.Items.Add('Item 2')
[void] $listBox.Items.Add('Item 3')
[void] $listBox.Items.Add('Item 4')
[void] $listBox.Items.Add('Item 5')

$listBox.Height = 70
$form.Controls.Add($listBox)
$form.Topmost = $true

$result = $form.ShowDialog()

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItems
    $x
}
```

<span data-ttu-id="c36a0-107">O script começa carregando duas classes do .NET Framework: **System.Drawing** e **System.Windows.Forms**.</span><span class="sxs-lookup"><span data-stu-id="c36a0-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="c36a0-108">Inicie uma nova instância da classe do .NET Framework **System.Windows.Forms.Form**, que fornece um formulário em branco ou janela ao qual você pode começar a adicionar controles.</span><span class="sxs-lookup"><span data-stu-id="c36a0-108">You then start a new instance of the .NET Framework class **System.Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```powershell
$form = New-Object System.Windows.Forms.Form
```

<span data-ttu-id="c36a0-109">Depois de criar uma instância da classe Form, atribua valores a três propriedades dessa classe.</span><span class="sxs-lookup"><span data-stu-id="c36a0-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

- <span data-ttu-id="c36a0-110">**Text.**</span><span class="sxs-lookup"><span data-stu-id="c36a0-110">**Text.**</span></span> <span data-ttu-id="c36a0-111">Isso se torna o título da janela.</span><span class="sxs-lookup"><span data-stu-id="c36a0-111">This becomes the title of the window.</span></span>

- <span data-ttu-id="c36a0-112">**Size.**</span><span class="sxs-lookup"><span data-stu-id="c36a0-112">**Size.**</span></span> <span data-ttu-id="c36a0-113">Esse é o tamanho do formulário, em pixels.</span><span class="sxs-lookup"><span data-stu-id="c36a0-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="c36a0-114">O script anterior cria um formulário que possui 300 pixels de largura por 200 pixels de altura.</span><span class="sxs-lookup"><span data-stu-id="c36a0-114">The preceding script creates a form that’s 300 pixels wide by 200 pixels tall.</span></span>

- <span data-ttu-id="c36a0-115">**StartingPosition.**</span><span class="sxs-lookup"><span data-stu-id="c36a0-115">**StartingPosition.**</span></span> <span data-ttu-id="c36a0-116">Esta propriedade opcional é definida para **CenterScreen** no script precedente.</span><span class="sxs-lookup"><span data-stu-id="c36a0-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="c36a0-117">Se você não adicionar essa propriedade, o Windows seleciona um local quando o formulário aberto.</span><span class="sxs-lookup"><span data-stu-id="c36a0-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="c36a0-118">Ao configurar o **StartingPosition** para **CenterScreen**, você está exibindo automaticamente o formulário no meio da tela cada vez que ela é carregada.</span><span class="sxs-lookup"><span data-stu-id="c36a0-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```powershell
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

<span data-ttu-id="c36a0-119">Em seguida, crie um botão **OK** para seu formulário.</span><span class="sxs-lookup"><span data-stu-id="c36a0-119">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="c36a0-120">Especifique o tamanho e comportamento do botão **OK**.</span><span class="sxs-lookup"><span data-stu-id="c36a0-120">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="c36a0-121">Neste exemplo, a posição do botão é de 120 pixels a partir da borda superior do formulário e 75 pixels a partir da borda esquerda.</span><span class="sxs-lookup"><span data-stu-id="c36a0-121">In this example, the button position is 120 pixels from the form’s top edge, and 75 pixels from the left edge.</span></span> <span data-ttu-id="c36a0-122">A altura do botão é de 23 pixels, enquanto seu comprimento é de 75 pixels.</span><span class="sxs-lookup"><span data-stu-id="c36a0-122">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="c36a0-123">O script usa tipos predefinidos de formulários do Windows para determinar os comportamentos do botão.</span><span class="sxs-lookup"><span data-stu-id="c36a0-123">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Size(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="c36a0-124">Crie o botão **Cancelar** da mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="c36a0-124">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="c36a0-125">O botão **Cancelar** fica a 120 pixels da parte superior e 150 pixels da borda esquerda da janela.</span><span class="sxs-lookup"><span data-stu-id="c36a0-125">The **Cancel** button is 120 pixels from the top, but 150 pixels from the left edge of the window.</span></span>

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="c36a0-126">Em seguida, forneça o texto de rótulo na janela que descreve as informações que você deseja que os usuários forneçam.</span><span class="sxs-lookup"><span data-stu-id="c36a0-126">Next, provide label text on your window that describes the information you want users to provide.</span></span>

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please make a selection from the list below:'
$form.Controls.Add($label)
```

<span data-ttu-id="c36a0-127">Adicione o controle (no caso, uma caixa de listagem) que permite que os usuários forneçam as informações descritas no texto do rótulo.</span><span class="sxs-lookup"><span data-stu-id="c36a0-127">Add the control (in this case, a list box) that lets users provide the information you’ve described in your label text.</span></span> <span data-ttu-id="c36a0-128">Há muitos outros controles que você pode aplicar além de caixas de texto. Para ver mais controles, consulte [Namespace System.Windows.Forms](https://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) no MSDN.</span><span class="sxs-lookup"><span data-stu-id="c36a0-128">There are many other controls you can apply besides text boxes; for more controls, see [System.Windows.Forms Namespace](https://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) on MSDN.</span></span>

```powershell
$listBox = New-Object System.Windows.Forms.Listbox
$listBox.Location = New-Object System.Drawing.Point(10,40)
$listBox.Size = New-Object System.Drawing.Size(260,20)
```

<span data-ttu-id="c36a0-129">Veja como especificar que você deseja que os usuários selecionem múltiplos valores na lista.</span><span class="sxs-lookup"><span data-stu-id="c36a0-129">Here’s how you specify that you want to allow users to select multiple values from the list.</span></span>

```powershell
$listBox.SelectionMode = 'MultiExtended'
```

<span data-ttu-id="c36a0-130">Na próxima seção, você deve especificar os valores que você deseja que a caixa de listagem mostre para os usuários.</span><span class="sxs-lookup"><span data-stu-id="c36a0-130">In the next section, you specify the values you want the list box to display to users.</span></span>

```powershell
[void] $listBox.Items.Add('Item 1')
[void] $listBox.Items.Add('Item 2')
[void] $listBox.Items.Add('Item 3')
[void] $listBox.Items.Add('Item 4')
[void] $listBox.Items.Add('Item 5')
```

<span data-ttu-id="c36a0-131">Especifica a altura máxima do controle de caixa de listagem.</span><span class="sxs-lookup"><span data-stu-id="c36a0-131">Specify the maximum height of the list box control.</span></span>

```powershell
$listBox.Height = 70
```

<span data-ttu-id="c36a0-132">Adicione o controle de caixa de listagem ao formulário e instrua o Windows a abrir o formulário sobre outras janelas e caixas de diálogo quando ela é aberta.</span><span class="sxs-lookup"><span data-stu-id="c36a0-132">Add the list box control to your form, and instruct Windows to open the form atop other windows and dialog boxes when it’s opened.</span></span>

```powershell
$form.Controls.Add($listBox)
$form.Topmost = $true
```

<span data-ttu-id="c36a0-133">Adicione a seguinte linha de código para exibir o formulário do Windows.</span><span class="sxs-lookup"><span data-stu-id="c36a0-133">Add the following line of code to display the form in Windows.</span></span>

```powershell
$result = $form.ShowDialog()
```

<span data-ttu-id="c36a0-134">Por fim, o código dentro do bloco **If** instrui o Windows sobre o que fazer com o formulário depois que os usuários selecionam uma opção ou mais opções na caixa de listagem e clicam no botão **OK** ou pressionam a tecla **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c36a0-134">Finally, the code inside the **If** block instructs Windows what to do with the form after users select one or more options from the list box, and then click the **OK** button or press the **Enter** key.</span></span>

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItems
    $x
}
```

## <a name="see-also"></a><span data-ttu-id="c36a0-135">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="c36a0-135">See Also</span></span>

- [<span data-ttu-id="c36a0-136">Ei Scripting Guy: por que esses exemplos de GUI do PowerShell não funcionam?</span><span class="sxs-lookup"><span data-stu-id="c36a0-136">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](https://go.microsoft.com/fwlink/?LinkId=506644)
- [<span data-ttu-id="c36a0-137">GitHub: WinFormsExampleUpdates do Dave Wyatt</span><span class="sxs-lookup"><span data-stu-id="c36a0-137">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [<span data-ttu-id="c36a0-138">Dica da semana do Windows PowerShell: caixas de listagem de seleção múltipla – E muito mais!</span><span class="sxs-lookup"><span data-stu-id="c36a0-138">Windows PowerShell Tip of the Week:  Multi-Select List Boxes - And More!</span></span>](https://technet.microsoft.com/library/ff730950.aspx)
