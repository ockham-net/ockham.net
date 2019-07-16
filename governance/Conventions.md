# Conventions

### Terminology

*See Terminology.md*

## General 

 - Every solution **must** solve a clear problem that is not solved in the .Net BCL, or in the particular libraries it is meant to augment. A problem can include making existing functionality simpler to use, but APIs should avoid *replacing* existing technologies in favor of augmenting them such as through extension methods.
 - Every solution **must** explicitly support [.NET Framework](https://docs.microsoft.com/en-us/dotnet/framework/) 4.7.2+, [.NET Standard](https://docs.microsoft.com/en-us/dotnet/standard/net-standard) 2.0+, and [.NET Core](https://docs.microsoft.com/en-us/dotnet/core/) 2.1+. A solution may support earlier Framework, Standard, or Core versions, but is not required to do so.  
   - **Exception**: If a solution specifically relates to a platform-specific technology, it need not support .NET Standard or not applicable platforms. Examples include Windows Forms, Windows Presentation Foundation, and Windows Registry for .NET Framework, or the Kestrel web server for .NET Core.

## Code

 - All solutions **should** follow the same naming and general pattern conventions as established in the [dotnet/corefx](https://github.com/dotnet/corefx) project. Specifically, see [Coding Guidelines](https://github.com/dotnet/corefx/tree/master/Documentation#coding-guidelines)
   - Public **and protected** code elements **must** follow the conventions described above, including
     - Parameters are `camelCased`, without prefix     
     - Classes, methods, properties, fields, events, and delegate types are `PascalCased`
     - **Exception**: Constants may be `UPPER_UNDERSCORE` cased
   - Enum names **should** avoid including the suffix `Enum`
   - Non-public member names and body code **may** follow primary or original author preferences. For example
     - Prefixing non-public fields with "m_" (or not)
     - Prefixing non-public static fields with "s_" (or not)
     - Using `this` even when not syntactically necessary, in order to clarify invocation of instance members
   - Non-public member names and body code **should** maintain the conventions established by the primary or original author of a project
   
 - Proposed APIs **must** be written in C#7+, using applicable idioms. 
 - Implementations **should** be  written in C#7+, using applicable idioms.
   - **Exception**: If solutions are proposed that require unsafe code, they may be implemented in C++. solutions specifically meant to augment functional programming in F# may be implemented in F#. Implementations in VB.NET are discouraged but may be considered in some circumstances.

## Tests

 - All projects **must** be fully unit tested with [Xunit](https://xunit.github.io/) before publishing release versions. "Fully unit tested" means every publicly accessible API is invoked at least once from at least on automated unit test. All tests shall pass against net472, netcoreapp2.1, and/or any other specific framework versions targeted by the applicable project. 
   - **Exception**: If automated tests are not feasible (such as for a UI behavior) then clearly defined manual test steps may be substituted.  
 
## Structure

 - All projects **must** be built against the [MSBuild](https://github.com/Microsoft/MSBuild) version included in VS 2017 or later, or any compatible build engine, in order to use the greatly simplified project format and [succinct multitargeting feature](https://blog.nuget.org/20170316/NuGet-now-fully-integrated-into-MSBuild.html#develop-against-multiple-tfms)
 - Each solution **must** be developed in its own repository. The repository structure is illustrated below. If there is only one implementation project, and it is a dll library (not an executable) it should be in the `lib` folder. Additional closely-associated projects (such as a console executable wrapper) should be in appropriately named folders. 
   - Each implementation project **must** have its own unit test project. All results **must** be written (or copied) to the `tests\results` folder.
   - Each library implementation project **must** have its own api project. Command line projects **should** have some documentation of usage in a corresponding "api" project
 - Each library implementation project **should** produce its own NuGet package. The MSBuild / VS 2017 build system automatically produces packages from C# projects, and transforms project dependencies into package dependencies. Working around this system by manually constructing and packing .nuspecs or including multiple assemblies in a single package greatly complicates building, versioning, and distributing, and should be avoided.

### Repository Template

The following illustrates the layout of each solution repository:
 
  - Repository root contains `build.ps1` and `test.ps1` scripts, and optionally an `init.ps1` script. Anyone should be able to build and test all projects within the solution by executing these scripts (optionally requiring init.ps1 to be run after initially cloning the repository)
  - `ref` folder contains any referenced git submodules, including a reference to the `ockham.net` repository itself. This ensures governance, reference, and development documents and utilities are standardized and shared across all solutions
  - `shared` folder contains `_Solution.shproj` Shared Project
     - `AssemblyVersion.csproj` is an MSBuild project file containing version numbers and other properties to be imported into all implementation projects in the solution
     - `deployment` contains deployment scripts for all implementation projects in the solution
  - `api` folder contains an api project for each implementation project in the solution
  - `src` folder contains the implementation projects for the solution
  - `tests` folder contains a unit test project for each implementation project, as well as a `results` folder for aggregating all unit test results

```
  <repo> 
    |- build.ps1
    |- test.ps1
    |- [init.ps1]
    |- ref
    |   \- ockham.net (git submodule)
    |- [docs]
    |- <solution>.sln
    |- shared
    |   |- Shared.shproj
    |   |- assembly
    |   |   \- Properties.csproj
    |   \- deployment
    |       |- lib
    |       |   \- publish.ps1
    |       |- [console]
    |       |   \- publish.ps1
    |       \- [other]
    |           |- publish.ps1
    |           \- some_script.ps1
    |- api
    |   |- lib
    |   |   \- <solution>.Api.csproj
    |   |- [console]
    |   |   \- <solution>.Console.Api.csproj  
    |   \- [other]
    |       \- <solution>.[other].Api.csproj  
    |- src
    |   |- lib
    |   |   \- <solution>.csproj
    |   |- [console]
    |   |   \- <solution>.Console.csproj  
    |   \- [other]
    |       \- <solution>.[other].csproj  
    \- tests
        |- lib
        |  \- <module>.Tests.csproj
        |- [console]
        |   \- <module>.Console.Tests.csproj
        |- [other]
        |   \- <module>.[other].Tests.csproj
        \- results
```