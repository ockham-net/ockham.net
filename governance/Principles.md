# Principles

## Project Purpose

The Ockham.NET project aims to promote quality, consistency, and supportability in .NET-based projects throughout by building, maintaining, and promoting a coherent set of standards and libraries for accomplishing common tasks in .NET programs. 

## Project Principles

These principles describe **how we work**. Everything else follows from this.

  - **Everyone is welcome**  
  
     We follow the [Contributor Covenant](https://www.contributor-covenant.org/) [Code of Conduct](https://www.contributor-covenant.org/version/1/4/code-of-conduct.md). Respect and positivity are absolute requirements for Maintainers and Contributors. 

  - **Everyone is equal** 
  
     We make decisions by voting. There is no [BDFL](https://en.wikipedia.org/wiki/Benevolent_dictator_for_life) here.

  - **Quality is king** 
  
     Our commitment to quality, consistency, and supportability starts with any code that we ourselves produce. Ensuring quality will always take priority over rushing to release.

  - **We support our code** 
     
      We treat any published release packages as production components. If users identify bugs, we fix them promptly.

## Development Principles

These principles describe **how we code**. They support our Project Principles. Specific coding guidelines and rules for API changes are described in detail elsewhere.

  - **Everything is tested**

     We don't *think* it works. We *know* it works, and have the records to prove it. 

  - **Coding style is consistent** 

     Reading our code feels familiar, because all of our code follows the same conventions, and those conventions are based on widely adopted best practices and conventions agreed upon by the Maintainers, not an author's own tastes.

  - **Everything is documented**

     All public APIs shall have both inline documentation comments (for Intellisense and Object Browser support) and published online documentation.

  - **APIs are obvious** 

     Although we document our APIs, most users shouldn't have to check the documentation to intuit what an API is for, in general.
     
  - **Packages are small and decoupled**

     Ockham.NET is one project, but it produces many small libraries. We strive to avoid dependencies between our libraries, while also avoiding solving the same problem in multiple places. 

  - **Published packages strictly follow [semver 2.0](https://semver.org/) conventions**

     Our package IDs and versions are a contract. We guarantee them per semver 2.0 conventions. This means:
      - Release packages have exactly three version elements ([major].[minor].[build])
      - Build element is only incremented for bugfixes that make no changes to the API
      - Minor elements is incremented for any non-breaking changes to the API
      - Major element is incremented for any breaking changes to the API

  - **We defer to the .NET Standard, the Base Class Library, and well-established open source projects** 
  
     We don't reinvent the wheel, even if ours is a little bit rounder. 
     - *Note* What constitutes "well-established" will always be a matter of debate as specific situations arise. One of the roles of the Maintainers is to make such judgements.

  