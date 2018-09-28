### Функции

```f#
let square x = x * x // Функция одной переменной
// int -> int

let add x y = x + y // Функция двух переменных
// int -> int -> int
```

Аннотации типов в функциях

```f#
let add (x: float) y = x + y
// float -> float -> float
```

Обобщенные функции

```f#
let ident (x: 'a) = x
// 'a -> 'a
```

Если хочется вернуть значение `unit`, можно воспользоваться функцией ignore, которая затеняет переданное ей значение:

```f#
ignore (square 4)
```

Прямой оператор композиции (forward composition operator) определен так:

```f#
let (>>) f g x = g (f x)
```

Пример

```f#
let cube x = x * x * x
let superCube = cube >> cube
superCube 2
// 512 = (2 * 2 * 2) * (2 * 2 * 2) * (2 * 2 * 2)
```

Обратный оператор композиции (backward composition operator) определен так:

```f#
let (<<) f g x f (g x)
```

Пример:

```f#
let cube x = x * x * x
let negate x = -x

(cube << negate) 10
```


