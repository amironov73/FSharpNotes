### Провайдеры типов данных

Замечательный фреймворк FSharp.Data позволяет поднять работу с данными на качественно новый уровень. Предлагаемый фреймворком алгоритм работы с данными таков:

Показываем фреймворку образец данных, по которому он строит типизированный интерфейс доступа к данным
Закачиваем реальные данные
Работаем с ними, используя всю мощь F#, .NET и статической типизации
В составе FSharp.Data поставляются следующие провайдеры:

* CSV Type Provider
* HTML Type Provider
* JSON Type Provider
* XML Type Provider
* WorldBank Provider

Вот простейший пример работы с CSV-файлами:

```f#
open FSharp.Data
 
// Обучаем провайдер на образце данных
type Books = CsvProvider<"Books.csv">
 
// В итоге получаем полноценный тип с полями, соответствующими столбцам данных
 
// Загружаем данные, можно из Сети
let books = Books.Load("https://raw.githubusercontent.com/"
        + "zygmuntz/goodbooks-10k/master/samples/books.csv")
 
// Отбираем первые 10 книг с рейтингом, выше 3.0
let firstBooks = 
  books.Rows 
  |> Seq.filter (fun x -> x.Average_rating > 3.0m)
  |> Seq.take 10
 
for row in firstBooks do
    printfn "%A %A %A" row.Authors row.Title row.Isbn
```

Типичный вывод:

```text
"Suzanne Collins" "The Hunger Games (The Hunger Games, #1)" "439023483"
"J.K. Rowling, Mary GrandPre" "Harry Potter and the Sorcerer's Stone (Harry Potter, #1)" "439554934"
"Stephenie Meyer" "Twilight (Twilight, #1)" "316015849"
"Harper Lee" "To Kill a Mockingbird" "61120081"
"F. Scott Fitzgerald" "The Great Gatsby" "743273567"
"John Green" "The Fault in Our Stars" "525478817"
"J.R.R. Tolkien" "The Hobbit" "618260307"
"J.D. Salinger" "The Catcher in the Rye" "316769177"
"Dan Brown" "Angels & Demons  (Robert Langdon, #1)" "1416524797"
"Jane Austen" "Pride and Prejudice" "679783261"
```

Имеется также FSharp.Data.SqlClient, который позволяет работать с SQL тремя способами:

* SqlCommandProvider
* SqlProgrammabilityProvider
* SqlEnumProvider

Пример для SqlCommandProvider:

```f#
open FSharp.Data
 
[<Literal>]
let connectionString = 
    @"Data Source=.;Initial Catalog=AdventureWorks2012;Integrated Security=True"
 
do
    use cmd = new SqlCommandProvider<"
        SELECT TOP(@topN) FirstName, LastName, SalesYTD 
        FROM Sales.vSalesPerson
        WHERE CountryRegionName = @regionName AND SalesYTD > @salesMoreThan 
        ORDER BY SalesYTD
        " , connectionString>(connectionString)
 
    cmd.Execute(topN = 3L, regionName = "United States", salesMoreThan = 1000000M) |> printfn "%A"
 
//output
//seq
//    [("Pamela", "Ansman-Wolfe", 1352577.1325M);
//     ("David", "Campbell", 1573012.9383M);
//     ("Tete", "Mensa-Annan", 1576562.1966M)]
```

Пример для SqlProgrammabilityProvider:

```f#
type AdventureWorks = SqlProgrammabilityProvider<connectionString>
do
    use cmd = new AdventureWorks.dbo.uspGetWhereUsedProductID(connectionString)
    for x in cmd.Execute( StartProductID = 1, CheckDate = System.DateTime(2013,1,1)) do
        //check for nulls
        match x.ProductAssemblyID, x.StandardCost, x.TotalQuantity with 
        | Some prodAsmId, Some cost, Some qty ->
            printfn "ProductAssemblyID: %i, StandardCost: %M, TotalQuantity: %M" prodAsmId cost qty
        | _ -> ()
 
//output
//ProductAssemblyID: 749, StandardCost: 2171.2942, TotalQuantity: 1.00
//ProductAssemblyID: 750, StandardCost: 2171.2942, TotalQuantity: 1.00
//ProductAssemblyID: 751, StandardCost: 2171.2942, TotalQuantity: 1.00
```

Ещё отметим пакет FSharp.Data.TypeProviders, предоставляющий следующие провайдеры типов:

* EdmxFile
* ODataService
* SqlDataConnection
* SqlEntityConnection
* WsdlService
* DbmlFile

