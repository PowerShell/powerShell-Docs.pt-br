---
ms.date: 06/05/2017
keywords: powershell, cmdlet
title: Criando uma caixa de entrada personalizada
ms.openlocfilehash: 9c1c3c72482157e849c0259e7d2e25ed969a4aab
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "67030231"
---
# <a name="creating-a-custom-input-box"></a><span data-ttu-id="d557c-103">Criando uma caixa de entrada personalizada</span><span class="sxs-lookup"><span data-stu-id="d557c-103">Creating a Custom Input Box</span></span>

<span data-ttu-id="d557c-104">Script de uma caixa de entrada gráfica personalizada usando recursos de criação de formulário do Microsoft .NET Framework no Windows PowerShell 3.0 e versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="d557c-104">Script a graphical custom input box by using Microsoft .NET Framework form-building features in Windows PowerShell 3.0 and later releases.</span></span>

## <a name="create-a-custom-graphical-input-box"></a><span data-ttu-id="d557c-105">Criar uma caixa de entrada gráfica personalizada</span><span class="sxs-lookup"><span data-stu-id="d557c-105">Create a custom, graphical input box</span></span>

<span data-ttu-id="d557c-106">Copie e cole o seguinte no Windows PowerShell ISE e salve-o como um script do Windows PowerShell (.ps1).</span><span class="sxs-lookup"><span data-stu-id="d557c-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

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
$label.Text = 'Please enter the information in the space below:'
$form.Controls.Add($label)

$textBox = New-Object System.Windows.Forms.TextBox
$textBox.Location = New-Object System.Drawing.Point(10,40)
$textBox.Size = New-Object System.Drawing.Size(260,20)
$form.Controls.Add($textBox)

$form.Topmost = $true

$form.Add_Shown({$textBox.Select()})
$result = $form.ShowDialog()

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $textBox.Text
    $x
}
```

<span data-ttu-id="d557c-107">O script começa carregando duas classes do .NET Framework: **System.Drawing** e **System.Windows.Forms**.</span><span class="sxs-lookup"><span data-stu-id="d557c-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="d557c-108">Inicie uma nova instância da classe do .NET Framework **System.Windows.Forms.Form**, que fornece um formulário em branco ou janela ao qual você pode começar a adicionar controles.</span><span class="sxs-lookup"><span data-stu-id="d557c-108">You then start a new instance of the .NET Framework class **System.Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```powershell
$form = New-Object System.Windows.Forms.Form
```

<span data-ttu-id="d557c-109">Depois de criar uma instância da classe Form, atribua valores a três propriedades dessa classe.</span><span class="sxs-lookup"><span data-stu-id="d557c-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

- <span data-ttu-id="d557c-110">**Text.**</span><span class="sxs-lookup"><span data-stu-id="d557c-110">**Text.**</span></span> <span data-ttu-id="d557c-111">Isso se torna o título da janela.</span><span class="sxs-lookup"><span data-stu-id="d557c-111">This becomes the title of the window.</span></span>

- <span data-ttu-id="d557c-112">**Size.**</span><span class="sxs-lookup"><span data-stu-id="d557c-112">**Size.**</span></span> <span data-ttu-id="d557c-113">Esse é o tamanho do formulário, em pixels.</span><span class="sxs-lookup"><span data-stu-id="d557c-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="d557c-114">O script anterior cria um formulário que possui 300 pixels de largura por 200 pixels de altura.</span><span class="sxs-lookup"><span data-stu-id="d557c-114">The preceding script creates a form that’s 300 pixels wide by 200 pixels tall.</span></span>

- <span data-ttu-id="d557c-115">**StartingPosition.**</span><span class="sxs-lookup"><span data-stu-id="d557c-115">**StartingPosition.**</span></span> <span data-ttu-id="d557c-116">Esta propriedade opcional é definida para **CenterScreen** no script precedente.</span><span class="sxs-lookup"><span data-stu-id="d557c-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="d557c-117">Se você não adicionar essa propriedade, o Windows seleciona um local quando o formulário aberto.</span><span class="sxs-lookup"><span data-stu-id="d557c-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="d557c-118">Ao configurar o **StartingPosition** para **CenterScreen**, você está exibindo automaticamente o formulário no meio da tela cada vez que ela é carregada.</span><span class="sxs-lookup"><span data-stu-id="d557c-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```powershell
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

