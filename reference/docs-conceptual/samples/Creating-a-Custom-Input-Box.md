---
ms.date: 06/05/2017
keywords: powershell, cmdlet
title: Criando uma caixa de entrada personalizada
ms.openlocfilehash: ff0588b44169bc276e2833254cec60eda759e2c8
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2020
ms.locfileid: "77706182"
---
# <a name="creating-a-custom-input-box"></a>Criando uma caixa de entrada personalizada

Script de uma caixa de entrada gráfica personalizada usando recursos de criação de formulário do Microsoft .NET Framework no Windows PowerShell 3.0 e versões posteriores.

## <a name="create-a-custom-graphical-input-box"></a>Criar uma caixa de entrada gráfica personalizada

Copie e cole o seguinte no Windows PowerShell ISE e salve-o como um script do Windows PowerShell (.ps1).

```powershell
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object System.Windows.Forms.Form
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'

$okButton = New-Object System.Windows.Forms.Button
$okButton.Location = New-Object System.Drawing.Point(75,120)
$okButton.Size = New-Object System.Drawing.Size(75,23)
$okButton.Text = 'OK'
$okButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $okButton
$form.Controls.Add($okButton)

$cancelButton = New-Object System.Windows.Forms.Button
$cancelButton.Location = New-Object System.Drawing.Point(150,120)
$cancelButton.Size = New-Object System.Drawing.Size(75,23)
$cancelButton.Text = 'Cancel'
$cancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $cancelButton
$form.Controls.Add($cancelButton)

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

O script começa carregando duas classes do .NET Framework: **System.Drawing** e **System.Windows.Forms**. Inicie uma nova instância da classe do .NET Framework **System.Windows.Forms.Form**, que fornece um formulário em branco ou janela ao qual você pode começar a adicionar controles.

```powershell
$form = New-Object System.Windows.Forms.Form
```

Depois de criar uma instância da classe Form, atribua valores a três propriedades dessa classe.

- **Text.** Isso se torna o título da janela.

- **Size.** Esse é o tamanho do formulário, em pixels. O script anterior cria um formulário que possui 300 pixels de largura por 200 pixels de altura.

- **StartingPosition.** Esta propriedade opcional é definida para **CenterScreen** no script precedente.
  Se você não adicionar essa propriedade, o Windows seleciona um local quando o formulário aberto. Ao configurar o **StartingPosition** para **CenterScreen**, você está exibindo automaticamente o formulário no meio da tela cada vez que ela é carregada.

```powershell
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

Em seguida, crie um botão **OK** para seu formulário. Especifique o tamanho e comportamento do botão **OK**. Neste exemplo, a posição do botão é de 120 pixels a partir da borda superior do formulário e 75 pixels a partir da borda esquerda. A altura do botão é de 23 pixels, enquanto seu comprimento é de 75 pixels. O script usa tipos predefinidos de formulários do Windows para determinar os comportamentos do botão.

```powershell
$okButton = New-Object System.Windows.Forms.Button
$okButton.Location = New-Object System.Drawing.Point(75,120)
$okButton.Size = New-Object System.Drawing.Size(75,23)
$okButton.Text = 'OK'
$okButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

Crie o botão **Cancelar** da mesma maneira. O botão **Cancelar** fica a 120 pixels da parte superior e 150 pixels da borda esquerda da janela.

```powershell
$cancelButton = New-Object System.Windows.Forms.Button
$cancelButton.Location = New-Object System.Drawing.Point(150,120)
$cancelButton.Size = New-Object System.Drawing.Size(75,23)
$cancelButton.Text = 'Cancel'
$cancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $cancelButton
$form.Controls.Add($cancelButton)
```

Em seguida, forneça o texto de rótulo na janela que descreve as informações que você deseja que os usuários forneçam.

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please enter the information in the space below:'
$form.Controls.Add($label)
```

Adicione o controle (no caso, uma caixa de texto) que permite que os usuários forneçam as informações descritas no texto do rótulo. Há muitos outros controles que você pode aplicar além de caixas de texto. Para ver mais controles, consulte [Namespace System.Windows.Forms](/dotnet/api/system.windows.forms) no MSDN.

```powershell
$textBox = New-Object System.Windows.Forms.TextBox
$textBox.Location = New-Object System.Drawing.Point(10,40)
$textBox.Size = New-Object System.Drawing.Size(260,20)
$form.Controls.Add($textBox)
```

Defina a propriedade **Topmost** como **$true** para forçar a janela a abrir por cima de outras janelas e caixas de diálogo abertas.

```powershell
$form.Topmost = $true
```

Em seguida, adicione esta linha de código para ativar o formulário e defina o foco para a caixa de texto que você criou.

```powershell
$form.Add_Shown({$textBox.Select()})
```

Adicione a seguinte linha de código para exibir o formulário do Windows.

```powershell
$result = $form.ShowDialog()
```

Por fim, o código dentro do bloco **If** instrui o Windows sobre o que fazer com o formulário depois que os usuários fornecem texto na caixa de texto e clicam no botão **OK** ou pressionam a tecla **Enter**.

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $textBox.Text
    $x
}
```

## <a name="see-also"></a>Consulte Também

- [GitHub: WinFormsExampleUpdates do Dave Wyatt](/previous-versions/windows/it-pro/windows-powershell-1.0/ff730941(v=technet.10))
- [Windows PowerShell Tip of the Week: Creating a Custom Input Box](https://technet.microsoft.com/library/ff730941.aspx) (Dica da Semana do Windows PowerShell: criar uma caixa de entrada personalizada)
