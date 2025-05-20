# IsNullOrEmpty vs IsNullOrWhitespace

#### IsNullOrEmpty vs IsNullOrWhiteSpace

* Если пробел в качестве единственного символа это все равно ошибка, используйте <mark style="color:blue;">`IsNullOrWhiteSpace`</mark>.
* Если пробел в качестве единственного символа это валидное значение, используйте <mark style="color:blue;">`IsNullOrEmpty`</mark>.
* [Сами Microsoft заявляют, что IsNullOrWhiteSpace быстрее](https://learn.microsoft.com/ru-ru/dotnet/api/system.string.isnullorwhitespace?view=net-8.0) но если посмотреть исходный код, то тело этого метода более громоздкое в плане инструкций, что заставляет сомневаться в словах MSDN.

[Source code:](https://referencesource.microsoft.com/mscorlib/R/55e241b6143365ef.html)

```csharp
[Pure]
public static bool IsNullOrEmpty(String value) {
	return (value == null || value.Length == 0);
}

[Pure]
public static bool IsNullOrWhiteSpace(String value) {
	if (value == null) return true;

	for(int i = 0; i < value.Length; i++) {
		if(!Char.IsWhiteSpace(value[i])) return false;
	}

	return true;
}
```
