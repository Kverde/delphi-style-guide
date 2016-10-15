# Рекомендации по оформлению исходного кода DELPHI

Этот файл содержит набор рекомендаций предназначенных для облегчения понимания и упрощения поддержки кода написанного на Delphi. Помимо правил по форматированию исходного кода, в тексте содержатся советы которые могут помочь избежать ошибок.

Любое из этих правил может быть нарушено, но на это должна быть веская причина.

Подразумевается что разработка ведется с использованием системы контроля версий.

## Оглавление

## Правила именования

  * Названия типов должны начинаться с `T` (Type)
    * Исключения: 
      * Типы-указатели должны начинаться с `P` (Pointer)
  * Приватные поля классов должны начинаться с `F` (Field)
  * Аргументы функций должны начинаться с `A` (Argument)
    * Исключения: 
      * Value - аргумент для сеттеров,
      * Message - Аргумент для функций обработки сообщений.
  
## Форматирование исходного кода

### использование пробелов и переносов строк

#### Пробелы, запрещённые к использованию

  * До или после оператора . (точка);
  * Между именем метода и открывающей скобкой;
  * Между унарным оператором и его операндом;
  * Между выражением приведения (cast) и приводимым выражением;
  * После открывающей скобки или перед закрывающей;
  * После открывающей квадратной скобки [ или перед закрывающей ];
  * Перед точкой с запятой;

```pascal    
// Правильно
  function TMyClass.MyFunc(var Value: Integer);
  MyPointer := @MyRecord;
  MyClass := TMyClass(MyPointer);
  MyInteger := MyIntegerArray[5];

// Неправильно
  function TMyClass.MyFunc( var Value: Integer ) ;
  MyPointer := @ MyRecord;
  MyClass := TMyClass ( MyPointer ) ;
  MyInteger := MyIntegerArray [ 5 ] ;
```

Двоеточие для всех объявлений переменных не должно содержать перед собой пробелов и иметь один пробел после перед именем типа. 


```pascal
// Правильно
var
  i: Integer;

  procedure Foo(Param1: Integer; Param2: Integer);

// Неправильно
var
  i :Integer;
  
  procedure Foo( Param :Integer; Param2:Integer );
```

#### Пробел должен стоять
  * После запятой;
  * Перед и после оператора присваивания, и операторами сравнения;

```pascal
  // Правильно
  MyProc(1, 'SecondParam', 3);  
  i := 1;

  // Неправильно
  MyProc(1,'SecondParam',3);  
  i:=1;
```

#### Выравнивание строк  

В некоторых случаях можно использовать несколько пробелов для выравнивания строк. Обычно это относится к оператору присваивания и объявлению переменных.

```pascal
  // Правильно
var
  Counter  : Integer;
  MyString : string;

  
  OraSession.Password := 'MyPassvord';
  OraSession.Server   := 'MyServer';
  OraSession.Username := 'MyLogin';
```

Объединять строки в такие столбцы нужно только если строки в левой части имеют разницу в длине не больше пяти символов.

```pascal
  // Неправильно
  
  MyBigIdentifier := 125;
  i               := 2;
```

#### Использование отступов

Всегда необходимо использовать два пробела для всех уровней отступа. Другими словами, первый уровень отступает на два пробела, второй на четыре и так далее. Никогда не используйте символы табуляции.

```pascal
// Правильно
program MyProgram;
uses
  MyUnit;
begin
  if IsValid then
  begin
    DoSomething1;
	DoSomething2;
  end;
  
  DoSomething3;
end.

// Неправильно
program MyProgram;
uses
  MyUnit;
begin
if IsValid then
begin
DoSomething1;
DoSomething2;
end;  
DoSomething3;
end.
```

Зарезервированные слова **unit**, **uses**, **type**, **interface**, **implementation**, **initialization** и **finalization** всегда должны примыкать к левой границе. Также должны быть отформатирован end завершающий модуль. В файле проекта (dpr) выравнивание по левой границе применяется к словам **program**, главным **begin** и **end**. Код внутри блока **begin**..**end** должен иметь отступ два символа.

```pascal
// Правильно

type
  MyInt = Integer;

var
  i, j: MyInt;
  
// Неправильно
type MyInt = Integer;

var
i, j: MyInt;
```

#### Переносы строк

Строки длиннее 80 символов должны быть разделены и перенесены. Все перенесенные строки должны быть выровнены по первой строке и иметь отступ в два символа. 


Сервис - Параметры - Отображение - Правая видимая граница

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

****
```pascal
  // Правильно
  Count := 4;
  MyProc(Count);

  // Неправильно
  Count := 4; MyProc(Count);
```

