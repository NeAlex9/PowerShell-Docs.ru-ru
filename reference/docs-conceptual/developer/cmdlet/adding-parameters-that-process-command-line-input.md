---
ms.date: 09/13/2016
ms.topic: reference
title: Добавление параметров для обработки входных данных команды
description: Добавление параметров для обработки входных данных команды
ms.openlocfilehash: f20469d366330aa787fbc16e4f0a76e67fc7c6db
ms.sourcegitcommit: ba7315a496986451cfc1296b659d73ea2373d3f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "93354615"
---
# <a name="adding-parameters-that-process-command-line-input"></a>Добавление параметров для обработки входных данных команды

Одним из источников входных данных для командлета является Командная строка. В этом разделе описывается, как добавить параметр в `Get-Proc` командлет (описанный при [создании первого командлета](./creating-a-cmdlet-without-parameters.md)), чтобы командлет мог обрабатывать входные данные с локального компьютера на основе явных объектов, переданных в командлет. `Get-Proc`Описанный здесь командлет извлекает процессы на основе их имен, а затем отображает сведения о процессах в командной строке.

## <a name="defining-the-cmdlet-class"></a>Определение класса командлета

Первым шагом при создании командлета является именование командлетов и объявление класса .NET Framework, который реализует командлет. Этот командлет извлекает сведения о процессе, поэтому выбранное здесь имя команды — "Get". (Практически любой командлет, который способен получить информацию, может обрабатывать входные данные командной строки.) Дополнительные сведения о утвержденных командах командлетов см. в разделе [имена глаголов командлетов](./approved-verbs-for-windows-powershell-commands.md).

Ниже приведено объявление класса для `Get-Proc` командлета. Сведения об этом определении приведены в статье [Создание первого командлета](./creating-a-cmdlet-without-parameters.md).

```csharp
[Cmdlet(VerbsCommon.Get, "proc")]
public class GetProcCommand: Cmdlet
```

```vb
<Cmdlet(VerbsCommon.Get, "Proc")> _
Public Class GetProcCommand
    Inherits Cmdlet
```

## <a name="declaring-parameters"></a>Объявление параметров

Параметр командлета позволяет пользователю предоставлять входные данные для командлета. В следующем примере и — `Get-Proc` это `Get-Member` имена командлетов конвейера, а `MemberType` — это параметр для `Get-Member` командлета. Параметр имеет аргумент "свойство".

**PS> Get-proc; `get-member` -MemberType, свойство**

Чтобы объявить параметры для командлета, необходимо сначала определить свойства, представляющие параметры. В `Get-Proc` командлете единственным параметром является `Name` , который в данном случае представляет имя объекта .NET Framework процесса для извлечения. Поэтому класс командлета определяет свойство типа String, которое принимает массив имен.

Ниже приведено объявление параметра для `Name` параметра `Get-Proc` командлета.

```csharp
/// <summary>
/// Specify the cmdlet Name parameter.
/// </summary>
  [Parameter(Position = 0)]
  [ValidateNotNullOrEmpty]
  public string[] Name
  {
    get { return processNames; }
    set { processNames = value; }
  }
  private string[] processNames;

  #endregion Parameters
```

```vb
<Parameter(Position:=0), ValidateNotNullOrEmpty()> _
Public Property Name() As String()
    Get
        Return processNames
    End Get

    Set(ByVal value As String())
        processNames = value
    End Set

End Property
```

Чтобы сообщить среде выполнения Windows PowerShell, что это свойство является `Name` параметром, в определение свойства добавляется атрибут [System. Management. Automation. параметераттрибуте](/dotnet/api/System.Management.Automation.ParameterAttribute) . Базовый синтаксис для объявления этого атрибута — `[Parameter()]` .

> [!NOTE]
> Параметр должен быть явно помечен как public. Параметры, которые не помечены как открытые по умолчанию, являются внутренними и не обнаруживаются средой выполнения Windows PowerShell.

Этот командлет использует массив строк для `Name` параметра. Если это возможно, командлет также должен определить параметр как массив, так как это позволяет командлету принимать более одного элемента.

#### <a name="things-to-remember-about-parameter-definitions"></a>Вопросы, которые следует помнить об определениях параметров

- Предопределенные имена параметров Windows PowerShell и типы данных следует использовать повторно, чтобы обеспечить совместимость командлета с командлетами Windows PowerShell. Например, если все командлеты используют предопределенное `Id` имя параметра для определения ресурса, пользователь сможет легко понять значение параметра, независимо от того, какой командлет используется. В сущности, имена параметров соответствуют тем же правилам, которые используются для имен переменных в общеязыковой среде выполнения (CLR). Дополнительные сведения об именовании параметров см. в разделе [имена параметров командлета](/previous-versions/ms714468(v=vs.85)).

