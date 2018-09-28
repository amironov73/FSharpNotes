### Сопоставление с образцом

```f#
let isOdd x = (x % 2 = 1)
let describe x =
    match isOdd x with
    | true -> "odd"
    | _ -> "even"
    
[1 .. 3] |> List.map describe
// ["odd"; "even"; "odd"]
```

Еще пример

```f#
let testAnd x y =
    match x, y with
    | true, true -> true
    | _, _ -> false
```

Именованные образцы:

```f#
let greet name =
    match name with
    | "Robert" -> printfn "Hello, Bob"
    | "William" -> printfn "Hello, Bill"
    | x -> printfn "Hello, %s" x
```

Ограничение when:

```f#
let estimate x =
    match x with
    | _ when x < 100 -> "Value is too small"
    | _ when x > 500 -> "Value is too big"
    | _ -> "Good value"

[150; 15; 700] |> List.map estimate
// ["Good value"; "Value is too small"; "Value is too big"]
```

Группировка значений:

```f#
let isVowel c =
    match c with
    | 'a' | 'e' | 'i' | 'o' | 'u' -> true
    | _ -> false
    
"Hello" |> Seq.map isVowel
// [false; true; false; false; true]   
```

Сопоставление со списком

```f#
let rec len theList =
    match theList with
    | [] -> 0
    | [_] -> 1
    | hd::tail -> 1 + len tail
    
len [1; 2; 3]    
```
