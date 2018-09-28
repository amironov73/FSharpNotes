### Элементарные (встроенные) типы

Числовые

| Тип F# | Суффикс | Тип .NET | Тип C#
|--------|---------|----------|-------
| byte | uy | System.Byte | byte  
| sbyte | y | System.SByte | sbyte
| int16 | s | System.Int16 | short
| uint16 | us | System.Uint16 | ushort 
| int, int32 | | System.Int32 | int
| uint32 | u | System.UInt32 | uint
| int64 | L | System.Int64 | long
| uint64 | UL | System.UInt64 | ulong
| float | | System.Double | double
| float32 | f | System.Single | float
| decimal | M | System.Decimal | decimal

Можно использовать префиксы `0x`, `0o` и `0b`: `0xFCAF`, `0o7771L`, `0b0101y`.