- Windows PowerShell резервирует несколько имен параметров для обеспечения единообразного взаимодействия с пользователем. Не используйте следующие имена параметров: `WhatIf` , `Confirm` , `Verbose` , `Debug` , `Warn` , `ErrorAction` , `ErrorVariable` , `OutVariable` и `OutBuffer` . Кроме того, следующие псевдонимы для этих имен параметров зарезервированы: `vb` , `db` , `ea` ,, `ev` `ov` и `ob` .

- `Name` — Это простое и общее имя параметра, рекомендуемое для использования в командлетах. Лучше выбрать имя параметра, которое отличается от сложного имени, уникального для конкретного командлета, и трудно запомнить.

- В Windows PowerShell параметры не учитывают регистр, хотя по умолчанию оболочка сохраняет регистр. Чувствительность к регистру аргументов зависит от операции командлета. Аргументы передаются в параметр, как указано в командной строке.

- Примеры других объявлений параметров см. в разделе [параметры командлета](./cmdlet-parameters.md).

## <a name="declaring-parameters-as-positional-or-named"></a>Объявление параметров как позиционированного или именованного

Командлет должен задавать каждый параметр как либо Позиционированный, либо именованный параметр. Оба типа параметров принимают одиночные аргументы, несколько аргументов, разделенных запятыми, и логические параметры. Логический параметр, также называемый *параметром, обрабатывает* только логические параметры. Параметр используется для определения наличия параметра. Рекомендуемое значение по умолчанию — `false` .

Образец `Get-Proc` командлета определяет `Name` параметр как параметр с положением
0. Это означает, что первый аргумент, вводимый пользователем в командной строке, автоматически вставляется для этого параметра. Если необходимо определить именованный параметр, для которого пользователь должен указать имя параметра из командной строки, оставьте `Position` ключевое слово за пределами объявления атрибута.

> [!NOTE]
> Если параметры не должны быть именованы, рекомендуется использовать наиболее часто используемые параметры, чтобы пользователи не могли вводить имя параметра.

## <a name="declaring-parameters-as-mandatory-or-optional"></a>Объявление параметров как обязательных или необязательных

Командлет должен задавать каждый параметр как необязательный или обязательный параметр. В примере `Get-Proc` командлета `Name` параметр определен как необязательный, так как в `Mandatory` объявлении атрибута не задано ключевое слово.

## <a name="supporting-parameter-validation"></a>Поддержка проверки параметров

Командлет Sample `Get-Proc` добавляет атрибут проверки входных данных [System. Management. Automation. валидатенотнуллоремптяттрибуте](/dotnet/api/System.Management.Automation.ValidateNotNullOrEmptyAttribute)к `Name` параметру, чтобы обеспечить проверку того, что входные данные не являются ни `null` пустыми, ни пустыми. Этот атрибут является одним из нескольких атрибутов проверки, предоставляемых Windows PowerShell. Примеры других атрибутов проверки см. в разделе [Проверка входных параметров](./validating-parameter-input.md).

```
[Parameter(Position = 0)]
[ValidateNotNullOrEmpty]
public string[] Name
```

## <a name="overriding-an-input-processing-method"></a>Переопределение метода обработки входных данных

Если командлет обрабатывает входные данные командной строки, он должен переопределять соответствующие методы обработки входных данных. Основные методы обработки ввода представлены при [создании первого командлета](./creating-a-cmdlet-without-parameters.md).

