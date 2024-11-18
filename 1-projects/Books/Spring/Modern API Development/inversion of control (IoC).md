In traditional programming, your code explicitly creates objects. With IoC, objects are created by the container and dependencies are injected automatically. For example, instead of writing `new UserService()`, you let Spring create and manage the UserService instead. 

The main benefits of IoC are _ since components are loosely coupled: 
- reduced dependency management
- improved modularity
- easier unit testing 

Traditional CLI programs were implemented using procedural programming - where the programmer runs code sequentially, one piece after another. However, the growth of the internet moved towards UI-based applications where user input dictated the flow of a program. Long ago, when mostly procedural ways of programming were dominant, you would have to look for a way to move the control flow from the procedural way to external sources such as a framework or components that determined the flow of the program. That movement is what is called **IoC**. It is a very generic principal and part of most frameworks. 