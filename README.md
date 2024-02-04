# Clean(Onion) Architecture


### Overview of the N-Layer Architecture
* Data Access(Database) is the Core of the Entire Application 
* The most popular Architecture 


```
[Presentation] ==> [Business Logic] ==> [Data Access]

** '==>': Project Dependency

* Presentation - Interact access point (WebApi, MVC, Webforms ...)
* Business Logic - 🤟Logic of Business requirements
* Data Access - Database access point


#### Disadvantages of N-Layer Architecture
 * Project Dependency
 * Highly decoupled structure
 * Lower scalable/Flexibility applications
```





### Clean(Onion) Architecture

#### >> Core Layer(Domain and Application Layer) 
Domain(Entity) is the Core of the Entire Application 

Core Layers(Domain and Application Layer) is at the center

```
🙋💥
Domain Layer - (Solution-wise) Enterprise logic and entities
Application Layer - (Application-specific) Interfaces and types

- Difference
Domain Layer: Common types across the entire enterprise and sharable with other solutions
Application Layer: Application-specific types and interfaces(DIP, Higher scalability)

The interfaces in the Application Layer will be implemented in the external layer(DIP, Higher scalability)
** DIP: Dependency Inversion Principle
```

#### >>  Presentation Layer
Projects that users can access (i.e. WebApi, Mvc Project, etc.)
```
For example,
- WebApi Project
- Mvc Project
- Webforms Project
-, etc.
```
#### >>  Infrastructure Layer
Tricky a bit. Infrastructure can be anything.

```
For example,
- Entity Framework Core Layer for Accessing the DB
- Layer specifically made to generate JWT Tokens for Authentication
- Hangfire Layer
-, etc.

```

## Implementing Onion Architecture in ASP.NET Core WebApi Project

