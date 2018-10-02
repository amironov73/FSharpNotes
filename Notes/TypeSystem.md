### Система типов

```f#
type CheckNumber = int
type CardNumber = string
type CardType = Visa | MasterCard
type CreditCardInfo = CardType * CardNumber

type PaymentMethod =
 | Cash
 | Check of CheckNumber
 | Card of CreditCardInfo

type PaymentAmount = decimal
type Currency = EUR | USD

type Payment = {
 Amount: PaymentAmount
 Currency: Currency
 Method: PaymentMethod
}

let payment1 = { Amount = PaymentAmount(100); Currency = USD; Method = Cash }
let payment2 = { Amount = PaymentAmount(110); Currency = EUR; Method = Check(12345) }
let payment3 = { Amount = PaymentAmount(120); Currency = EUR; Method = Card(Visa, "123456") } 

let payments = [ payment1; payment2; payment3 ]

payments
 |> List.map (fun x -> x.Method)
 |> List.iter ( printfn "%A" )
```