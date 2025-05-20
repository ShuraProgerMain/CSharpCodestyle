# Методы



* Если метод можно уместить в одну команду возвращающую значение, стоит использовать [**expression body**](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/statements-expressions-operators/expression-bodied-members).

```csharp
public int Add(int a, int b) => a + b;
```

* Если тело метода состоит только из Switch с возвращаемым значением, то стоит использовать [**expression body**](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/statements-expressions-operators/expression-bodied-members)**.**

```csharp
public string GetColorName(Color color) =>
    color switch
    {
        Color.Red => "Красный",
        Color.Green => "Зелёный",
        Color.Blue => "Синий",
        _ => "Неизвестный цвет"
    };
```

* Старайтесь ограничить методы размером до 50-70 строк.&#x20;
* Если количество аргументов в вашем методе больше 5, стоит задуматься об использовании [**DTO**](data-transfer-object-dto.md).

