## Рекомендации по оформлению исходного кода DELPHI

Этот файл содержит набор рекомендаций предназначенных для облегчения понимания и упрощения поддержки кода написанного на Delphi. Помимо правил по форматированию исходного кода, в тексте содержатся советы которые могут помочь избежать ошибок.

Любое из этих правил может быть нарушено, но на это должна быть веская причина.

Подразумевается что разработка ведется с использованием системы контроля версий.

### использование пробелов и переносов строк

#### Пробелы, запрещенные к использованию

  * До или после оператора . (точка);
  * Между именем метода и открывающей скобкой;
  * Между унарным оператором и его операндом;
  * Между выражением приведения (cast) и приводимым выражением;
  * После открывающей скобки или перед закрывающей;
  * После открывающей квадратной скобки [ или перед закрывающей ];
  * Перед точкой с запятой;

**Правильно**

```pascal    
function TMyClass.MyFunc(var Value: Integer);
MyPointer := @MyRecord;
MyClass := TMyClass(MyPointer);
MyInteger := MyIntegerArray[5];
```

**Неправильно**

```pascal
function TMyClass.MyFunc( var Value: Integer ) ;
MyPointer := @ MyRecord;
MyClass := TMyClass ( MyPointer ) ;
MyInteger := MyIntegerArray [ 5 ] ;
```

Двоеточие для всех объявлений переменных не должно содержать перед собой пробелов и иметь один пробел после перед именем типа. 

**Правильно**
```pascal
var
  i: Integer;
...
procedure Foo(Param1: Integer; Param2: Integer);
```

**Неправильно**
```pascal
var
  i :Integer;
...  
procedure Foo( Param :Integer; Param2:Integer );
```

#### Пробел должен стоять
  * После запятой;
  * Перед и после оператора присваивания, и операторами сравнения;

**Правильно**
```pascal
  MyProc(1, 'SecondParam', 3);
  
  i := 1;
```

**Неправильно**
```pascal
  MyProc(1,'SecondParam',3);
  
  i:=1;
```

#### Выравнивание строк  

В некоторых случаях можно использовать несколько пробелов для выравнивания строк. Обычно это относится к оператору присваивания и объявлению переменных.

**Правильно**
```pascal
var
  Counter  : Integer;
  MyString : string;
...
  OraSession.Password := 'MyPassvord';
  OraSession.Server   := 'MyServer';
  OraSession.Username := 'MyLogin';
```

Объединять строки в такие столбцы нужно только если строки в левой части имеют разницу в длине не больше пяти символов.

**Неправильно**
```pascal
  MyBigIdentifier := 125;
  i               := 2;
```

#### Использование отступов

Всегда необходимо использовать два пробела для всех уровней отступа. Другими словами, первый уровень отступает на два пробела, второй на четыре и так далее. Никогда не используйте символы табуляции.

**Примеры правильного использования**
```pascal
program MyProgram;
begin
  if IsValid then
  begin
    DoSomething1;
	DoSomething2;
  end;
  
  DoSomething3;
end.
```

**Примеры неправильного использования**
```pascal
program MyProgram;
begin
if IsValid then
begin
DoSomething1;
DoSomething2;
end;  
DoSomething3;
end.
```

Зарезервированные слова unit, uses, type, interface, implementation, initialization и finalization всегда должны примыкать к левой границе. Также должны быть отформатирован end завершающий модуль. В файле проекта (dpr) выравнивание по левой границе применяется к словам program, главным begin и end. Код внутри блока begin..end должен иметь отступ два символа.

#### Переносы строк

Строки длиннее 80 символов должны быть разделены и перенесены. Все перенесенные строки должны быть выровнены по первой строке и иметь отступ в два символа. 

**Правильно**
```pascal
function CreateWindowEx(dwExStyle: DWORD;
  lpClassName: PChar; lpWindowName: PChar;
  dwStyle: DWORD; X, Y, nWidth, nHeight: Integer;
  hWndParent: HWND; hMenu: HMENU; hInstance: HINST;
  lpParam: Pointer): HWND; stdcall;
```

Нельзя переносить строки в тех местах, где не допускаются пробелы, например между именем метода и открывающей скобкой или между именем массива и открывающей квадратной скобкой.

На одной строке должно находится не более одного оператора или команды.

**Правильно**
```pascal
  Count := 4;
  MyProc(Count);
```

**Неправильно**
```pascal
  Count := 4; MyProc(Count);
```

Оператор if (while, for) всегда должен располагаться, по крайней мере, на двух строках.

**Правильно**
```pascal
  if A < B then DoSomething;
```

**Неправильно**
```pascal
  if A < B then 
    DoSomething;  
```

Строки с ключевыми словами begin, else, end, var, const, type не должны содержать другого кода. 

**Неправильно**
```pascal
  for i := 0 to 10 do begin
    DoSomething1; 
    DoSomething2;
  end;
  
  procedure MyProc;
  var a, b: Integer;
  begin
```

**Неправильно**
```pascal
  for i := 0 to 10 do 
  begin
    DoSomething1;
    DoSomething2;
  end;

  // правильно
  procedure MyProc;
  var
    a, b: Integer;
  begin
```

### Идентификаторы

### Комментарии

Комментарии в теле процедур и методов не должны описывать, что делает тот или иной оператор или блок, а должны указывать цель, для которой он (оператор) используется.


#### Старый код

В коде не должно оставаться комментариев со старым кодом. Для хранения старого кода используется система контроля версий. 

Если необходимо что-то пояснить, то нужно писать информативный комментарий. Любые временные пометки должны быть исключены из фиксации.

### Средства для автоматического форматирования

#### JEDI Code Format
 [JEDI Code Format](http://jedicodeformat.sourceforge.net/) - отдельное приложение для форматирования исходных кодов Object Pascal и Delphi.
  

#### Experimental GExperts Version 
[Это экспериментальная версия](http://www.dummzeuch.de/delphi/gexperts/english.html) эксперта для IDE RAD Studio [GExpert](http://www.gexperts.org/).  

Поддерживаемые версии IDE: 6, 7, 2005, 2006, 2007, 2009, 2010, XE1, XE2.

#### Стандартное форматирование кода в Delphi 2010

Начиная с Delphi 2010 в IDE добавлено стандартное средство для автоматического форматирования исходного кода. Иллюстрированные справочник с описанием.

  * [Описание в Embarcadero wiki](http://docwiki.embarcadero.com/RADStudio/XE5/en/Source_Code_Formatter)
  * [Иллюстрированный справочник](http://www.webdelphi.ru/2010/10/formatter-delphi-xe-2/)

### Основано на следующих статьях

  * [Стиль оформления кода (gunsmoker.ru)](http://www.gunsmoker.ru/2010/07/blog-post.html)
  * [Стандарт стилевого оформления исходного кода DELPHI (DelphiKingdom.com)](http://www.delphikingdom.com/asp/viewitem.asp?catalogid=802)
  * [Project JEDI Delphi Language Style Guide](http://wiki.delphi-jedi.org/index.php?title=Style_Guide)
  * [Delphi 4 Developer's Guide Coding Standards Document](http://www.econos.de/delphi/cs.html)
  * [Guidelines for Writing Delphi Programs](http://mc-computing.com/languages/Delphi/Style_Guides.html)
  * [Заповеди молодого разработчика Delphi](http://habrahabr.ru/post/104377/)

### Полезная литература
  
  