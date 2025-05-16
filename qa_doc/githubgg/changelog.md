<!--
Documentation research and outputs by LexTego Ltd.
Licensed under the Creative Commons Attribution-ShareAlike 4.0 International License.
See: https://creativecommons.org/licenses/by-sa/4.0/
-->
# v1.3.0 (Unreleased)

## ✨ Features

* **Security Scanning**: Implemented multiple security scanning workflows to enhance code security:
  * **Codacy Security Scan**: Integrated Codacy for static code analysis and security vulnerability detection.
  * **CodeQL**: Added GitHub CodeQL for code analysis and vulnerability scanning.
  * **njsscan**: Integrated njsscan for Node.js security scanning.
  * **tfsec**: Implemented tfsec for Terraform security scanning.
  * **Hadolint**: Added Hadolint for Dockerfile linting and best practice checks.
  * **OpenSSF Scorecard**: Integrated OpenSSF Scorecard for supply chain security assessment.
  * **Anchore Syft SBOM Scan**: Implemented Anchore Syft to generate Software Bill of Materials (SBOM) for both source code and Docker images, enhancing supply chain transparency.
  * **Dependency Review**: Added Dependency Review workflow to scan dependency changes in pull requests for known vulnerabilities.
* **Code Quality and Compliance**:
  * **Conventional Commit Validation**: Implemented a workflow to validate pull request titles against conventional commit standards, improving commit message consistency and automation.
  * **DCO Check**: Added Developer Certificate of Origin (DCO) check workflow to ensure commit sign-offs, enforcing contribution compliance.
  * **GPG Commit Verification**: Implemented GPG commit signature verification workflow for enhanced commit authenticity and security.
* **Release Management**:
  * **Milestone Workflow**: Introduced a workflow to automate milestone closing and trigger release processes.
  * **Release Workflow**: Implemented a comprehensive release workflow including version bumping, changelog generation, and GitHub release creation.
  * **Docker Hub Image Publishing**: Added workflow to automatically build and publish Docker images to Docker Hub on `main` branch pushes.
* **Performance Monitoring**:
  * **Benchmark CI**: Implemented a Benchmark CI workflow to track and monitor performance metrics over time.
* **Dependency Management**:
  * **Dependabot Configuration**: Configured Dependabot to automatically update npm dependencies weekly, ensuring dependencies are kept up-to-date.

## 🛠️ Improvements

* **Enhanced CI/CD Pipeline**: Significantly expanded the CI/CD pipeline with numerous dedicated workflows for security, code quality, compliance, and release management.
* **Improved Security Posture**: Greatly enhanced the service's security posture through the integration of multiple security scanning tools and verification workflows.
* **Code Maintainability**: Improved code maintainability and consistency by enforcing code formatting with Prettier and linting with ESLint, as well as conventional commit messages.
* **Supply Chain Security**: Strengthened supply chain security through SBOM generation and dependency review processes.
* **Release Automation**: Automated the release process, including versioning, changelog generation, and Docker image publishing, streamlining releases and reducing manual effort.
* **Documentation**: Updated `README.md` to provide more detailed information about the service, including sequence and activity diagrams, and sample request bodies.

## ⚙️ Infrastructure

* **Kubernetes Deployment**: Updated Kubernetes deployment and service configurations (`deployment.yaml`, `service.yaml`).
* **Docker Compose**: Updated `docker-compose.yaml` for local development environment.
* **Test Infrastructure**: Enhanced testing setup with `cluster-setup.ts` and updated Jest configurations (`jest.config.ts`).

## 📦 Dependencies

* Updated various dependencies (refer to `package.json` for specific version changes).

**Note:** This changelog is based on the provided files and assumes a comparison to a previous version of the project. Specific bug fixes or more granular details would require a deeper code diff analysis and context of changes made.
