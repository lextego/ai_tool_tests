
## What are we testing

We have the following requirements for testing tools that provide documentation:

**Markdown Documentation Creation**

- Can the tool **create Markdown documentation** for products we work with?
- Can it ensure the documentation is written in **International (UK) English**?
- Does it support **templates or style guidelines** for consistent formatting?

**Why**: Clear, standardised documentation improves accessibility, professionalism, and global usability.

**Mermaid Diagram Generation**

- Can it assist in **creating Mermaid diagrams** directly from code, pseudocode, or prompts?
- Does it support the generation of the following diagram types:
  - **Git Flows**
  - **Sequence Diagrams**
  - **Flow Charts**
- Can it **integrate diagrams into Markdown or documentation platforms** easily?

**Why**: Visual diagrams improve comprehension of workflows, system interactions, and development processes, especially for complex projects.

**API Documentation Generation**

- If you're building APIs, does it support **auto-generating OpenAPI/Swagger specs**?
- Can it **document REST endpoints, GraphQL queries, or WebSocket flows**?

**Why**: Saves a huge amount of time for backend/frontend integration and third-party use.

**Changelog Management**

- Can it help **generate changelogs** automatically from Git commit history or pull requests?
- Can it **format them nicely** (e.g., by semantic versioning, features/fixes)?

**Why**: It helps a lot with release management and user-facing documentation.

**Code Annotation / Inline Comments**

- Can the tool **suggest or auto-generate inline comments** for your code?
- Can it follow **your team's commenting standards** (e.g., docstrings, Javadoc, Sphinx style)?
- Does it understand **function, class, and module-level summaries**?

**Why**: Good documentation isn't just external – clear internal commenting keeps your codebase maintainable.

**Versioned Documentation**

- Can it help you **version your documentation** alongside your code?
- Support for things like **MkDocs + MkDocs-Material** with versioning plugins?

**Why**: Critical when maintaining multiple release tracks.

**Architecture / System Diagrams**

- Beyond Git flows and basic sequences, can it assist in generating **high-level system architecture diagrams**?
  - Microservices architecture
  - Data flows
  - Infrastructure (AWS, Azure, on-prem)

**Why**: These diagrams are gold for onboarding new developers and aligning stakeholders.

**Glossary / Domain Knowledge Extraction**

- Can the AI help **extract key terms, domain concepts, abbreviations, and definitions**?
- Can it **auto-suggest glossary entries** from the codebase or tickets?

**Why**: Especially valuable for complex or specialised domains.

**Codebase Summarisation**

- Can it generate **project overviews** or **module summaries**?
- For example: "This module handles authentication and includes login, logout, and session management."

**Why**: Helps new developers (and you six months later!) quickly understand scope and intent.

**Linkage Between Code and Documentation**

- Does the tool **embed links between code sections and generated documentation**?
- For example, you click a function name in the docs and it takes you straight to the code repo.

**Why**: Smooths the navigation between code and documentation.

**Compliance and Formatting Standards**

- Can it check if documentation complies with your **style guides** (e.g., consistent tone, UK English spelling)?
- Does it support **custom templates** for consistency?

**Why**: Consistency builds professionalism and trust in internal and external documents.

## Where are we testing

We will do our testing against Tazama's TMS Repository. As a lot of the tools need to have repo access, we created a fork of the repo before testing - and gave access to that. It has 79 files across 14 folders, so it is also not a massive repository. The test will only use the free services, knowing this will hit some limitations at some points, but hopefully not too soon that we are not able to asssess the tools properly. The repository is here if you want to check it out and do your own testing :-)

## Which tools did we test with

| Name                                                           | tested |
| -------------------------------------------------------------- | ------ |
| [Dosu.dev](https://dosu.dev)                                   | [x]    |
| [catio.tech](https://catio.tech)                               | [x]    |
| [DevIn / DeepWiki](https://deepwiki.com/)                      | [x]    |
| [devdocs.io](https://devdocs.io)                               | [x]    |
| [doctave.com](https://doctave.com)                             | [x]    |
| [driver.ai](https://driver.ai)                                 | [x]    |
| [dyad.sh](https://dyad.sh)                                     | [x]    |
| [firstmate.io](https://firstmate.io)                           | [x]    |
| [gitbook.com](https://gitbook.com)                             | [x]    |
| [GitDiagram.com](https://gitdiagram.com/)                      | [x]    |
| [github.gg](https://github.gg)                                 | [x]    |
| [github.me.uk](https://github.me.uk)                           | [x]    |
| [Joggr.io](https://www.joggr.io/)                              | [x]    |
| [komment.ai](https://komment.ai)                               | [x]    |
| [mintlify.com](https://mintlify.com)                           | [x]    |
| [readme.com](https://readme.com)                               | [x]    |
| [github.com/swark-io/swark](https://github.com/swark-io/swark) | [x]    |
| [swimm.io](https://swimm.io)                                   | [x]    |