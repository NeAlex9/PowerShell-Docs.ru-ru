---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Создание настраиваемого поля ввода
ms.assetid: 0b12e56c-299f-40ee-afbf-d30d23ed2565
ms.openlocfilehash: 681a75a28a8fb03eb4442d5e20b32b25a337d540
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30954761"
---
# <a name="creating-a-custom-input-box"></a>Создание настраиваемого поля ввода

Создание сценария настраиваемого графического поля ввода с помощью функций создания форм Microsoft .NET Framework в Windows PowerShell 3.0 и более поздних версиях.

## <a name="create-a-custom-graphical-input-box"></a>Создание настраиваемого графического поля ввода

Скопируйте и вставьте следующий код в интегрированную среду сценариев Windows PowerShell, а затем сохраните файл как сценарий Windows PowerShell (PS1-файл).

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

Сценарий начинается с загрузки двух классов .NET Framework: **System.Drawing** и **System.Windows.Forms**. Затем вы запускаете новый экземпляр класса .NET Framework **System.Windows.Forms.Form**, предоставляющий пустую форму или окно, в которые можно добавить элементы управления.

```powershell
$form = New-Object System.Windows.Forms.Form
```

После создания экземпляра класса "Форма" назначьте значения для трех свойств этого класса.

- **Text.** Это будет заголовком окна.

- **Size.** Это размер формы в пикселях. Предыдущий сценарий создает форму шириной 300 пикселей и высотой 200 пикселей.

- **StartingPosition.** Для этого дополнительного свойства задается значение **CenterScreen** в предыдущем сценарии. Если это свойство не добавлено, Windows выберет расположение после открытия формы. Если для **StartingPosition** задать значение **CenterScreen**, форма будет автоматически отображаться в центре экрана при загрузке.

```powershell
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

Далее создайте кнопку **OК** для формы. Укажите размер и поведение кнопки **ОК**. В этом примере кнопка расположена на 120 пикселей ниже верхней границы формы и на 75 пикселей правее левой границы. Высота кнопки — 23 пикселя, а длина — 75 пикселей. Сценарий использует предопределенные типы Windows Forms для определения поведения кнопок.

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

Аналогичным образом создайте кнопку **Отмена**. Кнопка **Отмена** расположена на 120 пикселей ниже верхней границы и на 150 пикселей правее левой границы окна.

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

Далее введите текст метки в окне, который должны получить пользователи.

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please enter the information in the space below:'
$form.Controls.Add($label)
```

Добавьте элемент управления (в данном случае текстовое поле), который позволит пользователям указать сведения, описанные в тексте метки. Помимо текстового поля существует много других элементов управления, которые можно применить. Их описание см. в статье [Пространство имен System.Windows.Forms](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) на сайте MSDN.

```powershell
$textBox = New-Object System.Windows.Forms.TextBox
$textBox.Location = New-Object System.Drawing.Point(10,40)
$textBox.Size = New-Object System.Drawing.Size(260,20)
$form.Controls.Add($textBox)
```

Задайте для свойства **Topmost** значение **$true**, чтобы принудительно открыть окно поверх других диалоговых окон.

```powershell
$form.Topmost = $true
```

Затем добавьте следующую строку кода, чтобы активировать форму и установить фокус на текстовое поле, которое вы создали.

```powershell
$form.Add_Shown({$textBox.Select()})
```

Добавьте следующую строку кода для отображения формы в Windows.

```powershell
$result = $form.ShowDialog()
```

Наконец, код внутри блока **If** указывает Windows, что следует делать с формой после того, как пользователь задаст текст в поле и нажмет кнопку **ОК** или клавишу **ВВОД**.

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $textBox.Text
    $x
}
```

## <a name="see-also"></a>См. также

- [Блог Hey Scripting Guy: Why don’t these PowerShell GUI examples work? (Почему эти примеры скриптов PowerShell GUI не работают)](http://go.microsoft.com/fwlink/?LinkId=506644)
- [GitHub: Dave Wyatt's WinFormsExampleUpdates (WinFormsExampleUpdates от Дэйва Уайята)](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [Windows PowerShell Tip of the Week: Creating a Custom Input Box](http://technet.microsoft.com/library/ff730941.aspx) (Совет недели для Windows PowerShell: создание настраиваемого поля ввода)