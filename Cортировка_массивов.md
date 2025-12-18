# Задача 1

> Дан массив 12 3 5 7 9 10. За один просмотр методом «пузырька» он становится отсортированным, остальные просмотры ничего не дают. Исключите лишние просмотры.

```pascal
var
  arr: array[1..6] of integer = (12, 3, 5, 7, 9, 10);
  n, i: integer;
  swapped: boolean;
begin
  n := 6;
  Write('Исходный массив: ');
  for i := 1 to n do
    Write(arr[i], ' ');
  WriteLn;
  
  swapped := true;
  while swapped do
  begin
    swapped := false;
    for i := 1 to n - 1 do
      if arr[i] > arr[i + 1] then
      begin
        Swap(arr[i], arr[i + 1]);
        swapped := true;
      end;
  end;
  
  Write('Отсортированный массив: ');
  for i := 1 to n do
    Write(arr[i], ' ');
end.
```

# Задача 2

> Массив 12 3 5 7 9 10 сортируется методом пузырька за один просмотр, а массив 5 7 9 10 12 3 --- за пять (N-1). Напишите программу, реализующую модификацию этого метода, одинаково хорошо (или одинаково плохо?) сортирующую подобные массивы. Устранить «неравноправие» можно путем смены направлений просмотров, то есть первоначально в направлении → получаем 5 7 9 10 3 12, а затем в направлении ←, результат --- 3 5 7 9 10 12. И так чередуем направления, пока массив не будет отсортирован.

```pascal
var
  arr: array[1..6] of integer = (5, 7, 9, 10, 12, 3);
  n, i: integer;
  swapped: boolean;
  direction: integer; // 1 - слева направо, -1 - справа налево
begin
  n := 6;
  Write('Исходный массив: ');
  for i := 1 to n do
    Write(arr[i], ' ');
  WriteLn;
  
  swapped := true;
  direction := 1;
  
  while swapped do
  begin
    swapped := false;
    
    if direction = 1 then
    begin
      // Слева направо
      for i := 1 to n - 1 do
        if arr[i] > arr[i + 1] then
        begin
          Swap(arr[i], arr[i + 1]);
          swapped := true;
        end;
    end
    else
    begin
      // Справа налево
      for i := n - 1 downto 1 do
        if arr[i] > arr[i + 1] then
        begin
          Swap(arr[i], arr[i + 1]);
          swapped := true;
        end;
    end;
    
    direction := -direction; // Меняем направление
  end;
  
  Write('Отсортированный массив: ');
  for i := 1 to n do
    Write(arr[i], ' ');
end.
```

# Задача 3

> Объедините требования заданий 2 и 3 в единое целое. Этот метод называется «шейкер-сортировкой». Реализуйте его.

```pascal
var
  arr: array[1..6] of integer = (5, 7, 9, 10, 12, 3);
  n, left, right, i: integer;
  swapped: boolean;
begin
  n := 6;
  Write('Исходный массив: ');
  for i := 1 to n do
    Write(arr[i], ' ');
  WriteLn;
  
  left := 1;
  right := n;
  swapped := true;
  
  while (left < right) and swapped do
  begin
    swapped := false;
    
    // Проход слева направо
    for i := left to right - 1 do
      if arr[i] > arr[i + 1] then
      begin
        Swap(arr[i], arr[i + 1]);
        swapped := true;
      end;
    right := right - 1;
    
    if not swapped then break;
    
    // Проход справа налево
    for i := right downto left + 1 do
      if arr[i - 1] > arr[i] then
      begin
        Swap(arr[i - 1], arr[i]);
        swapped := true;
      end;
    left := left + 1;
  end;
  
  Write('Отсортированный массив: ');
  for i := 1 to n do
    Write(arr[i], ' ');
end.
```

# Задача 4

> В сортировке простыми вставками уберите переменную x, то есть внутренний цикл запишите в виде: `While A[0] < A[j] Do...`  
> *Подсказка.* Массив А необходимо объявить так: `Array[0..Nmax] Of Integer` и i-й элемент записывать на нулевое место (`A[0]:=A[i]`). Это так называемый прием барьерного элемента.

```pascal
const
  N = 6;
var
  arr: array[0..N] of integer;
  i, j: integer;
begin
  // Инициализация массива (индексы 1..N)
  arr[1] := 12; arr[2] := 3; arr[3] := 5;
  arr[4] := 7; arr[5] := 9; arr[6] := 10;
  
  Write('Исходный массив: ');
  for i := 1 to N do
    Write(arr[i], ' ');
  WriteLn;
  
  // Сортировка вставками с барьерным элементом
  for i := 2 to N do
  begin
    arr[0] := arr[i]; // Барьерный элемент
    j := i - 1;
    
    while arr[0] < arr[j] do
    begin
      arr[j + 1] := arr[j];
      j := j - 1;
    end;
    
    arr[j + 1] := arr[0];
  end;
  
  Write('Отсортированный массив: ');
  for i := 1 to N do
    Write(arr[i], ' ');
end.
```
