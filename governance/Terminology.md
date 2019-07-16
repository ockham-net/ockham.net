### Terminology

#### Requirements

 - **must** is an absolute requirement, unless exceptions are explicitly noted
 - **should** is a strong suggestion, but exceptions may be considered
 - **may** highlights places where a variety of choices are all acceptable

#### Governance

 - **simple majority** means more than 50% yes votes out of possible votes. No votes and abstentions are treated the same. Exactly 50% is **not** a simple majority.
 - **super majority** means at least 75% yes votes out of possible votes. No votes and abstentions are treated the same. Exactly 75% **is** a super majority.

#### Code Units

 - **solution** is a collection of projects developed as a unit. Usually there is only one implementation project per solution, but in some circumstances there could be more than one, such as a code library along with a console application that exposes much of the code API to command line environments. A solution also has one actual Visual Studio .sln file.
 - **project** is a `dotnet` project
   - *Note*: In some contexts, "the Ockham project" or "the project" refers to the Ockham.NET initiative as a whole
 - **package** is a NuGet package 
 - **implementation project** is a `dotnet` project with the actual implementation code
 - **api project** is a `dotnet` project with a compilable API, but without method bodies (bodies contain the single statement `throw null;`)
 - **test project** is a `dotnet` Xunit unit test project.
