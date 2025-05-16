<!--
Documentation research and outputs by LexTego Ltd.
Licensed under the Creative Commons Attribution-ShareAlike 4.0 International License.
See: https://creativecommons.org/licenses/by-sa/4.0/
-->

# Transaction Monitoring Service (TMS) - Repository Overview

## 1. Overview

The `transaction-monitoring-service` is a Node.js application built with TypeScript designed to receive, validate, process, and monitor financial transaction messages, primarily in the ISO 20022 format. It acts as a crucial component in a larger financial transaction processing system (like Tazama).

The service exposes an HTTP API (defined via Swagger) to accept specific ISO 20022 message types (pain.001, pain.013, pacs.008, pacs.002). Upon receiving a message, it performs validation, persists transaction details and related entities (accounts, holders) into an ArangoDB database, utilizes caching (Redis/Valkey and local Node Cache) for performance, and forwards the processed message via NATS to a downstream service (likely the `event-director`).

## 2. Key Features

*   **ISO 20022 Message Processing:** Accepts and validates `pain.001.001.11`, `pain.013.001.09`, `pacs.008.001.10`, and `pacs.002.001.12` messages.
*   **API Endpoints:** Provides RESTful endpoints for submitting transactions and checking service health.
*   **Data Persistence:** Stores transaction history, account information, and entity relationships in ArangoDB.
*   **Caching:** Implements both distributed (Redis/Valkey) and local caching strategies to optimize data retrieval.
*   **Event Forwarding:** Publishes processed transaction messages to a NATS stream (`event-director`) for further processing or rule evaluation.
*   **Configurable:** Service behavior (e.g., quoting mode, authentication, database connections, NATS servers, caching TTLs) is configurable via environment variables.
*   **Containerized:** Designed to run as a Docker container, with Kubernetes manifests provided.

## 3. Technology Stack

*   **Language:** TypeScript
*   **Runtime:** Node.js (v16, v20 tested in CI)
*   **Framework:** Likely Fastify (inferred from Node.js backend service structure)
*   **API Definition:** Swagger (OpenAPI 2.0)
*   **Database:** ArangoDB (for transaction history, pseudonyms)
*   **Caching:** Redis/Valkey (distributed), Node Cache (local)
*   **Messaging:** NATS
*   **Containerization:** Docker
*   **Orchestration:** Kubernetes
*   **CI/CD:** GitHub Actions
*   **Linting/Formatting:** ESLint, Prettier
*   **Testing:** Likely Jest or similar (inferred from `npm test`)
*   **Monitoring:** Elastic APM (optional, configurable)
*   **Logging:** Configurable, potentially Logstash integration

## 4. Repository Structure

. 
├── .github/ # GitHub specific files (workflows, templates) 
│ 
├── workflows/ # CI/CD pipeline definitions 
│ └── PULL_REQUEST_TEMPLATE.md # Template for PR descriptions 
├── .husky/ # Git hooks configuration (pre-commit, pre-push) 
├── src/ # Service source code (TypeScript) 
│ └── interfaces/ # TypeScript interfaces (e.g., iTransactionRelationship.ts) 
├── .dockerignore # Files to ignore during Docker build 
├── .editorconfig # Editor configuration settings 
├── .env.template # Template for environment variables 
├── .gitignore # Files ignored by Git 
├── .npmrc # NPM configuration (scoped registry) 
├── .prettierignore # Files ignored by Prettier 
├── .sonarcloud.properties # SonarCloud configuration 
├── CHANGELOG.md # Manual changelog file 
├── Dockerfile # Multi-stage Docker build definition 
├── README.md # Original project README 
├── VERSION # File containing the current version string 
├── cluster-setup.ts # Helper script (likely for testing setup) 
├── deployment.yaml # Kubernetes Deployment manifest 
├── docker-compose.yaml # Docker Compose file (likely for local dev/testing) 
├── package-lock.json # NPM dependency lock file ├── package.json # NPM project manifest (dependencies, scripts) ├── service.yaml # Kubernetes Service manifest ├── swagger.yaml # OpenAPI (Swagger) definition for the API └── tsconfig.json # TypeScript compiler configuration ```

## 5 Configuration

The service is configured primarily through environment variables. A template file .env.template lists the available options, including:

FUNCTION_NAME, NODE_ENV, PORT
NATS connection details (SERVER_URL, PRODUCER_STREAM, STARTUP_TYPE)
Database connection details (ArangoDB URLs, credentials for transactionHistory and pseudonyms databases)
Caching settings (Redis/Valkey servers, auth, TTLs, local cache settings)
Authentication settings (AUTHENTICATED, CERT_PATH_PUBLIC)
Elastic APM settings (APM_ACTIVE, APM_SERVICE_NAME, etc.)
Logging settings (Logstash host/port/level)

## 6. API

The service exposes an HTTP API defined in swagger.yaml. Key endpoints include:

GET / & GET /health: Check the health status of the service.
POST /v1/evaluate/iso20022/pain.001.001.11: Submit a pain.001 message.
POST /v1/evaluate/iso20022/pain.013.001.09: Submit a pain.013 message.
POST /v1/evaluate/iso20022/pacs.008.001.10: Submit a pacs.008 message.
POST /v1/evaluate/iso20022/pacs.002.001.12: Submit a pacs.002 message.
Refer to the swagger.yaml file for detailed request/response schemas.

## 7. Sequence Diagram (ISO Message Flow)

This diagram illustrates the typical flow when an ISO 20022 message is processed by the TMS.