Строки с ключевыми словами **begin**, **else**, **end**, **var**, **const**, **type** не должны содержать другого кода. 

```pascal
  // Неправильно
  for i := 0 to 10 do begin
    DoSomething1; 
    DoSomething2;
  end;
  
  procedure MyProc;
  var a, b: Integer;
  begin

  // Правильно
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

### Форматирование операторов

Операторы - это одна или более строк кода, разделенных точкой с запятой. Простые операторы имеют одну точку с запятой, а составные могут иметь более чем одну точку с запятой и, таким образом, состоят из множества простых операторов.

```pascal
  // Это простой оператор:
  A := B; 

  // Это составной или структурированный оператор:
  begin
    B := C;
    A := B;
  end;
```
Оператор if (while, for) всегда должен располагаться, по крайней мере, на двух строках.

```pascal
  // Правильно
  if A < B then DoSomething;

  // Неправильно
  if A < B then 
    DoSomething;  
```

Если внутри оператора **if** (**while**, **for**) используется составной оператор, то для него не нужно делать отступ.

```pascal
  // Неправильно
  if A < B then 
    begin
      DoSomething1;  
	  DoSomething2; 
    end;
	  	
  if A < B then 
  begin
    DoSomething1;  
	DoSomething2; 
  end 
  else begin
    DoSomething3;  
	DoSomething4; 
  end;  
	
  // Правильно
  if A < B then 
  begin
    DoSomething1;  
	DoSomething2; 
  end;
	  	
  if A < B then 
  begin
    DoSomething1;  
	DoSomething2; 
  end 
  else 
  begin
    DoSomething3;  
	DoSomething4; 
  end;
```

Операторы **repeat** и **try** оформляются также.

```pascal
  repeat
    x := j;
    j := UpdateValue;
  until j > 25;

  try
    try
      EnumThreadWindows(CurrentThreadID, @Disable, 0);
      Result := TaskWindowList;
    except 
      EnableTaskWindows(TaskWindowList);
      raise;
    end; 
  finally
    TaskWindowList := SaveWindowList; 
    TaskActiveWindow := SaveActiveWindow;
  end;
```

#### Оператор case

Рекомендуемое оформление оператора **case**:

```pascal
 case ScrollCode of
    SB_LINEUP, SB_LINEDOWN:
      begin
        Incr := FIncrement div FLineDiv;
        FinalIncr := FIncrement mod FLineDiv;
        Count := FLineDiv;
      end;
    SB_PAGEUP, SB_PAGEDOWN:
      begin
        Incr := FPageIncrement;
        FinalIncr := Incr mod FPageDiv;
        Incr := Incr div FPageDiv;
        Count := FPageDiv;
      end;
  else
    Count := 0;
    Incr := 0;
    FinalIncr := 0;
  end;
```

## Комментарии

Комментарии в теле процедур и методов не должны описывать, что делает тот или иной оператор или блок, а должны указывать цель, для которой он (оператор) используется.


### Старый код

В коде не должно оставаться комментариев со старым кодом. Для хранения старого кода используется система контроля версий. 

Если необходимо что-то пояснить, то нужно писать информативный комментарий. Любые временные пометки должны быть исключены из фиксации.

## Использование операторов и других средств языка

### Объявление процедур и функций

Комбинируйте формальные параметры одного типа в одно выражение.

```pascal
  // Правильно
  procedure MyProc(AFirstInt, ASecondInt: Integer);

  // Неправильно
  procedure MyProc(AFirstInt: Integer; ASecondInt: Integer);
```

Придерживайтесь следующего порядка в параметрах: сначала входные параметры, затем входные/выходные, затем выходные.

```pascal
  // Правильно
  procedure MyProc(const AStr: string; var ACounter: Integer; out AOutStr: string);

  // Неправильно
  procedure MyProc(out AOutStr: string; var ACounter: Integer; const AStr: string);
```

Всегда используйте const для параметров, которые не изменяются при работе вызываемых методов, процедур и функций.

```pascal
  // Правильно
  procedure SetName2(const AParam2: TComponent; const AName: string);
  begin
    AParam2.Name := AName + AName;
  end;

  // Неправильно
  procedure MyProc(AParam2: TComponent; AName: string);
  begin
    AParam2.Name := AName + AName;
  end;  
```

Процедуры должны иметь только по одной секции type, const и var в следующем порядке:

```pascal
procedure SomeProcedure;
type
  TMyType = Integer;
const
  ArraySize = 100;
var
  MyArray: array [1..ArraySize] of TMyType;
begin
  ...
