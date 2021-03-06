---
ms.date: 09/12/2016
ms.topic: reference
title: Как задать номера версий XML-файла HelpInfo
description: Как задать номера версий XML-файла HelpInfo
ms.openlocfilehash: 9ef1940ca05d8aa9b04770013287490b71c8065a
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "92658830"
---
# <a name="how-to-set-helpinfo-xml-version-numbers"></a>Как задать номера версий XML-файла HelpInfo

В этом разделе объясняется, как задать и увеличить номера версий в файле обновляемой справочной информации, который обычно называется XML-файлом HelpInfo.

## <a name="how-to-set-helpinfo-xml-version-numbers"></a>Как задать номера версий XML-файла HelpInfo

Номера версий в XML-файле HelpInfo критически важны для работы обновляемой справки. Командлеты [Update — Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) и [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) загружают новые файлы справки только в том случае, если номер версии языка и региональных параметров пользовательского интерфейса в удаленном XML-файле HelpInfo больше номера версии для этого языка и региональных параметров пользовательского интерфейса в локальном HelpInfo XML или отсутствует локальный XML-файл HelpInfo.

XML-файл HelpInfo использует номер версии из 4 частей, определенный в классе **System. Version** платформы Microsoft .NET Framework. Формат — `N1.N2.N3.N4`. Авторы модулей могут использовать любую схему нумерации версий, которая разрешена классом **System. Version** . Для обновляемой справки необходимо, чтобы номер версии языка и региональных параметров пользовательского интерфейса был увеличен, когда новая версия CAB-файла для этого языка и региональных параметров пользовательского интерфейса передается в расположение, указанное элементом **хелпконтентури** в файле XML HelpInfo.

В следующем примере показаны элементы XML-файла HelpInfo для языка и региональных параметров (de-DE) пользовательского интерфейса, если версия 2.15.0.10.

```xml
<UICulture>
  <UICultureName>de-DE</UICultureName>
  <UICultureVersion>2.15.0.10</UICultureVersion>
</UICulture>
```

Номер версии языка и региональных параметров пользовательского интерфейса отражает версию CAB-файла для этого языка и региональных параметров пользовательского интерфейса. Номер версии применяется ко всему CAB-файлу. Нельзя задать разные номера версий для разных файлов в CAB-файле. Номер версии для каждого языка и региональных параметров пользовательского интерфейса вычисляется независимо друг от друга и не должен быть связан с номерами версий других культур пользовательского интерфейса, поддерживаемых модулем.
