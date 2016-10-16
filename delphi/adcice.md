# Использование конструкций языка

## Блок try..finally и контроль ресурсов

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

Если ресурс не реализован в виде класса и используется неоднократно — надо создать класс, в конструкторе которого осуществляется захват ресурса, а в деструкторе — освобождение. Это сделает использование ресурса более простым и единообразным, а отлов его утечек сведётся к отлову утечек памяти.
