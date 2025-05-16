<!--
Documentation research and outputs by LexTego Ltd.
Licensed under the Creative Commons Attribution-ShareAlike 4.0 International License.
See: https://creativecommons.org/licenses/by-sa/4.0/
-->
## Glossary of Terms

**Anchore Syft:** An open-source tool used for generating Software Bill of Materials (SBOMs) from container images and filesystems. It helps in understanding the components within software.

**ArangoDB:** A NoSQL database used in this project, likely for storing transaction history, relationships between entities, and other relevant data for transaction monitoring.

**Cache (Valkey/Redis):** An in-memory data store used for caching frequently accessed transaction data to improve performance and reduce database load. Valkey and Redis are both mentioned as potential cache technologies.

**ClrSysMmbId (Clearing System Member ID):** An identifier for a participant within a financial clearing system. It helps identify the financial institution involved in a transaction within a specific clearing network.

**Codacy:** A platform used for code quality and security analysis. In this project, it's used to perform security scans and integrate the results with GitHub Advanced Security.

**CodeQL:** GitHub's semantic code analysis engine. It's used to perform deep code analysis for security vulnerabilities and code quality issues.

**ContainerPort:** In the context of Kubernetes deployments, this refers to the port exposed by a container within a pod, making the application accessible.

**Conventional Commits:** A specification for structuring commit messages in a standardized format. This helps automate changelog generation and improve the readability of commit history.

**Ccy (Currency code):** A standardized code representing a specific currency, such as USD for US Dollar or EUR for Euro.

**CreDtTm (Creation Date Time):**  A timestamp indicating when a message or transaction was created.

**ClusterIP:** A Kubernetes Service type that exposes the service on an internal IP address within the cluster. This makes the service accessible to other applications within the same Kubernetes cluster.

**DCO (Developer Certificate of Origin):** A declaration included in commits, certifying that the contributor has the right to submit the code under the project's license. It ensures code provenance and legal compliance.

**Dependabot:** A GitHub service that automatically creates pull requests to update dependencies in a repository, helping to keep projects secure and up-to-date.

**Deployment:** In Kubernetes, a Deployment is an object that manages stateless applications. It ensures a specified number of replicas are running and handles updates and rollbacks.

**Dependency Review:** A GitHub feature and action that scans pull requests for known vulnerabilities in project dependencies, enhancing supply chain security.

**Docker Hub:** A cloud-based registry service for Docker images. It's used to store and distribute container images.

**Docker Compose:** A tool for defining and running multi-container Docker applications. It simplifies the setup and management of complex application environments locally.

**EndToEndId (End-to-End Identifier):** A unique identifier that tracks a transaction throughout its entire lifecycle, from initiation to completion, across different systems.

**Entity:** In the context of this service, an Entity represents a party involved in a transaction, such as a person or organization (Debtor or Creditor).

**Event-Director (ED):** An external service that the Transaction Monitoring Service (TMS) interacts with. It likely handles the routing, processing, or further actioning of transaction events after they are monitored by TMS.

**GitHub Actions:** GitHub's platform for automating workflows directly within repositories. It's used here for CI/CD, security scanning, and other automation tasks.

**GPG Verify (GPG Signature Verification):** The process of verifying commits using GPG (GNU Privacy Guard) signatures. This ensures the authenticity and integrity of commits, confirming they were made by the claimed author.

**Hadolint:** A linter specifically designed for Dockerfiles. It helps enforce best practices and identify potential issues in Dockerfile configurations.

**InstdAmt (Instructed Amount):** The original amount specified in a transaction instruction to be transferred, before any potential deductions or exchange rate conversions.

**IntrBkSttlmAmt (Interbank Settlement Amount):** The actual amount settled between financial institutions during a transaction, which might differ slightly from the instructed amount due to fees or exchange rates.

**ISO 20022:** An international standard for financial messaging. It defines a common platform and methodology for the development of financial messages, promoting interoperability and efficiency.

**Kubernetes:** An open-source system for automating deployment, scaling, and management of containerized applications. It's used to orchestrate and manage the Transaction Monitoring Service in a containerized environment.

**Milestone:** In project management, a milestone is a significant point or checkpoint in a project timeline, often marking the completion of a major phase or deliverable.

**MmbId (Member ID):** A general identifier for a member or participant, often used within financial systems or networks.

**MP2P (Mobile Person-to-Person):** A type of payment transaction where funds are transferred between individuals using mobile devices.

