# CleanArchitecture.API.Template

# Api.Template

This is a starting point (TEMPLATE) for Clean Architecture with ASP.NET Core. [Clean Architecture](https://8thlight.com/blog/uncle-bob/2012/08/13/the-clean-architecture.html) is just the latest in a series of names for the same loosely-coupled, dependency-inverted architecture. You will also find it named [hexagonal](http://alistair.cockburn.us/Hexagonal+architecture), [ports-and-adapters](http://www.dossier-andreas.net/software_architecture/ports_and_adapters.html), or [onion architecture](http://jeffreypalermo.com/blog/the-onion-architecture-part-1/).

## Summary

This project Api.Template cover concepts about:
  
 - CQRS (http://www.codeproject.com/Articles/555855/Introduction-to-CQRS)
 - Dependency Injection (http://en.wikipedia.org/wiki/Dependency_injection)
 - Loose Coupling (http://en.wikipedia.org/wiki/Loose_coupling)
 - Onion Architecture (http://jeffreypalermo.com/blog/the-onion-architecture-part-1/)
 - SOLID Principles (http://en.wikipedia.org/wiki/SOLID_%28object-oriented_design%29)
 - Cross Cutting Concerns: (http://en.wikipedia.org/wiki/Cross-cutting_concern)
 - Hexagonal Architecture:(https://herbertograca.com/2017/11/16/explicit-architecture-01-ddd-hexagonal-onion-clean-cqrs-how-i-put-it-all-together/)

## Learning Path:
- [SOLID Principles of Object Oriented Design](https://www.pluralsight.com/courses/principles-oo-design)
- [Domain-Driven Design Fundamentals](https://www.pluralsight.com/courses/domain-driven-design-fundamentals)

## DotNetCore

Using .NETCore version 2.2 

## 3rd Party Nuget Packages 
 
- Autofac
- AutoMapper
- FluentAssertiong
- EFCore
- NUnit
- Swagger (Swashbuckle) 
- Serilog
 
## Development Tools

 - Visual Studio (2017 or newer) or Visual Studio Code
 - Azure DevOps ( Backlog and Code Repository)
 - MSSQL Server Management Studio 17 
 - Swagger Editor 
 - GIT

## How to clone this project

```
cd\
mkdir repo
cd repo
git clone https://github.com/diegosmorf/CleanArchitecture.API.Template.git
```

### Cloning the strucuture using your namespace
```
powershell .\CopyProject.ps1 "Api.Template" "Your.Namespace"
cd ..\Your.Namespace
```

### Restore, Build and Test
```
dotnet restore
dotnet build
dotnet test


dotnet run --p Api.Template.WebApi

```

you can access this API via browser: http://localhost:5200/swagger

## 0 - Core
Api.Common.Cqrs.Core is a basic set of interfaces for building a command and event driven CQRS application. 

- Commands are created and dispatched by the application, 
- They are received by command handlers which apply behaviors on the domain model
- Which generates events 
- Collected by the command handler
- Then published
- Received by event handlers which update the read/query model 
- Consumed by the front end of the application via query services.

## 1 - Domain
Domain commands and handlers specifically affect the domain model's aggregate roots. 

Some of the basic premises of CQRS are modeled by these interfaces either explicitly or in their documentation.

- Commands and events should be immutable
- The query model should be immutable, except from the event handlers responsible for updating them when triggered by events published from domain model changes
- Domain commands and handlers should only affect a single aggregate root instance in the domain model - more complex operations should be handled by sagas

## 2 - Application Service
This project will expose domain features to external world (e.g.: apis, apps, windows services, desktop apps) and it is responsible for business rules as well.

## 3 - Infrastructure

This project contains implementations of the interfaces defined in the inner layers of the solution. They may be dependent on external libraries or resources. Note that the implementations themselves are internal and should only be used for injection via their implemented interfaces. 

## 4 - Entry Points 

API project.

## 5 - Tests

DomainTest: NUnit will test ApplicationService classes with no external dependencies. All Infrastructure dependencies must be mocked. 

IntegrationTests:Longer running, more involved tests that test the integration of multiple components and external dependencies as Database/Email.

AcceptanceTests: SpecFlow acceptance tests project (may modify data, so are meant to run in non-production environments)

## You shouldn't find:

  - Binaries committed to source control.
  - Unnecessary project or library references or third party frameworks.
  - Many "try" blocks - code defensively and throw exceptions if something is wrong.
  - Third party APIs exposed via public interfaces.