end;
```

### Вложенность

### Блок try..finally и контроль ресурсов

Для удаления объектов всегда следует использовать FreeAndNil.

```pascal
  // Неправильно
  Obj.Free;
  Obj.Destroy;
  
  // Правильно
  FreeAndNil(Obj);  
```

Блок try..finally применяется для освобождения ресурсов, в том числе для освобождения памяти при создании объектов. Захват ресурса производится непосредственно перед try, а освобождение — в finally.

```pascal
  // Неправильно
  try
    Obj := TMyObj.Create;
	Obj.Run;
  finally 
    FreeAndNil(Obj);
  end;
    
  // Правильно 
  Obj := TMyObj.Create;
  try
    Obj.Run;
  finally 
    FreeAndNil(Obj);
  end;
```

При создании нескольких объектов, для уменьшения вложенности блоков следует инициализировать переменные, а затем создавать все объекты внутри одного блока **try**..**finally**;

```pascal
  // Неправильно
  Obj1 := TMyObj.Create;
  try    
    Obj2 := TMyObj.Create;
	try
      Obj2.Run(Obj1);
	finally
	  FreeAndNil(Obj2);
	end;
  finally
    FreeAndNil(Obj1);
  end;
  
  // Правильно
  Obj1 := TMyObj.Create;
  Obj2 := TMyObj.Create;
  try
    Obj2.Run(Obj1);
  finally
    FreeAndNil(Obj2);
    FreeAndNil(Obj1);
  end;
```

Если ресурс не реализован в виде класса и используется неоднократно — надо создать класс, в конструкторе которого осуществляется захват ресурса, а в деструкторе — освобождение. Это сделает использование ресурса более простым и единообразным, а отлов его утечек сведется к отлову утечек памяти.

### Условия

В условиях, внутри операторов **if**, **where** и др., не должно быть лишних скобок, если они не упрощают понимание условия.

```pascal
  //неправильно
  if (I > 0) then
    DoSomething;
 
  // правильно  
  if I > 0 then 
    DoSomething;
```

Результатом выполнения условия является тип Boolean, можно сразу присваивать его логической переменной.

```pascal
var
  Flag: Boolean;
  
  //неправильно
  if I > 0 then
    Flag := True
  else
    Flag := False;  
 
  // правильно  
  Flag := I > 0;
```

При разделении длинных условий на несколько строк
  * Логические операторы должны находится перед строкой с условием
  * **then** (**do**) должен быть на отдельной строке  

```pascal
  // Неправильно
  if (LongExpression1) or 
    (LongExpression2) or 
    (LongExpression3) then 
  begin
  end;  

  // Правильно	
  if (LongExpression1) 
    or (LongExpression2) 
    or (LongExpression3) 
  then 
  begin
  end;
```

## Средства для автоматического форматирования

### JEDI Code Format
 [JEDI Code Format](http://jedicodeformat.sourceforge.net/) - отдельное приложение для форматирования исходных кодов Object Pascal и Delphi.
  

### Experimental GExperts Version 
[Это экспериментальная версия](http://www.dummzeuch.de/delphi/gexperts/english.html) эксперта для IDE RAD Studio [GExpert](http://www.gexperts.org/).  

Поддерживаемые версии IDE: 6, 7, 2005, 2006, 2007, 2009, 2010, XE1, XE2.

### Стандартное форматирование кода в Delphi 2010

Начиная с Delphi 2010 в IDE добавлено стандартное средство для автоматического форматирования исходного кода. Иллюстрированные справочник с описанием.

  * [Описание в Embarcadero wiki](http://docwiki.embarcadero.com/RADStudio/XE5/en/Source_Code_Formatter)
  * [Иллюстрированный справочник](http://www.webdelphi.ru/2010/10/formatter-delphi-xe-2/)

## Основано на следующих статьях

  * [Стиль оформления кода (gunsmoker.ru)](http://www.gunsmoker.ru/2010/07/blog-post.html)
  * [Стандарт стилевого оформления исходного кода DELPHI (DelphiKingdom.com)](http://www.delphikingdom.com/asp/viewitem.asp?catalogid=802)
  * [Project JEDI Delphi Language Style Guide](http://wiki.delphi-jedi.org/index.php?title=Style_Guide)
  * [Delphi 4 Developer's Guide Coding Standards Document](http://www.econos.de/delphi/cs.html)
  * [Guidelines for Writing Delphi Programs](http://mc-computing.com/languages/Delphi/Style_Guides.html)
  * [Заповеди молодого разработчика Delphi](http://habrahabr.ru/post/104377/)

## Полезная литература
  
  