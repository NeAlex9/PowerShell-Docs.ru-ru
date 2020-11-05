---
ms.date: 06/05/2017
title: Объект ISEAddOnTool
description: Объект ISEAddonTool — это устанавливаемая надстройка, расширяющая функциональные возможности интегрированной среды сценариев Windows PowerShell.
ms.openlocfilehash: cc2d50881b7d0033e08de9af5d4cc9e1a9aa55db
ms.sourcegitcommit: 488a940c7c828820b36a6ba56c119f64614afc29
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/27/2020
ms.locfileid: "92667136"
---
# <a name="the-iseaddontool-object"></a>Объект ISEAddOnTool

Объект **ISEAddonTool**  — это устанавливаемая надстройка, расширяющая функциональные возможности интегрированной среды сценариев Windows PowerShell. В качестве примера можно привести средство **Commands** , которое отображается, если выбрать **Вид** , а затем **Show Command Add-on** (Показать настройку Command). После этого средство становится доступным за счет манипуляций с различными доступными объектами **ISEAddOnTool**.

Каждую надстройку можно связать с вертикальной или горизонтальной панелью. Вертикальная область прикрепляется к правому краю интегрированной среды сценариев Windows PowerShell. Горизонтальная панель прикрепляется к нижнему краю.

Каждая вкладка PowerShell в интегрированной среде сценариев Windows PowerShell может содержать собственный набор установленных надстроек. Доступ к коллекции средств, доступных для выбранной вкладки, или к свойствам одного из объектов **PowerShellTab** в объекте коллекции [$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md) рассматривается в статьях [$psISE.CurrentPowerShellTab.HorizontalAddOnTools](The-PowerShellTab-Object.md) и [$psISE.CurrentPowerShellTab.VerticalAddOnTools](The-PowerShellTab-Object.md).

## <a name="methods"></a>Методы

Для объектов этого класса нет доступных методов интегрированной среды сценариев Windows PowerShell.

## <a name="properties"></a>Свойства

### <a name="control"></a>Control

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Свойство **Control** обеспечивает доступ для чтения ко множеству сведений надстройки Command.

```powershell
# View the properties of the Commands add-on tool.
# (assumes that it is visible in the vertical pane)
$psISE.CurrentVisibleVerticalTool.Control
```

```Output
HostObject                  : Microsoft.PowerShell.Host.ISE.ObjectModelRoot
Content                     :
HasContent                  :
ContentTemplate             :
ContentTemplateSelector     :
ContentStringFormat         :
BorderBrush                 :
BorderThickness             :
Background                  :
Foreground                  :
FontFamily                  :
FontSize                    :
FontStretch                 :
FontStyle                   :
FontWeight                  :
HorizontalContentAlignment  :
VerticalContentAlignment    :
TabIndex                    :
IsTabStop                   :
Padding                     :
Template                    : System.Windows.Controls.ControlTemplate
Style                       :
OverridesDefaultStyle       :
UseLayoutRounding           :
Triggers                    : {}
TemplatedParent             :
Resources                   : {System.Windows.Controls.TabItem}
DataContext                 :
BindingGroup                :
Language                    :
Name                        :
Tag                         :
InputScope                  :
ActualWidth                 : 370.75
ActualHeight                : 676.559097412109
LayoutTransform             :
Width                       :
MinWidth                    :
MaxWidth                    :
Height                      :
MinHeight                   :
MaxHeight                   :
FlowDirection               : LeftToRight
Margin                      :
HorizontalAlignment         :
VerticalAlignment           :
FocusVisualStyle            :
Cursor                      :
ForceCursor                 :
IsInitialized               : True
IsLoaded                    :
ToolTip                     :
ContextMenu                 :
Parent                      :
HasAnimatedProperties       :
InputBindings               :
CommandBindings             :
AllowDrop                   :
DesiredSize                 : 227.66,676.559097412109
IsMeasureValid              : True
IsArrangeValid              : True
RenderSize                  : 370.75,676.559097412109
RenderTransform             :
RenderTransformOrigin       :
IsMouseDirectlyOver         : False
IsMouseOver                 : False
IsStylusOver                : False
IsKeyboardFocusWithin       : False
IsMouseCaptured             :
IsMouseCaptureWithin        : False
IsStylusDirectlyOver        : False
IsStylusCaptured            :
IsStylusCaptureWithin       : False
IsKeyboardFocused           : False
IsInputMethodEnabled        :
Opacity                     :
OpacityMask                 :
BitmapEffect                :
Effect                      :
BitmapEffectInput           :
CacheMode                   :
Uid                         :
Visibility                  : Visible
ClipToBounds                : False
Clip                        :
SnapsToDevicePixels         : False
IsFocused                   :
IsEnabled                   :
IsHitTestVisible            :
IsVisible                   : True
Focusable                   :
PersistId                   : 1
IsManipulationEnabled       :
AreAnyTouchesOver           : False
AreAnyTouchesDirectlyOver   :
AreAnyTouchesCapturedWithin : False
AreAnyTouchesCaptured       :
TouchesCaptured             : {}
TouchesCapturedWithin       : {}
TouchesOver                 : {}
TouchesDirectlyOver         : {}
DependencyObjectType        : System.Windows.DependencyObjectType
IsSealed                    : False
Dispatcher                  : System.Windows.Threading.Dispatcher
```

### <a name="isvisible"></a>IsVisible

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Логическое свойство, которое определяет видимость надстройки в соответствующей области. Если она видна, свойству **IsVisible** можно присвоить значение `$false`, чтобы скрыть средство, или **IsVisible** `$true`, чтобы средство отображалось на вкладке PowerShell. Обратите внимание, что к скрытой надстройке нельзя получить доступ с помощью объекта **CurrentVisibleHorizontalTool** или **CurrentVisibleVerticalTool** , а значит, ее нельзя сделать видимой, используя данное свойство объекта.

```powershell
# Hide the current tool in the vertical tool pane
$psISE.CurrentVisibleVerticalTool.IsVisible = $false
# Show the first tool on the currently selected PowerShell tab
$psISE.CurrentPowerShellTab.VerticalAddOnTools[0].IsVisible = $true
```

### <a name="name"></a>Имя

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Свойство только для чтения, которое получает имя надстройки.

```powershell
# Gets the name of the visible vertical pane add-on tool.
$psISE.CurrentVisibleVerticalTool.Name
```

```Output
Commands
```

## <a name="see-also"></a>См. также:

- [Объект ISEAddOnToolCollection](The-ISEAddOnToolCollection-Object.md)
- [Назначение объектной модели скриптов интегрированной среды скриптов Windows PowerShell](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Иерархия объектной модели интегрированной среды скриптов](The-ISE-Object-Model-Hierarchy.md)
