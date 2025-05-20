# Модификатор in

* Используйте модификатор  <mark style="color:blue;">`in`</mark> если в метод передается _reference-type_, который не должен быть изменен.
* Используйте модификатор  <mark style="color:blue;">`in`</mark> если в метод передается _readonly struct_, который не должен быть изменен.

> **ВАЖНО** отметить, что в случаях не описанных выше использование модификатора <mark style="color:blue;">`in`</mark> в паре со <mark style="color:blue;">`struct`</mark> может привести к проблемам с производительностью.
>
> Что бы этого избежать, стоит подробнее ознакомиться с принципами работы модификатора <mark style="color:blue;">`in`</mark> по ссылкам ниже.
>
>
>
> [c# 7.2 - Why would one ever use the "in" parameter modifier in C#? - Stack Overflow](https://stackoverflow.com/questions/52820372/why-would-one-ever-use-the-in-parameter-modifier-in-c)
>
> [The ‘in’-modifier and the readonly structs in C# - Developer Support (microsoft.com)](https://devblogs.microsoft.com/premier-developer/the-in-modifier-and-the-readonly-structs-in-c/)

