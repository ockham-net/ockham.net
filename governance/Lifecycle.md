# Lifecycle

This document describes the lifecycle of proposing and implementing new solutions or changes to existing solutions.

### Terminology

*See [Terminology.md](./Terminology.md)*

## New Solution

 - A new solution should be proposed which solves a clear problem with limited scope. A proposal might include discussions, API code, or even actual implementations to demonstrate the intent and usage. Documents and discussions supporting a proposal should be posted to a publicly accessible location.
 - To formally complete the proposal, a pull request should be submitted adding the proposed new solution to the list in the `/docs/Solutions.md` file in the `ockham.net` repository. This is treated as an API change, so a **simple majority** of Maintainers must approve the request.
 - Once the proposal has been approved, any Maintainer can create a new repository for the solution. The repository contents should be initialized using the solution template, and then checked in as the initial commit to the `master` branch of the solution's repository.
 - A maintainer then immediately creates release candidate branch `rc-1-0`.
 - To begin building the solution proceed to "Adding APIs"

## Existing Solution (new release candidate)

 - Either breaking or non-breaking changes may be proposed to an existing solutions. A breaking change is anything that alters the behavior of an existing public API or protected API that users are able to invoke or override in derived classes. 
 - Similar to a new solution, discussions and supporting documents should be provided and posted to a publicly accessible location.
 - To formally complete the proposal, a pull request should be submitted which updates the current release candidate version number for the applicable solution in the `/docs/Solutions.md` file in the `ockham.net` repository. This is treated as an API change, so a **simple majority** of Maintainers must approve the request.
 - Non-breaking changes require the minor version number to be incremented by one, while any breaking changes require incrementing the major version by one.
 - Once the proposal has been approved, any Maintainer can create the new release candidate branch with the applicable version number (e.g. `rc-1-1` or `rc-2-0`)

## Adding APIs

Adding APIs **must** follow a two-step process:

### Proposing the API itself
First, the API itself is proposed in a pull request to the current release candidate branch of the applicable solution's repository. API changes constitute adding or updating C# files in the applicable API project. API files should include all **public** and **protected** classes and members. Method bodies and read-only properties should contain the single statement `throw null;`. This request **must** be approved by a **simple majority** of current Maintainers. API change pull requests **must** only contain API changes. Additional API changes may be proposed at any point during the lifetime of a release candidate branch. API changes during work on a release candidate branch may include breaking changes provided the breaking change does not affect any released package version.

#### protected members

Members declared with the `protected` keyword still constitute part of the public API of a solution, because they are invokable by any consuming projects which include applicable derived classes. If a developer wishes to use a `protected` member as an implementation detail, that member should be declared `internal protected`, or the containing class should be `sealed`, or both.  

### Implementing APIs
Once approved, APIs can be incrementally implemented by anyone:

1. A work item should be created with a description of what the developer intends to implement
2. A branch should be created from the current release candidate branch, and the work item should be associated with it
3. The developer(s) can check in changes to the work item branch at will
4. At any time, the developer(s) can submit a pull request to merge a work item branch back into the current release candidate branch. These pull requests may be approved by any Maintainer (only one approval is required), but Maintainers may not approve their own pull requests except for bug fixes and documentation-only updates (see Rules.md for more information). To be accepted, the changes in the pull request **must** include passing unit tests that cover any new or updated implementations. At this point the complete API comparison test may still be failing (because not all approved APIs are implemented), but the pull request must not contain changes to the API itself.

### Squash Merging
To keep the commit history of a solution manageable, feature branches should be squash-merged into release candidate branches. Likewise, release candidate branches should be squash-merged into the master branch.

## Distributing pre-release packages
A Maintainer may package and distribute a **pre-release** package from a release candidate branch at any time provided **all** APIs currently in the branch are implemented with passing unit tests. The package version should be the release candidate version with a 0 build element and the suffix `rc##`, where the two digits start at 01 and are incremented by one every time the a new pre-release package is distributed. For example, a release candidate 3.2 of a solution might distribute pre-release package versions `3.2.0-rc01`, `3.2.0-rc02`, etc.

## Distributing release packages
At any point when all APIs in a release candidate branch are implemented with passing unit tests, a Contributor or Maintainer may submit a pull request to merge a release candidate back in to the master branch. Only one Maintainer approval is required, not including the submitter. Once approved, the release candidate branch should be deleted, and a Maintainer should package and distribute a release version package matching the release candidate number, with a 0 build element. Any future changes to the API require creating a new release candidate, incrementing the major or minor version by 1. 

## Preserving major releases
Whenever a new major version is released, the existing major version should first be branched into a `release-#` branch, where the number is the major release number. This preserves past major releases so that bugfixes can be applied as needed.

# Bug fixes
If a bug is discovered in a **production (release)** package: 

1. A bug work item should be created with a complete description
2. If the bug is present in the current major release, the bugfix branch should be created off of the master branch. If the bug is present only in past major release, OR requires a different fix in a previous major release, a corresponding bugfix branch should be created off the applicable major release branch.
3. If at all possible, a unit test should be created or updated which reproduces the bug
4. The bug should be fixed, and a corresponding pull request submitted
5. A Maintainer should promptly review and accept the request, provided all unit tests are still passing, and there is evidence that the reported bug has been fixed.
6. A Maintainer should promptly build and release a package including the bugfix, incrementing the release's build number by 1.
7. If the bug affects multiple major releases, and the same bugfix commit can be applied to multiple release branches, a Maintainer should create applicable pull requests to merge the change into all applicable past release branches, and should build and distribute packages as in step 6 for each applicable release branch.

# Documentation changes
Documentation source should be included in the solution contents. Documentation source may include markdown files, text files, proprietary formats, XML documentation comments embedded in .NET code files, or other materials. Documentation updates are treated similar to bug fixes, but without the need for a work item or unit tests:

 - A current release branch is not required
 - Maintainers **may** approve their own pull request provided the changes are to documentation only (including documentation comments embedded in source code files)
 - If the update requires a new package version (to include updated documentation xml files), the build number should be incremented by 1

# Experimental Branches
Maintainers, Contributors, or other developers may wish to experiment with possible changes to a solution before formally proposing that changes be made. Anyone is welcome to clone a solution repository, or create an expiremental branch within a repository. Experimental branches in the solution repository itself should be clearly marked with the prefix `exp-`. There are no restrictions for modifications to experimental branches. Experimental branches should not be directly merged back into the main branch structure of a solution.

Experimental packages may also be built and distributed, but they **must** include the version suffix `-exp-[initials]-[#]`, where `initials` are the initials of the primary developer. The version numbers should be the same as the version from which the expiriment was originally branched. For example, developer Suzy Ford might branch an experiment off of the master branch, where the current releases version is `2.12.6`, and publish packages `2.12.6-exp-sf-1`, `2.12.6-exp-sf-2`, etc.