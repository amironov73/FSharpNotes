### Цикл for

Целочисленный вариант

```f#
for i = 1 to 5 do
    printfn "i = %d" i
    
// 1
// 2
// 3
// 4
// 5    
```

Значение i менять вручную нельзя!

Вариант с перечислением

```f#
let fruits = ["apple"; "lemon"; "pear"]

for fruit in fruits do
    printfn "%s" fruit
```

Использование сопоставления с образцом

```f#
type Pet =
    | Cat of string * int
    | Dog of string
    
let famousPets = [ Dog("Lassie"); Cat("Felix", 9); Dog("Rin Tin Tin")]

for Dog(name) in famousPets do
    printfn "Famous dog %s" name
// Выведет на консоль только собак    
```
