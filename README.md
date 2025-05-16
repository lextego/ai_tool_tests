# AI Tool Review for Codebase Documentation

## Introduction

This evaluation initially drew from the excellent open-source listing at [landscape.ainativedev.io](https://landscape.ainativedev.io), a curated collection of AI-native development tools. As our research progressed, we expanded the list to include additional tools not originally featured, particularly those demonstrating unique value for internal documentation and support workflows. If you have not seen the AI Native Dev Con YouTubes, they are also worth checking out at [You Tube](https://youtube.com/playlist?list=PLISstAySqk7Lt1qUF0qWS2F15qBNesyzU)

As part of ongoing efforts to maintain comprehensive and accessible documentation for the evolving Tazama.org platform, we tested a range of AI tools aimed at helping automate and improve codebase documentation. The goal was to reduce the burden on developers while ensuring support teams and implementers had up-to-date, relevant information.

The evaluation was grounded in real-world needs, including:

* Developer onboarding and familiarization
* Internal technical support and root cause analysis
* Broader implementation and stakeholder understanding

This document provides a narrative review of each tool tested. Where possible, we've described what each tool is best suited for, without scoring or ranking. Subjective impressions are included, but framed around practical outcomes.

## DeepWiki

**Overview:** DeepWiki focuses on open-source repositories, offering fast documentation generation and ongoing updates. Full documentation for this evaluation can be browsed directly at [deepwiki.com/lextego/EMMA\_event\_monitoring\_api](https://deepwiki.com/lextego/EMMA_event_monitoring_api). DeepWiki focuses on open-source repositories, offering fast documentation generation and ongoing updates.

**Strengths:**

* Produced an instant overview and system architecture pages
* Included flow diagrams, sequence diagrams, and API documents
* Created a useful glossary and inline environment configuration comments

**Best for:** Developer documentation and architectural summaries

**Artifacts:** (Some outputs are unedited screenshots due to copy/export limitations)

* [API Documentation](./deepwiki/api_doc.md)
* [Changelog](./deepwiki/changelog.md)
* [Glossary of Terms](./deepwiki/glossary_of_terms.md)
* [Process Flow (Markdown)](./deepwiki/processflow.md)
* [Sequence Diagram (Markdown)](./deepwiki/sequence_diagram.md)
* Process Flow Diagrams:  …&#x20;
* [Sequence Diagram Image](./deepwiki/sequence_diagram.jpg)

---

## Dosu.dev

**Overview:** Markets itself as an auto-documentation platform that learns as you build.

**Experience:** Despite indexing our repo, the tool failed to generate any meaningful documentation.

**Best for:** Potentially useful for developer Q\&A over time, but not for initial documentation needs.

---

## Catio.tech

**Overview:** Describes itself as an AI assistant for tech architecture.

**Experience:** Early access only – no interaction or documentation available at time of testing.

---

## DevDocs.io

**Overview:** A comprehensive library of existing API docs.

**Best for:** Quick API reference, not documentation creation.

---

## Doctave.com

**Overview:** Documentation site generator with an AI angle.

**Experience:** No AI-generated output identified during use; primarily a static documentation generator.

---

## Driver.ai

**Overview:** Promises automated documentation generation.

**Experience:** Signup process required a demo request – no trial available.

---

## Dyad.sh

**Overview:** An open-source tool with local execution and LLM connectivity.

**Experience:** Requires technical setup and user guidance through prompts; limited by token quotas.

---

## Firstmate.io

**Overview:** AI tool for making knowledge accessible across an org.

**Experience:** Still in waitlist stage – no access during review period.

---

## GitBook

**Overview:** Popular documentation platform with some AI support.

**Experience:** Setup was smooth, but no documentation was generated from the connected repo.

---

## GitDiagram.com

**Overview:** Tool for turning GitHub repos into visual diagrams.

**Artifacts:**

* [Architecture Diagram](./gitdiagram/diagram.md)

---

## GitHubGG

**Overview:** Fast, interactive documentation generation from GitHub repos.

**Strengths:**

* Created a comprehensive documentation suite

**Artifacts:**

* [README](./githubgg/README.md)
* [API Documentation](./githubgg/api_doc.md)
* [Architecture](./githubgg/architecture.md)
* [Changelog](./githubgg/changelog.md)
* [Glossary](./githubgg/glossary_of_terms.md)
* [Inline Comments](./githubgg/inline_comments.md)
* [Process Flow](./githubgg/process_flow.md)
* [Sequence Diagram](./githubgg/sequence.md)
* [Summary](./githubgg/summary.md)

---

## GitHub.me.uk

**Overview:** Similar to GitHubGG but hosted on a different platform.

**Artifacts:**

* [README](./githubme/README.md)
* [API Documentation](./githubme/api_doc.md)
* [Glossary](./githubme/glossary.md)
* [Summary](./githubme/summary.md)
* [Additional Comments](./githubme/comments_to_files.md)
* [Other Output](./githubme/output.md)

---

## Joggr.io

**Overview:** CLI-first, dev-centric AI documentation tool.

**Strengths:**

* Produced a full set of developer documentation

**Artifacts:**

* [README](./joggr/README.md)
* [API Documentation](./joggr/api-documentation.md)
* [Changelog](./joggr/change-log.md)
* [Glossary](./joggr/glossary-of-terms.md)
* [Inline Comments](./joggr/inline-comments.md)
* [Process Flow](./joggr/process-flow.md)
* [Sequence Diagram (raw)](./joggr/sequence.md)
* [Sequence Diagram](./joggr/sequence-diagram.md)
* [Summary](./joggr/summary-of-the-code-base.md)

---

## Komment.ai

**Overview:** Wiki-style auto-documentation and insights engine.

**Artifacts:**

* [README](./komment_ai/README.md)
* [API Diagram](./komment_ai/api01.jpg)
* [Other Output](./komment_ai/other.md)

---

## Mintlify.com

**Overview:** AI-native documentation generator.

**Experience:** Encountered setup errors and repo access issues. No documentation was produced.

---

## ReadMe.com

**Overview:** API documentation platform with AI suggestions.

**Best for:** Hosting and presenting OpenAPI specs, not full codebase docs.

---

## Swark (VSCode extension)

**Overview:** Diagram generation for GitHub repos inside VSCode

**Artifacts:**

* [Architecture Diagram](./swark/2025-04-17__15-07-30__diagram.md)

---

## Swimm.io

**Overview:** AI-powered docs generation tool with focus on legacy and mainframe systems.

**Experience:** Not tested due to niche positioning.

---

## Additional Tool Testing

As we continue exploring the landscape of AI tools for documentation, future updates will include additional tools, deeper integration evaluations, and expanded use cases. This repository will evolve as we test new platforms and incorporate feedback from the community. Stay tuned for:

* Tools supporting multilingual documentation
* LLM-integrated IDE extensions
* QA scoring for accessibility and formatting compliance

We welcome contributions or suggestions for tools to test.

---

## Licensing and Attribution

This work is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/). You are free to share and adapt the material, provided that you give appropriate credit. Please attribute as follows:

> Documentation research and outputs by **LexTego Ltd**, available under CC BY 4.0.

We encourage contributions and comparisons, and welcome any pull requests that help improve or extend the testing methodology.

---

## Summary & Next Steps

Many of the tools tested are promising – especially for developer audiences. GitHubGG, Joggr, and DeepWiki stood out for generating high-quality markdown, diagrams, and summaries with little effort. Others may be better suited for API-centric workflows or internal knowledge-sharing platforms.

All relevant outputs have been included in this repository under their respective tool folders. Contributions and comparisons are welcome.

(c) LexTego Ltd 2021–2025