`Get-Proc`Командлет переопределяет метод [System. Management. Automation. командлет. ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) для управления `Name` входными параметрами, предоставленными пользователем или сценарием. Этот метод получает процессы для каждого запрошенного имени процесса или все для процессов, если имя не указано. Обратите внимание, что в [System. Management. Automation. командлет. ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord)вызов [System. Management. Automation. командлет. WriteObject% 28System. Object% 2CSystem. Boolean %29](/dotnet/api/system.management.automation.cmdlet.writeobject#System_Management_Automation_Cmdlet_WriteObject_System_Object_System_Boolean_) является механизмом вывода для отправки выходных объектов в конвейер. Вторым параметром этого вызова `enumerateCollection` является значение, чтобы `true` информировать среду выполнения Windows PowerShell о перечислении выходного массива объектов процессов и записи одного процесса в командную строку.

```csharp
protected override void ProcessRecord()
{
  // If no process names are passed to the cmdlet, get all processes.
  if (processNames == null)
  {
    // Write the processes to the pipeline making them available
    // to the next cmdlet. The second argument of this call tells
    // PowerShell to enumerate the array, and send one process at a
    // time to the pipeline.
    WriteObject(Process.GetProcesses(), true);
  }
  else
  {
    // If process names are passed to the cmdlet, get and write
    // the associated processes.
    foreach (string name in processNames)
    {
      WriteObject(Process.GetProcessesByName(name), true);
    }
  }
}
```

```vb
Protected Overrides Sub ProcessRecord()

    '/ If no process names are passed to the cmdlet, get all processes.
    If processNames Is Nothing Then
        Dim processes As Process()
        processes = Process.GetProcesses()
    End If

    '/ If process names are specified, write the processes to the
    '/ pipeline to display them or make them available to the next cmdlet.

    For Each name As String In processNames
        '/ The second parameter of this call tells PowerShell to enumerate the
        '/ array, and send one process at a time to the pipeline.
        WriteObject(Process.GetProcessesByName(name), True)
    Next

End Sub 'ProcessRecord
```

## <a name="code-sample"></a>Образец кода

Полный пример кода на C# см. в разделе [GetProcessSample02 Sample](./getprocesssample02-sample.md).

## <a name="defining-object-types-and-formatting"></a>Определение типов объектов и форматирование

Windows PowerShell передает сведения между командлетами с помощью .NET Framework объектов. Следовательно, командлету может потребоваться определить собственный тип, или командлету может потребоваться расширить существующий тип, предоставленный другим командлетом. Дополнительные сведения об определении новых типов или расширении существующих типов см. в разделе [расширение типов объектов и форматирование](/previous-versions/ms714665(v=vs.85)).

## <a name="building-the-cmdlet"></a>Создание командлета

После реализации командлета его необходимо зарегистрировать в Windows PowerShell с помощью оснастки Windows PowerShell. Дополнительные сведения о регистрации командлетов см. [в разделе Регистрация командлетов, поставщиков и ведущих приложений](/previous-versions/ms714644(v=vs.85)).

## <a name="testing-the-cmdlet"></a>Тестирование командлета

Если командлет зарегистрирован в Windows PowerShell, его можно проверить, запустив его в командной строке. Ниже приведены два способа проверки кода для примера командлета. Дополнительные сведения об использовании командлетов из командной строки см. в разделе [Начало работы with Windows PowerShell](/powershell/scripting/getting-started/getting-started-with-windows-powershell).

- В командной строке Windows PowerShell используйте следующую команду, чтобы получить список процессов Internet Explorer с именем IEXPLORE.

  ```powershell
  get-proc -name iexplore
  ```

  Появится следующий результат.

  ```Output
  Handles  NPM(K)  PM(K)   WS(K)  VS(M)  CPU(s)   Id   ProcessName
  -------  ------  -----   -----  -----   ------ --   -----------
      354      11  10036   18992    85   0.67   3284   iexplore
  ```

- Чтобы получить список браузеров Internet Explorer, Outlook и Notepad с именами «IEXPLORE», «OUTLOOK» и «NOTEPAD», используйте следующую команду. При наличии нескольких процессов отображаются все они.

  ```powershell
  get-proc -name iexplore, outlook, notepad
  ```

  Появится следующий результат.

  ```
  Handles  NPM(K)  PM(K)   WS(K)  VS(M)  CPU(s)   Id   ProcessName
  -------  ------  -----   -----  -----  ------   --   -----------
      732      21  24696    5000    138   2.25  2288   iexplore
      715      19  20556   14116    136   1.78  3860   iexplore
     3917      62  74096   58112    468 191.56  1848   OUTLOOK
       39       2   1024    3280     30   0.09  1444   notepad
       39       2   1024     356     30   0.08  3396   notepad
  ```

## <a name="see-also"></a>См. также:

[Добавление параметров для обработки входных данных конвейера](./adding-parameters-that-process-pipeline-input.md)

[Создание первого командлета](./creating-a-cmdlet-without-parameters.md)

[Расширение типов объектов и форматирование](/previous-versions/ms714665(v=vs.85))

[Регистрация командлетов, поставщиков и ведущих приложений](/previous-versions/ms714644(v=vs.85))

[Справочник по Windows PowerShell](../windows-powershell-reference.md)

[Примеры командлетов](./cmdlet-samples.md)