<span data-ttu-id="d557c-119">Em seguida, crie um botão **OK** para seu formulário.</span><span class="sxs-lookup"><span data-stu-id="d557c-119">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="d557c-120">Especifique o tamanho e comportamento do botão **OK**.</span><span class="sxs-lookup"><span data-stu-id="d557c-120">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="d557c-121">Neste exemplo, a posição do botão é de 120 pixels a partir da borda superior do formulário e 75 pixels a partir da borda esquerda.</span><span class="sxs-lookup"><span data-stu-id="d557c-121">In this example, the button position is 120 pixels from the form’s top edge, and 75 pixels from the left edge.</span></span> <span data-ttu-id="d557c-122">A altura do botão é de 23 pixels, enquanto seu comprimento é de 75 pixels.</span><span class="sxs-lookup"><span data-stu-id="d557c-122">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="d557c-123">O script usa tipos predefinidos de formulários do Windows para determinar os comportamentos do botão.</span><span class="sxs-lookup"><span data-stu-id="d557c-123">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="d557c-124">Crie o botão **Cancelar** da mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="d557c-124">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="d557c-125">O botão **Cancelar** fica a 120 pixels da parte superior e 150 pixels da borda esquerda da janela.</span><span class="sxs-lookup"><span data-stu-id="d557c-125">The **Cancel** button is 120 pixels from the top, but 150 pixels from the left edge of the window.</span></span>

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="d557c-126">Em seguida, forneça o texto de rótulo na janela que descreve as informações que você deseja que os usuários forneçam.</span><span class="sxs-lookup"><span data-stu-id="d557c-126">Next, provide label text on your window that describes the information you want users to provide.</span></span>

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please enter the information in the space below:'
$form.Controls.Add($label)
```

<span data-ttu-id="d557c-127">Adicione o controle (no caso, uma caixa de texto) que permite que os usuários forneçam as informações descritas no texto do rótulo.</span><span class="sxs-lookup"><span data-stu-id="d557c-127">Add the control (in this case, a text box) that lets users provide the information you’ve described in your label text.</span></span> <span data-ttu-id="d557c-128">Há muitos outros controles que você pode aplicar além de caixas de texto. Para ver mais controles, consulte [Namespace System.Windows.Forms](https://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) no MSDN.</span><span class="sxs-lookup"><span data-stu-id="d557c-128">There are many other controls you can apply besides text boxes; for more controls, see [System.Windows.Forms Namespace](https://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) on MSDN.</span></span>

```powershell
$textBox = New-Object System.Windows.Forms.TextBox
$textBox.Location = New-Object System.Drawing.Point(10,40)
$textBox.Size = New-Object System.Drawing.Size(260,20)
$form.Controls.Add($textBox)
```

<span data-ttu-id="d557c-129">Defina a propriedade **Topmost** como **$true** para forçar a janela a abrir por cima de outras janelas e caixas de diálogo abertas.</span><span class="sxs-lookup"><span data-stu-id="d557c-129">Set the **Topmost** property to **$true** to force the window to open atop other open windows and dialog boxes.</span></span>

```powershell
$form.Topmost = $true
```

<span data-ttu-id="d557c-130">Em seguida, adicione esta linha de código para ativar o formulário e defina o foco para a caixa de texto que você criou.</span><span class="sxs-lookup"><span data-stu-id="d557c-130">Next, add this line of code to activate the form, and set the focus to the text box that you created.</span></span>

```powershell
$form.Add_Shown({$textBox.Select()})
```

<span data-ttu-id="d557c-131">Adicione a seguinte linha de código para exibir o formulário do Windows.</span><span class="sxs-lookup"><span data-stu-id="d557c-131">Add the following line of code to display the form in Windows.</span></span>

```powershell
$result = $form.ShowDialog()
```

<span data-ttu-id="d557c-132">Por fim, o código dentro do bloco **If** instrui o Windows sobre o que fazer com o formulário depois que os usuários fornecem texto na caixa de texto e clicam no botão **OK** ou pressionam a tecla **Enter**.</span><span class="sxs-lookup"><span data-stu-id="d557c-132">Finally, the code inside the **If** block instructs Windows what to do with the form after users provide text in the text box, and then click the **OK** button or press the **Enter** key.</span></span>

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $textBox.Text
    $x
}
```

## <a name="see-also"></a><span data-ttu-id="d557c-133">Consulte Também</span><span class="sxs-lookup"><span data-stu-id="d557c-133">See Also</span></span>

- [<span data-ttu-id="d557c-134">Hey Scripting Guy:  por que esses exemplos de GUI do PowerShell não funcionam?</span><span class="sxs-lookup"><span data-stu-id="d557c-134">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](https://go.microsoft.com/fwlink/?LinkId=506644)
- [<span data-ttu-id="d557c-135">GitHub: WinFormsExampleUpdates de Dave Wyatt</span><span class="sxs-lookup"><span data-stu-id="d557c-135">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [<span data-ttu-id="d557c-136">Dica da semana para o Windows PowerShell:  Criando uma caixa de entrada personalizada</span><span class="sxs-lookup"><span data-stu-id="d557c-136">Windows PowerShell Tip of the Week:  Creating a Custom Input Box</span></span>](https://technet.microsoft.com/library/ff730941.aspx)
