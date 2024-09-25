---
created: 2024-09-05T11:03
updated: 2024-09-25T20:58
---
In [[java]], you can tell the complier to treat a generic as a specific type. If the value cannot be cast, a `ClassCastExcetption` [[Exceptions]] will be thrown. 
```java 
UUID id = (UUID) rs.getObject("id"); //telling complier that the object will be UUID 
```

[[UUIDs]]