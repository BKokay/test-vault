*Naming* - use nouns and not verbs in REST apis. Using verbs would make it an RPC endpoint. In REST, you transfer states and not the instructions. Use the plural form for naming the collection resource in the endpoint path

[[spring]] was initially looked at as a Java Enterprise Edition (JEE) alternative, but it has become preferred over JEE. Spring supports [[dependency injection]] (DI), also known as [[inversion of control (IoC)]] and [[aspect-oriented programming (AOP)]] out of the box. 

[[Beans]] are java objects that are managed by the IoC containers. The developer supplies the configuration to an IoC container (using code, annotations, or xml). The container then uses the metadata to construct, assemble, and manage beans. Each bean shoud have a unique identifier inside a container. A bean can have more than one identity using an **alias**. 

