# Clean(Onion) Architecture


### Overview of the N-Layer Architecture
* Data Access(Database) is the Core of the Entire Application 
* The most popular Architecture 


![N-Layer Architecture](img/N-LayerArchitecture.jpg)
```
[Presentation] ==> [Business Logic] ==> [Data Access]

** '==>': Project Dependency

- Presentation - Interact access point (WebApi, MVC, Webforms ...)
- Business Logic - 🤟Logic of Business requirements
- Data Access - Database access point


Disadvantages of N-Layer Architecture
- Project Dependency
- Highly decoupled structure
- Lower scalable/Flexibility applications
```





# Clean(Onion) Architecture
![clean_architecture](img/clean_architecture.jpg)
#### >> Core Layer(Domain and Application Layer) 
Domain(Entity) is the Core of the Entire Application 

Core Layers(Domain and Application Layer) is at the center

```
🙋💥
Domain Layer - (Solution-wise) Enterprise logic and entities
Application Layer - (Application-specific) Interfaces and types

Difference
- Domain Layer: Common types across the entire enterprise and sharable with other solutions
- Application Layer: Application-specific types and interfaces(DIP, Higher scalability)

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
- ,etc.
```
#### >>  Infrastructure Layer
Tricky a bit. Infrastructure can be anything.

```
For example,
- Entity Framework Core Layer for Accessing the DB
- Layer specifically made to generate JWT Tokens for Authentication
- Hangfire Layer
- ,etc.

```

## Implementing Onion Architecture in ASP.NET Core WebApi Project

```
<Features and Tech>
- Onion Architecture
- Entity Framework Core
- .NET Core 3.1 Library / .NET Standard 2.1 Library / ASP.NET Core 3.1 WebApi
- Swagger
- CQRS / Mediator Pattern using MediatR Library
- Wrapper Class for Responses
- CRUD Operations
- Inverted Dependencies
- API Versioning

```

#### 1. Adding The Entities to the Domain Project
```
🙋💥
Domain Layer - (Solution-wise) Enterprise logic and entities

- models/entities
- Exception
- Validation rules
- Settings
- Common things throughout the solution.
```


#### 2. Adding the Required Interfaces And Packages in the Application Layer

```
🙋💥
Application Layer - (Application-specific) Interfaces and types

1. Add Reference to the Domain Project.
2. install the required packages via Console
    Install-Package MediatR.Extensions.Microsoft.DependencyInjection
    Install-Package Microsoft.EntityFrameworkCore
3. Add an IApplicatoinDbContext
- models/entities
- Exception
- Validation rules
- Settings
- Common things throughout the solution.
```

### CQRS (Command Query Responsibility Segregation)
```
Commands: Insert/Modify/Remove Operations on the system
Queries:  Fetch data from the database

🤷 What does CORS do for Clean Architecture?
Each query handler and command handler are responsible for only one operation and one responsibility.
-> 💥 No Dependecy(Clean Architecture's goal: Scalability/Flexibility/Low-coupled) 
```

### Mediator (Command Query Responsibility Segregation)
```
MediatR nuget package is to communicate between objects and it helps in achieving the CQRS pattern and clean architecture by reducing dependency among objects.

🤷 What does MediatR do for Clean Architecture?

<Set up the MediatR usage case>
1. Dependency Setup
                                            Core
API(Presentation Layer) ==> [ Application Layer ==> Domain Layer ] 

2. Install the MediateR  in API(Presentation Layer)

3. Add the MediatR to our controller
   var clients = await _mediator.Send(new GetCustomersQuery());  
   In the API controller, the MediateR is responsible for sending the GetCustomersQuery 
   and this is how it interacts with the other objects.

In this current scenario( I said 'in this scenario of interaction b/w objects), 
💥 there is no dependency!!! 
   The API does not depend on the Application Layer.
   Instead, Api is to send the command and receive the command using Mediator.
   Loosely coupled

🤷 So again, What does MediatR do for Clean Architecture?
   MediatR nuget package helps in achieving the CQRS pattern and clean architecture.
   - MediatR in the controller of the API sends and receives commands to the Application Layer(Project) without a dependency.
```
