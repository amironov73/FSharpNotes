### Строки

Обычные строки .NET, но с небольшими дополнениями

```f#
let password = "abracadabra"

let multiline = "This string
takes up
multiple lines"
```

Если нужна длинная строка, ее можно разбить на несколько с помощью обратного слэша:

```f#
let longString = "abc-\
                 def-\
                 ghi"
                 
// Это означает: "abc-def-ghi"                 
```

Verbatim-строки:

```f#
let verbatimString = @"C:\Temp\File.txt"
```

Байтовая строка:

```f#
let hello = "Hello"B

// массив байт: [ 72uy; 101uy; 108uy; 108uy; 111uy ]
```

Тройные кавычки:

```f#
let byteString = """<message text="Hello" />"""
```


