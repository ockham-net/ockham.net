# Rules
 
### Terminology

*See [Terminology.md](./Terminology.md)*

## Summary

 - All activity within the Ockham.NET project shall follow the Rules, Principles, and Conventions described in the documents located in the `governance` folder
 - **Changes to Rules, Principles, or Conventions** require a **super majority** vote of current Maintainers
 - **Changes to the API** require a **simple majority** vote of current Maintainers
 - **Implementations** of approved APIs require the approval of **one** Maintainer, **not including the submitter**
    - Exception: **Bug fixes** may be approved by the submitter if the submitter is a Maintainer
    - Exception: **Documentation only changes** may be approved by the submitter if the submitter is a Maintainer
 - **Changes to tools and templates** in the `ockham.net` repository itself must be approved by a **simple majority** vote of current maintainers

## 1. Contents and Changes

### 1.1. Contents

 - The Rules consist of the contents of this document
 - Principles and Conventions consist of the contents of the `governance` folder besides this document

### 1.2. Scope

 - All activity within the Ockham.NET project shall follow the Rules, Principles, and Conventions

### 1.3. Changes

 - Changes can be submitted only by Maintainers
 - Changes to the Rules, Principles, or Conventions shall be proposed by submitting a pull request with changes to this or other documents in the `governance` folder. 
 - Changes to the Rules, Principles, or Conventions require **super majority** approval of the list of Maintainers at the time the pull request was submitted.

## 2. Team

### 2.1. Maintainers

 - Maintainers are the people who direct the Ockham.NET by voting on which solutions and APIs should be included, fostering an environment in accordance with the Code of Conduct, and ensuring code and documentation meets agreed upon standards and conventions
 - The list of Maintainers is documented in the Team.md document 
 - Only Maintainers may:
   - Submit proposed changes to rules and conventions
   - Approve pull requests
   - Vote to include or remove Maintainers or Contributors

#### 2.1.1 Expectations of Maintainers

 - Maintainers are both individually and collectively responsible for guiding the direction of the project and ensuring the quality of code incorporated into any particular solution
 - Maintainers should only approve a pull request if they have reviewed the changes in detail and have judged that the submitted code or other content meets the expectations and conventions described in this and associated governance documents
 - Maintainers should provide helpful and encouraging feedback when rejecting pull requests 
 - Maintainers should participate promptly and regularly in at least one of: voting on rules changes, voting on API changes, reviewing implementation pull requests, providing bug fixes, or authoring documentation

#### 2.1.2 Self-Approvals

 - To aid prompt responses to bugfixes, Maintainers **may** approve their own bug fix pull requests
 - To reduce barriers to building or improving documentation, Maintainers **may** approve their own pull requests for documentation-only changes
 - Including anything other than a bug fix OR documentation update in a self-approved change will be considered a serious breach of these rules

#### 2.1.3 Becoming a Maintainer

 - Anyone may request to become a Maintainer. Adding to the list of Maintainers is treated like a change to the Rules and Conventions, and so requires a super majority vote of current Maintainers
 - Proposed maintainers must:
   - Submit the request themselves 
   - Be regularly involved in writing, debugging, or maintaining .NET code deployed in a production environment   

#### 2.1.4 Removing a Maintainer

 - Any Maintainer may choose to stop being a Maintainer at any time by simply submitting and self-approving a pull request removing their name from the list of Maintainers. The Maintainer may add themselves to the list of Contributors in the same self-approved pull request.
 - Any Maintainer may be removed from the list of Maintainers by a **super majority** vote of the **other** Maintainers. This should only be done for one or more of the following reasons:
   - Actions or communications contrary to the Code of Conduct
   - Self-approving a pull request with anything other than a bug fix OR a documentation update
   - Repeatedly self-approving bugfixes that substantially depart from the agreed upon conventions and standards 
   - Approving other's pull requests without adequately ensuring that the submitted changes conform to the agreed upon conventions and standards 
   - Consistent lack of participation in at least one of the activities noted in 2.1.1
 - Maintainers removed for lack of participation only may request to become Contributors at any time
 
### 2.2. Contributors
 
 - Contributors are people in addition to the Maintainers who submit proposed API changes, implementations, bugfixes, and documentation
 - The list of Contributors is documented in the Team.md document

#### 2.2.1 Expectations of Contributors

 - Contributors may participate at whatever level of activity or frequency they desire
 - Contributors must act and communicate in accordance with the Code of Conduct
 - Contributors may submit pull requests for API changes, implementations, documentation, or bug fixes

#### 2.2.2 Becoming a Contributor

 - Anyone may request to become a Contributor. Adding to the list of Contributors requires approval of two current Maintainers  
 - Proposed Contributors must submit the request themselves

#### 2.2.3 Removing a Contributor

 - Any Contributor may choose to stop being a Contributor at any time by simply submitting a pull request removing their name from the list of Contributors
 - Any Contributor may be removed from the list of Contributors by a vote of three Maintainers. This should only be done in response to the following actions on the part of the Contributor being removed:
   - Actions or communications contrary to the Code of Conduct 
   - Prolonged and consistent submission of pull requests that fail to meet agreed upon standards and conventions
 
## 3. The API

 - Changes can be submitted only by Maintainers or Contributors
 - Changes to the API shall be proposed by submitting a pull request including changes to the applicable API project
 - Changes to the API require a simple majority vote of current Maintainers
 - The API of a solution, including any proposed changes, shall be documented in the form of valid C# 7+ code, but with `throw null;` in the place of any method implementations.

### 3.1. Principles and Conventions

 - All proposed API changes shall conform to the Principles and Conventions of the project

### 3.2. Implementation

 - Any submitted pull requests for API implementations must include passing unit tests that cover the implementations being added or changed

### 3.3. Branching and merging

 - Changes to the master branch shall only be pulled from a release candidate branch (for API implementations), or from a bugfix branch
 - Changes to a release candidate branch shall only be pulled from a clearly scoped feature or bugfix branch

### 3.4. Publishing

 - Pull requests for merging release candidate branches into the master branch must include XML documentation comments for all publicly visible members
 - Prerelease packages shall be published only by Maintainers, built from unmodified code cloned from a release candidate branch
 - Release packages shall be published only by Maintainers, built from unmodified code cloned from the master branch or from a previous major release branch
 - Release packages shall not be published unless there is documentation of all publicly visible members published online