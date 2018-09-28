### Конвейерные операторы

Прямой конвейерный оператор (pipe-forward operator) определен как

```f#
let (|>) x f = f x
```

Он нужен для того, чтобы указывать аргумент функции перед ее именем. Это позволяет рисовать "паровозы" из вызовов функций

```f#
[2; 3; 1] |> List.sort |> List.iter (printfn "%d")
```

Пример полезной программы с "паровозом" - подсчет общего объема файлов в указанной папке

```f#
open System.IO

let folderSize folder =
    let len file = (new FileInfo(file)).Length
    Directory.GetFiles folder
    |> Array.map len
    |> Array.sum
    
[<EntryPoint>]
let main argv =    
    printfn "%d" (folderSize argv.[0])
    0
```

Обратный конвейерный оператор (pipe-backward operator) определен как

```f#
let (<|) f x = f x
```

Он позволяет изменить порядок вычислений и избавиться от скобок:

```f#
let sum x y = x + y
printfn "%d" <| sum 1 2
// Вместо printfn "%d" (sum 1 2)
```


