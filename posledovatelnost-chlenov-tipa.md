# Последовательность членов типа

Предпочтение отдается выделению взаимосвязанных членов в одну группу с учетом приведенных ниже правил, но уже относительно группы.&#x20;

```csharp
[Header("View data")]
[SerializeField] private Image icon;
private Sprite _currentIcon;
public string CurrentIconName => currentIcon.name;

[Header("Timer data")]
[SerializeField] private int timerLenghtAtSeconds;
private Task _currentTimer;
private CancellationTokenSource _currentTimerToken_;
```

Так же внутри взаимосвязанной группы желательно рядом друг с другом держать члены одного типа.

```csharp
private int _firstValue;
private int _secondValue;
private string _firstName;
private string _secondName;
private int[] _integers_;
private string[] _strings;
```

Глобально последовательность сортировки членов класса по модификаторам должна выглядеть так:

* <mark style="color:blue;">`public -> [SerializeField] private -> protected -> internal -> private -> new -> abstract -> virtual -> override -> sealed -> static -> readonly -> extern -> unsafe -> volatile -> async`</mark>.&#x20;

Члены класса располагаются в следующем порядке:

* Внутренние классы, структуры, перечисления.
* Поля, свойства.
* Статические поля, константы и readonly-поля \ свойства.
* Конструкторы и финализаторы.
* Методы. Внутри каждой группы элементы должны располагаться в следующем порядке:
* <mark style="color:blue;">`public -> internal -> protected internal -> protected -> private`</mark>

С методами есть одна особенность. Располагать их нужно в предполагаемом порядке вызова. Но сохраняя при этом правило _работы с публичными и приватными методами_.

```csharp
 public sealed class exampleClass
 {
 	public void ShowExample() {}
 	public void HideExapmle() {}
 	private void StartExapmleWork() {}
 	private void OnUpdateExapmleView() {}
 	private void OnExapmleCompleteWork() {}
 	private void AutoHideExapmle(){}
 }
```

Здесь логика последовательна, но при этом сохраняются и _private \ public_ правила.
