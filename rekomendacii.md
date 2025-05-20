# Рекомендации

* Если нужно присвоить значение какой-то переменной лишь в случае, когда она равна `null` то можно обойтись без конструкции `if` обойдясь следующей записью:

```csharp
SomeClass someVar;

someVar ??= new SomeClass(); 
```

Здесь весь "`if`" спрятан в операторе `??`.

* По возможности не стоит опускать **Pattern Matching**.

> \[!tip] Почитать о нем можно по ссылкам ниже:
>
> [Patterns - Pattern matching using the is and switch expressions. - C# | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/patterns#constant-pattern) [C# и .NET | Pattern matching (metanit.com)](https://metanit.com/sharp/tutorial/3.34.php)
