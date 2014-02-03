# Рекомендации по оформлению исходного кода DELPHI

Этот файл содержит набор рекомендаций предназначенных для облегчения понимания и упрощения поддержки кода написанного Delphi. Помимо правил по форматированию исходного кода в тексте также содержатся советы которые могут помочь избежать ошибок.

Любое из этих правил может быть нарушено, но на это должна быть веская причина.


### Идентификаторы

### Комментарии

Комментарии в теле процедур и методов не должны описывать, что делает тот или иной оператор или блок, а должны указывать цель, для которой он (оператор) используется.

### использование пробелов

#### Пробелы, запрещенные к использованию

  * До или после оператора . (точка);
  * Между именем метода и открывающей скобкой;
  * Между унарным оператором и его операндом;
  * Между выражением приведения (cast) и приводимым выражением;
  * После открывающей скобки или перед закрывающей;
  * После открывающей квадратной скобки [ или перед закрывающей ];
  * Перед точкой с запятой;

**Примеры правильного использования:**

```pascal    
function TMyClass.MyFunc(var Value: Integer);
MyPointer := @MyRecord;
MyClass := TMyClass(MyPointer);
MyInteger := MyIntegerArray[5];
```

**Примеры неправильного использования:**

```pascal
function TMyClass.MyFunc( var Value: Integer ) ;
MyPointer := @ MyRecord;
MyClass := TMyClass ( MyPointer ) ;
MyInteger := MyIntegerArray [ 5 ] ;
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
