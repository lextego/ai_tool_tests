<!--@@joggrdoc@@-->
<!-- @joggr:version(v2):end -->
<!-- @joggr:warning:start -->
<!-- 
  _   _   _    __        __     _      ____    _   _   ___   _   _    ____     _   _   _ 
 | | | | | |   \ \      / /    / \    |  _ \  | \ | | |_ _| | \ | |  / ___|   | | | | | |
 | | | | | |    \ \ /\ / /    / _ \   | |_) | |  \| |  | |  |  \| | | |  _    | | | | | |
 |_| |_| |_|     \ V  V /    / ___ \  |  _ <  | |\  |  | |  | |\  | | |_| |   |_| |_| |_|
 (_) (_) (_)      \_/\_/    /_/   \_\ |_| \_\ |_| \_| |___| |_| \_|  \____|   (_) (_) (_)
                                                              
This document is managed by Joggr. Editing this document could break Joggr's core features, i.e. our 
ability to auto-maintain this document. Please use the Joggr editor to edit this document 
(link at bottom of the page).

Documentation research and outputs by LexTego Ltd.
Licensed under the Creative Commons Attribution-ShareAlike 4.0 International License.
See: https://creativecommons.org/licenses/by-sa/4.0/

-->
<!-- @joggr:warning:end -->
**EMMA Event Monitoring API** is a Node.js service designed to process, validate, and monitor ISO 20022 financial transaction messages. The application is built with scalability, reliability, and observability in mind, leveraging modern frameworks and best practices.

### Key Components

* **Fastify Server:** The API uses Fastify for high-performance HTTP handling, schema validation, and plugin support. Endpoints are defined for processing various ISO 20022 message types.

* **Message Handlers:** The main controller (`app.controller.ts`) provides handlers for different message types (`pain.001`, `pain.013`, `pacs.008`, `pacs.002`). Each handler validates, processes, and stores transaction data, and responds with appropriate status messages.

* **Business Logic:** The core logic (`logic.service.ts`) extracts transaction details, manages relationships, and coordinates database/cache operations. It also notifies an external event director service after processing.

* **Authentication:** Optional JWT-based authentication is implemented via middleware, configurable through environment variables.

* **Database & Caching:** The `CacheDatabaseService` abstracts interactions with databases and Redis, supporting transaction history, account, and entity management.

* **Clustering & Observability:** The app supports multi-core scaling using Node.js clustering and integrates APM and structured logging for monitoring and debugging.

* **API Documentation:** Swagger UI is provided for interactive API exploration and testing.

### Main Features

* **Endpoints for ISO 20022 messages:**

  * `pain.001.001.11` (Customer Credit Transfer Initiation)

  * `pain.013.001.09` (Creditor Payment Activation Request)

  * `pacs.008.001.10` (FI to FI Customer Credit Transfer)

  * `pacs.002.001.12` (Payment Status Report)

* **Health check and documentation endpoints**

* **Configurable authentication and quoting modes**

* **Robust error handling and logging**

### Project Structure

* `src/`

  * `app.controller.ts` – HTTP request handlers

  * `logic.service.ts` – Business logic for message processing

  * `clients/` – Fastify server and database/cache integration

  * `auth/` – Authentication middleware

  * `router.ts` – API route definitions

  * `utils/` – Utility functions

  * `schemas/` – JSON schemas for validation

***

**In summary:** The codebase is a modular, production-ready API for financial message processing, with strong support for validation, security, observability, and extensibility.

<!-- @joggr:editLink(069e87b6-474b-4bf7-b790-84faf0286cf5):start -->
---
<a href="https://app.joggr.io/app/documents/069e87b6-474b-4bf7-b790-84faf0286cf5/edit">
  <img src="https://cdn.joggr.io/assets/static/badges/joggr-document-edit.svg?did=069e87b6-474b-4bf7-b790-84faf0286cf5" alt="Edit doc on Joggr" />
</a>
<!-- @joggr:editLink(069e87b6-474b-4bf7-b790-84faf0286cf5):end -->
