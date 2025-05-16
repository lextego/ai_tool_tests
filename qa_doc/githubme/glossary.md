<!--
Documentation research and outputs by LexTego Ltd.
Licensed under the Creative Commons Attribution-ShareAlike 4.0 International License.
See: https://creativecommons.org/licenses/by-sa/4.0/
-->
# Glossary

- **Account**: Represents a financial account involved in a transaction (e.g., DbtrAcct, CdtrAcct). Stored in ArangoDB.
- **Account Holder**: Represents the relationship between an Entity (person/organization) and an Account. Stored in ArangoDB.
- **Activity Diagram**: A type of flowchart used in the README to illustrate the step-by-step workflow of processing a transaction message within the TMS.
- **API (Application Programming Interface)**: The set of endpoints (defined in swagger.yaml) that the TMS exposes for external clients to interact with, primarily for submitting transaction messages.
- **APM (Application Performance Monitoring)**: A system (like Elastic APM) used for monitoring the performance and health of the application. Configured via APM_... environment variables.
- **ArangoDB**: The multi-model NoSQL database used by TMS to store persistent data, including transaction history, account details, entity information, and relationships between them. Configured via TRANSACTION_HISTORY_DATABASE_... and PSEUDONYMS_DATABASE_... environment variables.
- **AUTHENTICATED (Environment Variable)**: A boolean flag (true/false) indicating whether API authentication is enabled.
- **Cache (Valkey Cache / Redis)**: An in-memory data store used to temporarily hold frequently accessed data (like pacs.008 messages) to speed up processing (e.g., for subsequent pacs.002 messages). Configured via REDIS_..., DISTRIBUTED_CACHE..., and LOCAL_CACHE... **environment variables. (Note**: README mentions Valkey, .env.template mentions Redis - likely related or interchangeable in this context).
- **Cache Miss**: An event that occurs when the application requests data from the cache, but the data is not found there, requiring retrieval from the primary database (ArangoDB).
- **CERT_PATH_PUBLIC (Environment Variable)**: Specifies the file path to the public key used for validating authentication tokens when AUTHENTICATED is true.
- **Client (External Client)**: Any external system or application that sends transaction requests (pain.001, pain.013, pacs.008, pacs.002) to the TMS API.
- **Creditor (Cdtr)**: The party receiving funds in a transaction (payee).
- **Debtor (Dbtr)**: The party initiating the payment or sending funds in a transaction (payer).
- **Dockerfile**: A script containing instructions to build the Docker container image for the TMS application. It defines build stages, dependencies, environment variables, and the final command to run the service.
- **docker-compose.yaml**: A configuration file used by Docker Compose to define and run multi-container Docker applications, often used for local development environments.
- **deployment.yaml**: A Kubernetes manifest file defining how the TMS application (including its sidecar) should be deployed onto a Kubernetes cluster (e.g., number of replicas, image details, update strategy).
- **ED (Event-Director)**: A downstream service that receives processed transaction messages from the TMS via the NATS messaging system.
- **Entity**: Represents a party (person or organization) involved in a transaction (e.g., InitgPty, Dbtr, Cdtr). Stored in ArangoDB.
- **Environment Variables**: Configuration settings passed to the application at runtime (defined in .env.template and set in the Dockerfile and potentially Kubernetes). Examples: PORT, SERVER_URL, QUOTING, database credentials, cache settings.
- **Fastify**: A Node.js web framework used to build the TMS API (implied by PORT and common Node.js practices, though not explicitly named in these files).
- **HTTP POST**: The HTTP method used by clients to submit transaction data to the TMS API endpoints.
- **ISO 20022**: An international standard for electronic data interchange between financial institutions. TMS specifically handles messages based on this standard.
- **pain.001.001.11 (Customer Credit Transfer Initiation)**: An ISO 20022 message type used to initiate a payment order from a debtor customer to their financial institution. Historically mapped to a Mojaloop Quote message. Processing might be conditional based on the QUOTING variable.
- **pain.013.001.09 (Creditor Payment Activation Request)**: An ISO 20022 message type often used in request-to-pay scenarios, where a creditor requests payment from a debtor. Historically mapped to a Mojaloop Quote Response message. Processing might be conditional based on the QUOTING variable.
- **pacs.008.001.10 (FI to FI Customer Credit Transfer)**: An ISO 20022 message type representing a payment instruction exchanged between financial institutions (FI) for a customer credit transfer. Historically mapped to a Mojaloop Transfer message.
- **pacs.002.001.12 (FI to FI Payment Status Report)**: An ISO 20022 message type used by financial institutions to report the status (e.g., acceptance, rejection) of a previously sent payment instruction (like a pacs.008).
- **JSON (JavaScript Object Notation)**: The data format used for requests and responses in the TMS API.
- **Logger**: The component within the TMS responsible for recording application events, transaction details, and errors, potentially sending them to Logstash.
- **Logstash**: An external log processing pipeline component, configured via LOGSTASH_... environment variables, likely used to collect, parse, and forward logs from the TMS.
- **Middleware**: Software components that handle requests before they reach the main application logic. In this context, Swagger acts as middleware for request validation.
- **MSISDN (Mobile Station International Subscriber Directory Number)**: A unique number identifying a subscription in a mobile network (a phone number). Often used as an account identifier in mobile money systems, as seen in the sample messages (SchmeNm: { Prtry: "MSISDN" }).
- **NATS**: A high-performance messaging system used for communication between the TMS and the Event-Director (ED). Configured via SERVER_URL, PRODUCER_STREAM, etc.
- **Node.js**: The JavaScript runtime environment used to execute the TMS application.
- **QUOTING (Environment Variable)**: A boolean flag (true/false) that controls specific business logic, potentially enabling or disabling the processing of pain.001 and pain.013 messages.
- **Sequence Diagram**: A type of interaction diagram used in the README to show how different components (Client, TMS, ArangoDB, Cache, ED, Logger) interact over time for each message type.
- **service.yaml**: A Kubernetes manifest file defining how to expose the TMS deployment as a network service within the cluster (e.g., assigning it an internal IP address and port).
- **Sidecar**: An auxiliary container deployed alongside the main application container (TMS) within the same Kubernetes Pod (defined in deployment.yaml). It likely handles tasks like log forwarding or metrics collection, communicating over port 5000 (SIDECAR_HOST).
- **Swagger**: A toolset for defining and documenting RESTful APIs. The swagger.yaml file defines the TMS API structure, endpoints, request/response formats, and is used for automatic request validation.
- **TAZAMA_EID**: A proprietary identifier scheme mentioned in the pacs.008 sample message (SchmeNm: { Prtry: "TAZAMA_EID" }), likely representing a Tazama-specific Entity ID.
- **TMS (Transaction Monitoring Service)**: The core application described in the repository. Its primary function is to receive financial transaction messages (ISO 20022), validate them, store relevant data in ArangoDB and cache, and forward them to the Event-Director via NATS for further processing or analysis.
- **Transaction History**: The record of processed transactions stored in the transactionHistory database in ArangoDB.
- **Transaction Relationship**: A data structure stored in ArangoDB that links related transaction messages or entities (e.g., linking a pacs.002 status update back to the original pacs.008 transfer). Defined by the iTransactionRelationship.ts interface.
- **TypeScript**: A typed superset of JavaScript used to develop the TMS application, compiled to JavaScript during the build process (tsconfig.json, npm run build).