<!--
Documentation research and outputs by LexTego Ltd.
Licensed under the Creative Commons Attribution-ShareAlike 4.0 International License.
See: https://creativecommons.org/licenses/by-sa/4.0/
-->
1. Project Overview & Purpose

Name: Transaction Monitoring Service (TMS)
Purpose: This service acts as an ingestion point for financial transaction messages, specifically focusing on the ISO 20022 standard. Its primary goal is to receive these messages, validate them, persist relevant information for monitoring and analysis, and then forward them for further processing. It plays a role in risk management and compliance within a larger financial system (likely the Tazama platform, given the @tazama-lf scope in .npmrc).
Core Functionality:
Accepts HTTP POST requests containing specific ISO 20022 messages (pain.001.001.11, pain.013.001.09, pacs.008.001.10, pacs.002.001.12).
Validates the incoming message format against its Swagger/OpenAPI definition.
Extracts key data points (parties, accounts, amounts, IDs, etc.).
Persists transaction history, account details, entity information, and relationships between them into an ArangoDB database.
Utilizes caching (both local Node cache and distributed Redis/Valkey) for performance, particularly noted for retrieving related pacs.008 messages when processing pacs.002.
Forwards the validated message to another service, the "Event-Director" (ED), via NATS messaging.
Provides health check endpoints (/ and /health).
2. Technology Stack

Language: TypeScript (compiled to JavaScript for runtime)
Framework: Likely Fastify (inferred from PORT env var and common Node.js practices, although not explicitly stated in provided files)
Database: ArangoDB (for storing transaction history, pseudonyms, accounts, entities, and relationships)
Caching: Redis (configurable as cluster or standalone) and an in-memory Node cache.
Messaging: NATS (for publishing messages to the event-director stream)
API Definition: OpenAPI v2 (Swagger) defined in swagger.yaml.
Containerization: Docker (Dockerfile, .dockerignore, docker-compose.yaml)
Orchestration: Kubernetes (deployment.yaml, service.yaml)
Monitoring: Elastic APM (optional, configured via env vars), Logstash (for log shipping)
Code Quality: Prettier (formatting), ESLint (linting - implied by .eslintcache in .gitignore), SonarCloud (static analysis)
3. Architecture & Flow

The service follows a typical microservice pattern:

Receive: Listens for HTTP POST requests on specific endpoints defined in swagger.yaml.
Validate: Uses Swagger middleware (implied by the activity diagram and standard practice) to validate the request body against the defined schema. Invalid requests are rejected (HTTP 400).
Process:
Parses the valid ISO 20022 message.
Performs database operations (ArangoDB):
Saves transaction history.
Adds/updates account and entity information for debtor and creditor.
Creates relationships between entities/accounts and the transaction.
Handles caching logic (check cache, retrieve from DB if miss, update cache).
Logs relevant information (potentially shipping to Logstash).
Optionally sends traces to Elastic APM.
Forward: Publishes the processed message payload to a NATS stream (event-director).
Respond: Sends an HTTP 200 success response back to the original client, typically containing the original transaction object.
The QUOTING environment variable acts as a feature flag, potentially disabling the processing of pain.001 and pain.013 messages if set to false.

4. API Definition (swagger.yaml)

Defines the REST API structure, including paths, parameters, request bodies, and responses.
Endpoints:
GET /, GET /health: Service health checks.
POST /v1/evaluate/iso20022/pain.001.001.11: Submit pain.001 messages.
POST /v1/evaluate/iso20022/pain.013.001.09: Submit pain.013 messages.
POST /v1/evaluate/iso20022/pacs.008.001.10: Submit pacs.008 messages.
POST /v1/evaluate/iso20022/pacs.002.001.12: Submit pacs.002 messages.
Includes detailed schemas for each ISO 20022 message type and standard error responses.
5. Containerization & Deployment (Dockerfile, deployment.yaml, service.yaml)

Dockerfile:
Uses a multi-stage build approach for efficiency and security.
Stage 1 (builder): Installs all dependencies, compiles TypeScript.
Stage 2 (dep-resolver): Installs only production dependencies.
Stage 3 (run-env): Uses a minimal distroless/nodejs20-debian11:nonroot image. Copies built code, production node_modules, and necessary configuration files.
Sets numerous environment variables with default production values.
The final command runs the compiled application (build/index.js).
Kubernetes:
deployment.yaml: Defines a Deployment for the service in the processor namespace.
Includes the main TMS container and a sidecar container (tms-sidecar-rel-1-0-0), likely for observability or other cross-cutting concerns (e.g., log forwarding, metrics scraping proxy).
Uses a RollingUpdate strategy (maxUnavailable: 0, maxSurge: 1).
service.yaml: Defines a ClusterIP Service to expose the Deployment internally within the Kubernetes cluster on ports 3000 (TMS) and 5000 (sidecar).
6. Configuration (.env.template)

Configuration is heavily reliant on environment variables.
Key configurable areas include:
NATS connection details and stream names.
Fastify port.
Caching settings (Redis/Valkey connection, TTLs, enable/disable flags for distributed and local cache).
ArangoDB connection details (URLs, credentials, database names) for both transactionHistory and pseudonyms databases.
Elastic APM configuration (activation, URL, token).