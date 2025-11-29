# Задача 1

```pascal
program LowerToUpperCase;

var myString: string;

begin
  myString := ReadString('Введите строку: ');
  
  for var i := 1 to myString.Length do
  begin
    if myString[i] = 'а' then myString[i] := 'б'
    else if myString[i] = 'б' then myString[i] := 'а';
    
    
    writeln(myString[i], ' ', myString[i].isUpper);
    if myString[i].isUpper then myString[i] := myString[i].ToLower
    else myString[i] := myString[i].ToUpper;
  end;
  
  writeln('------');
  writeln(myString);
end.
```

# Задача 2
```pascal
program Palindrom;

var myString: string;

begin
  myString := ReadString('Введите строку:');
  
  for var i := 1 to myString.Length do
  begin
    if myString[i] <> myString[^i] then
    begin
      writeln('Число не является палиндромом');
      exit;
    end;
  end;
  
  writeln('Число является палиндромом');
end.
```

# Задача 3

```pascal
program MyFilePath;

var myFilePathSegments: array of string;

begin
  writeln(ReadString('Введите строку').Replace('/', #13#10))
end.
```

# Задача 4

```pascal
program StringSum;

var myString: string;

begin
  myString := ReadString('Введите строку: ');
  
  var myNumbers := myString.ToWords('+').Select(n -> n.toInteger);
  
  writeln('Сумма чисел: ', myNumbers.Sum);
end.
```

# Задача 5

```pascal
program MyName;

var myStrings: array of string;

begin
  myStrings := ReadString('Введите ФИО:').ToWords;
  
  writeln(myStrings[0], ' ' , myStrings[1][1], '. ', myStrings[2][1], '.');
end.
```
