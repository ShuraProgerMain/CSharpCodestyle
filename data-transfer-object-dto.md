# Data Transfer Object(DTO)

DTO представляют собой объекты используемые для передачи между разными компонентами системы.&#x20;



Пример DTO:

```csharp
public readonly struct UserDTO
{
    public readonly int Id;
    public readonly string UserName;
    public readonly string Email;
    
    public UserDTO(int id, string userName, string email)
    {
        Id = id;
        UserName = userName;
        Email = email;
    }
}
```
