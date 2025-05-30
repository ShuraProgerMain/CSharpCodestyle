# Именование идентификаторов

Все правила _именования идентификаторов_ подробно описаны на [**RSDN**](https://rsdn.org/article/mag/200401/codestyle.XML).&#x20;

Однако следует обратить внимание на пару замечаний.

* Именование _<mark style="color:blue;">`[SerializeField] private protected internal`</mark>_ - полей пишется **без** нижнего подчеркивания. Иначе говоря, идентично _`public`_ полям.
* Имена полей в [**DTO**](data-transfer-object-dto.md) пишутся в `PascaleCase` вне зависимости от того, являются они свойствами или нет.

> Поскольку и _<mark style="color:blue;">`public`</mark>_ и _<mark style="color:blue;">`[SerializeField] private protected internal`</mark>_ поля могут быть модифицированы в инспекторе, использование одинакового стиля именования для этих полей обеспечивает единообразие и улучшает читаемость кода, позволяя сразу понимать, что поля могут быть изменены в инспекторе.
