# Форматирование кода

## Пробелы, запрещённые к использованию

  * До или после оператора . (точка);
  * Между именем метода и открывающей скобкой;
  * Между унарным оператором и его операндом;
  * Между выражением приведения (cast) и приводимым выражением;
  * После открывающей скобки и перед закрывающей (для любых скобок);
  * Перед точкой с запятой;
  * Перед запятой;
  * Перед двоеточием;

## Пробел должен стоять  
  * После запятой;
  * Перед и после бинарных операторов;
  
```pascal    
// Примеры

// Неправильно - лишние пробелы
  function TMyClass.MyFunc( var Value: Integer ) ;  
// Правильно  
  function TMyClass.MyFunc(var Value: Integer);
  
// Неправильно - пробел после унарного оператора
  MyPointer := @ MyRecord;
// Правильно
  MyPointer := @MyRecord;

// Неправильно 
//   Нет пробелов до и после оператора присваивания
//   Лишние пробелы 
  MyInteger:=MyIntegerArray [ 5 ] ;
// Правильно
  MyInteger := MyIntegerArray[5];
  
// Неправильно - пробел перед ":", нет пробела после
  i :Integer;
// Правильно 
  i: Integer;

// Неправильно 
//   Нет пробелов после запятой
//   Нет пробелов до и после оператора +
  MyProc(1,'SecondParam',Value+Summa);  
// Правильно 
  MyProc(1, 'SecondParam', Value + Summa);  
```

## Выравнивание строк  

В некоторых случаях нужно использовать несколько лишних пробелов для выравнивания строк. Обычно это относится к оператору присваивания и объявлению переменных.

```pascal
// Неправильно
var
  Counter: Integer;
  MyString: string;

  OraSession.Password:= 'MyPassvord';
  OraSession.Server:= 'MyServer';
  OraSession.Username:= 'MyLogin';

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
  
  VeryBigIdentifier := 125;
  i                 := 2;
  
// Правильно
  i := 2; 
  VeryBigIdentifier := 125;

// Правильно  
  VeryBigIdentifier := 125;  
  
  i := 2; 
```

## Использование отступов

Для каждого уровня вложенности нужно использовать два пробела. Другими словами, первый уровень отступает на два пробела, второй на четыре и так далее. Никогда не используйте символы табуляции.

```pascal
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