### Hello, world!

```f#
[<EntryPoint>]
let main argv =
    printfn "Hello, world!"
    0
```

Того же эффекта можно добиться по-другому:

```f#
open System

let main argv =
    Console.WriteLine "Hello, world!"
    0
```
