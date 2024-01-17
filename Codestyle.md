# Официальные рекомендации
Основная информация о том, каких подходов следует придерживаться при написании когда непосредственно на C# приведена на **[MSDN](https://learn.microsoft.com/ru-ru/dotnet/csharp/fundamentals/coding-style/coding-conventions)**
Так же часть информации взята с соглашения **[RSDN](https://rsdn.org/article/mag/200401/codestyle.XML)**

### Уточнения, которые на MSDN не присутствуют

**Делегаты** - Microsoft пишет, что нужно вызывать делегаты в формате:
``` csharp
actionExample(args)
```

Но мы так делать не будем, потому что это создает необходимость писать дополнительный `if`. 

Вместо этого продолжим использовать:

```csharp
actionExample?.Invoke(args)
```

**Оператор `new`** - везде где можно используем запись вида `new ()`. А значит в объявлениях локальных функциях заменяем `var` на создаваемый тип. 
Пример:
```csharp
// Before
var exampleClass = new ExampleClass();

// After
ExampleClass exampleClass = new ();
```

**Обработка событий** - лямбда-выражения используются только для коротких обработчиков не содержащих вычисления. Во всех остальных случаях *обработчики* выносятся в отдельный метод.

**Запросы LINQ** - по возможности не используются в рантайме Unity. Или используются но на уровне инициализации типов. 

**Комментарии** - очень желательно избегать их существования в принципе за исключением ситуаций с неоднозначными вычислениями. 
Целессообразно оставлять комментарии которые дадут понять за счет чего происходят те или иные вычисления если название метода\класса не дают полноты картины. 
Так же логичны комментарии с сылками на более подробное объяснение логики работы вычислений находящиеся в ГДД или таблицах геймдизайнеров. 

**TODO** - не используются. Альтернативой служит вынесение на обсуждение и последующее создание задачи или отказ от действий. 

**XML-комментарии** - не используются, если только вы не пишете публичный API. 
> [!NOTE]-
> К примеру, когда вы пишете класс в C# своего внутреннего проекта, то писать там XML-комментарии будет скорее моветоном и показателем не достаточно хорошо прописанного класса. 
> 
> В то же время если пишется EditorScript или вспомогательный метод с "особым" поведением. То к такому коду XML-комментарии могут быть написаны но лишь в случае острой в них необходимости. 
> 
> Ну и ситуацией, когда XML-комментарии скорее необходимы, это когда вы пишете публичный API с которым будут работать только на вызов люди, которым не нужно лезть в детали реализации что бы понять, что произойдет. 

# Последовательность членов типа
Для большего удобства при "чтении" кода, необходимо всем придерживаться определенных правил не только в нейминге, но и в расположении членов типа.

Предпочтение отдается выделению взаимосвязынных членов в одну группу с учетом приведенных ниже правил, но уже относительно группы. 
Тем не менее **все поля располагаются в начале типа и никогда не располагаются между методами.**

> [!example]-
> ```csharp
> [Header("View data")]
> [SerializeField] private Image icon;
> private Sprite _currentIcon;
> public string CurrentIconName => currentIcon.name;
>
>[Header("Timer data")]
>[SerializeField] private int timerLenghtAtSeconds;
>private Task _currentTimer;
>private CancellationTokenSource _currentTimerToken_;
>```

Так же внутри взаимосвязной группы желательно рядом друг с другом держать члены одного типа(List под List \ int под int и т.д). 

>[!example]-
>
>```csharp
>private int _firstValue;
>private int _secondValue;
>private string _firstName;
>private string _secondName;
>private int[] _integers_;
>private string[] _strings;

Ожидаемая последовательность выглядит так: 
Ниже будет просто `private` но подразумевать стоит иерархическую последовательность `internal -> protected -> private`

- `public` поля
- **`SerializeField private`** поля
- `private` поля
- `public` cобытия и делегаты
- `private` cобытия и делегаты
- Индексаторы
- `public` свойства
- `private` свойства
- `public` методы
- `private` методы

С методами есть одна особенность. Располагать их нужно в предполагаемом порядке вызова. Но сохраняя при этом правило *работы с публичными и приватными методами*.

>[!example]-
>```csharp
> public sealed class ExampleClass
> {
> 	public void ShowExample() {}
> 	public void HideExample() {}
> 	private void StartExampleWork() {}
> 	private void OnUpdateExampleView() {}
> 	private void OnExampleCompleteWork() {}
> 	private void AutoHideExample(){}
> }
>```
>Здесь логика последовательна, но при этом сохраняются и *private \ public* правила. 


# Именование идентификаторов
Здесь я за основу беру правила *именования идентификаторов* от **[RSDN](https://rsdn.org/article/mag/200401/codestyle.XML)**. При этом есть лишь одно замечание.

- Именование *`[SerializeField] private protected internal`* - полей пишется **без** нижнего подчеркивания. Иначе говоря, идентично *`public`* полям.

>[!info]-
>Поскольку и *`public`* и *`[SerializeField] private protected internal`* поля могут быть модифицированы в инспекторе, куда целесообразнее видеть их одинаковыми, что бы сразу понимать ситуацию.

# Конкретнее о методах

- Использование **[expression bodies](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/statements-expressions-operators/expression-bodied-members)** там где это возможно. 
> [!info]-
> Считаю целесообразным использование *expression bodies* в ситуациях, когда тело метода можно представить исключительно возвращаемым значением.

- Использование модификатора **`in`** когда в метод передается `class` состояние которых должно оставаться неизменным. При передаче `struct` стоит задуматься на сколько необходимо и допустимо использование данного модификатора для производительности. 
>[!warning]-
> Не правильное использование *`in`* с типом `struct` может привести к проблемам с производительностью!

> [!info]-
> Как правило использовать *`in`* имеет смысл в ситуациях с "большими" структурами что бы не создавать лишнюю копию в процессе передачи и в процессе работы со структурой в методе.

- По возможности ограничить методы размером до 50-70  строк. 
- Количество аргументов метода не должно превышать 10.

> [!tip]-
> В случае неуверенности в понимании того, что такое *`in`* и как оно работает можно почитать немного информации по ссылкам ниже.
>
>[c# 7.2 - Why would one ever use the "in" parameter modifier in C#? - Stack Overflow](https://stackoverflow.com/questions/52820372/why-would-one-ever-use-the-in-parameter-modifier-in-c)
>[The ‘in’-modifier and the readonly structs in C# - Developer Support (microsoft.com)](https://devblogs.microsoft.com/premier-developer/the-in-modifier-and-the-readonly-structs-in-c/)

# Конкретнее о классах

- Для всех классов, от которых не подразумевается возможность наследования используем модификатор *`sealed`*.
- Количество аргументов конструктора недолжно превышать 10.
- Классы, которым нужно обеспечить неизменяемость, а так же используемые для сравнения в качестве ключа(или чего-то в этом роде), заменяются на *[`record`](https://habr.com/ru/amp/publications/675560/)*.
- Обобщенные классы, по возможности, должны иметь модификатор *`where`* с указанием родительских типов.
>[!example]-
>```csharp
>public class AGenericClass<Т> where T : IComparable<Т> { }; 
>```

# Nullable типы

- Если тип по какой-то причине может быть `null`, не зависимо от того ссылочный он или значимый, он должен быть `Nullable`, но использовать конструкцию `Nullable<T>` явно смысла нет, достаточно использовать `?`
>[!tip]-
> https://habr.com/ru/articles/786082/?utm_campaign=786082&utm_source=habrahabr&utm_medium=rss


# Throw Exception

- Генерировать исключение имеет смысл только в тех случаях, когда от результата работы метода зависит дальнейшая стабильность приложения. Во всех остальных случаях имеет смысл использовать иные способы регистрации проблем, которые не портят пользовательский опыт.

# Рекомендации
- **`IsNullOrWhiteSpace`** необходимо использовать вместо *`IsNullOrEmpty`*. [Сами Microsoft заявляют, что первый вариант производительнее. ](https://learn.microsoft.com/ru-ru/dotnet/api/system.string.isnullorwhitespace?view=net-8.0#-----------)
- Использование оператора `??` там, где это нужно. 
- По возможности не стоит опускать **Pattern Matching**.
> [!tip]-
> Почитать о нем можно по ссылкам ниже:
> 
> [Patterns - Pattern matching using the is and switch expressions. - C# | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/patterns#constant-pattern)
> [Patterns - Pattern matching using the is and switch expressions. - C# | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/patterns#constant-pattern)
> [C# и .NET | Pattern matching (metanit.com)](https://metanit.com/sharp/tutorial/3.34.php)
