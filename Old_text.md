
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

## Основано на следующих статьях

  * [Стиль оформления кода (gunsmoker.ru)](http://www.gunsmoker.ru/2010/07/blog-post.html)
  * [Стандарт стилевого оформления исходного кода DELPHI (DelphiKingdom.com)](http://www.delphikingdom.com/asp/viewitem.asp?catalogid=802)
  * [Project JEDI Delphi Language Style Guide](http://wiki.delphi-jedi.org/index.php?title=Style_Guide)
  * [Delphi 4 Developer's Guide Coding Standards Document](http://www.econos.de/delphi/cs.html)
  * [Guidelines for Writing Delphi Programs](http://mc-computing.com/languages/Delphi/Style_Guides.html)
  * [Заповеди молодого разработчика Delphi](http://habrahabr.ru/post/104377/)

  
  