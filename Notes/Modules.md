### Модули

```f#
module Info

let name = "Alexey"
```

На имя из другого модуля ссылаются так: `Info.name`.

Могут быть вложенные модули

```f#
module Conversions

    module Length
    
        let toFoot x = x * 3.28084
    
    module Temperature
    
        let toKelvin x = x + 273.15      
```
