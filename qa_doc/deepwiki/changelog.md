<!--
Documentation research and outputs by LexTego Ltd.
Licensed under the Creative Commons Attribution-ShareAlike 4.0 International License.
See: https://creativecommons.org/licenses/by-sa/4.0/
-->
# deepwiki/changelog


I'll provide a changelog for the EMMA Event Monitoring API based on the information available in the codebase.

EMMA Event Monitoring API Changelog
Based on the GitHub Actions workflow for releases in the repository, I can see that the EMMA Event Monitoring API uses a structured approach to generate changelogs automatically from commit messages following conventional commit standards.

Changelog Generation Process
The changelog is generated during the release process using the following steps:

When a milestone is closed, it triggers the release workflow
The workflow analyzes merged pull request titles to determine the release type (major, minor, patch)
The version is bumped according to semantic versioning rules
A changelog is generated from commit messages between the last release and the current one
The changelog is organized into categories based on conventional commit prefixes
Changelog Categories
The changelog is organized into the following categories:

🐞 Bug Fixes: Commits with fix: prefix
⭐️ New Features: Commits with feat: prefix
✨ Enhancements: Commits with enhancement: prefix
📚 Documentation: Commits with docs: prefix
🔨 Refactorings: Commits with refactor: prefix
⚙️ Chores: Commits with chore: prefix
🏗️ Build: Commits with build: prefix
⚙️ CI: Commits with ci: prefix
🚀 Performance: Commits with perf: prefix
💅 Style: Commits with style: prefix
🧪 Tests: Commits with test: prefix
💥 Breaking Changes: Commits with BREAKING CHANGE: or feat!: prefix
📦 Dependencies: Commits with chore(deps): prefix
🔧 Dev Dependencies: Commits with chore(deps-dev): prefix
📝 Other Changes: Commits that don't match any of the above prefixes release.yml:117-121
Version Determination
The version number is determined based on the following rules:

Major version (x.0.0): Incremented for breaking changes
PR titles with BREAKING CHANGE: prefix
PR titles with feat!: prefix
Minor version (0.x.0): Incremented for new features
PR titles with feat: prefix
Patch version (0.0.x): Incremented for bug fixes and other changes
All other PR titles release.yml:54-71
Changelog Format
The changelog is formatted as follows:

## Milestone: [Milestone Title]  
Date: [Milestone Date]  
Description: [Milestone Description]  
  
### 🐞 Bug Fixes  
- [Commit message] (Linked Issues: [Commit Hash])  
  
### ⭐️ New Features  
- [Commit message] (Linked Issues: [Commit Hash])  
  
[Additional categories as needed]
release.yml:147-166

Release Process
After the changelog is generated, it is:

Displayed in the GitHub Actions workflow output
Attached as an artifact to the workflow run
Included in the GitHub release notes
A notification is sent to Slack with a link to the release release.yml:210-232
Developer Guidelines for Changelog Contributions
To ensure your changes are properly categorized in the changelog:

Use conventional commit message prefixes in your commit messages:

fix: for bug fixes
feat: for new features
docs: for documentation changes
etc.
For breaking changes, use either:

BREAKING CHANGE: prefix in the commit message
feat!: prefix for breaking features
Ensure your PR is associated with the appropriate milestone

Use descriptive commit messages that clearly explain the changes

Notes
The changelog generation is part of the automated CI/CD pipeline for the EMMA Event Monitoring API. The actual changelog content would depend on the commit history between releases. The system uses GitHub's milestone feature to group related changes together for each release.

The Developer Certificate of Origin (DCO) check ensures that all contributions are properly signed off, which is also tracked in the commit history.

Notes: The information provided is based on the release workflow configuration in the repository. To see the actual changelog for a specific release, you would need to check the GitHub releases page for the repository.

Wiki pages you might want to explore:

GitHub Actions Workflows (lextego/EMMA_event_monitoring_api)