**MSISDN (Mobile Station International Subscriber Directory Number):** Commonly known as a mobile phone number. In financial transactions, it can be used as an account identifier.

**Namespace:** In Kubernetes, namespaces provide a way to logically partition a cluster, allowing for resource isolation and organization among different teams or projects.

**NATS:** A high-performance, open-source messaging system used for building distributed systems. In this project, it likely facilitates communication between the Transaction Monitoring Service and other services like Event-Director.

**njsscan:** A static security code scanner specifically for Node.js applications. It helps identify potential security vulnerabilities in JavaScript and TypeScript codebases.

**Pacs.002 (Payment Status Message):** An ISO 20022 message type used to report the status of a payment transaction between financial institutions.

**Pacs.008 (Customer Credit Transfer Message):** An ISO 20022 message type used for initiating credit transfers between financial institutions on behalf of customers.

**Pain.001 (Customer Credit Transfer Initiation Message):** An ISO 20022 message type used by a customer to initiate a credit transfer, instructing their bank to move funds to a beneficiary.

**Pain.013 (Creditor Payment Activation Request):** An ISO 20022 message type used by a creditor to request payment from a debtor, often used in direct debit scenarios.

**PmtInfId (Payment Information Identifier):** A unique identifier for a block of payment instructions within a financial message, grouping related transactions.

**Prettier:** A code formatter that enforces consistent code style automatically. It helps maintain code readability and reduces stylistic debates in development.

**Protobuf (Protocol Buffers):** A language-neutral, platform-neutral, extensible mechanism for serializing structured data, often used for efficient data exchange and storage.

**Prtry (Proprietary):** Indicates that a code, scheme, or identifier is not part of a standard and is specific or custom to a particular system or organization.

**Replica:** In Kubernetes, a replica represents an instance of a Pod in a Deployment. Deployments manage replicas to ensure application availability and scalability.

**Release Workflow:** An automated process designed to create, test, and publish new versions of software. It often includes steps like version bumping, changelog generation, and artifact publishing.

**SARIF (Static Analysis Results Interchange Format):** A standardized format for representing the output of static analysis tools. It enables the consistent reporting and sharing of code analysis results across different tools and platforms.

**SBOM (Software Bill of Materials):** A comprehensive inventory of all components used in software, including libraries, dependencies, and other software artifacts. It's crucial for software supply chain security and vulnerability management.

**Scorecard (OSSF Scorecard):** A tool from the Open Source Security Foundation (OSSF) that assesses the security posture of open-source projects based on various security checks.

**Service:** In Kubernetes, a Service is an object that provides a stable network endpoint to access applications running in Pods. It abstracts away the underlying Pod IPs and enables service discovery and load balancing.

**SonarCloud:** A cloud-based service for continuous code quality and security inspection. It helps identify bugs, vulnerabilities, and code smells in software projects.

**SPDX (Software Package Data Exchange):** An open standard for SBOMs, defining a common format for documenting the components, licenses, and security information of software packages.

**SPDX-License-Identifier:** A standardized way to declare the software license in source code files, making it clear under what terms the software is distributed. "Apache-2.0" indicates the Apache License, Version 2.0.

**TAZAMA_EID (Tazama Entity Identifier):** A proprietary identifier specific to the Tazama system, used to uniquely identify entities within that ecosystem.

**tfsec:** A static security scanner for Terraform code. It helps identify potential security misconfigurations and vulnerabilities in infrastructure-as-code deployments.

**Terraform:** An infrastructure-as-code tool that allows users to define and provision infrastructure resources in a declarative manner.

**TMS (Transaction Monitoring Service):** The core service of this project, responsible for monitoring financial transactions for various purposes, such as fraud detection, compliance, and risk management.

**TxTp (Transaction Type):**  Indicates the specific type of financial transaction being processed, such as 'pain.001' or 'pacs.008', as defined by ISO 20022 standards.

**TxSts (Transaction Status):** Represents the current state or outcome of a transaction, such as 'ACCC' (Accepted Credit Commitment) in pacs.002 messages, indicating successful processing.

**Valkey Cache:** (See Cache (Valkey/Redis))

**XchgRate (Exchange Rate):** The rate at which one currency can be exchanged for another, used in cross-currency transactions.

**XTS:** An example currency code, often used in testing or development environments to represent a generic or system-specific currency.
