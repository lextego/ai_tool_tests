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
# EMMA Event Monitoring API

## Overview

**EMMA Event Monitoring API** is a Node.js-based service for processing, validating, and monitoring ISO 20022 financial transaction messages. It is designed for high reliability, scalability, and integration with distributed systems. The API supports message types such as `pain.001`, `pain.013`, `pacs.008`, and `pacs.002`, and provides robust authentication, caching, and database management.

## Features

* **ISO 20022 Message Processing:** Handles `pain.001.001.11`, `pain.013.001.09`, `pacs.008.001.10`, and `pacs.002.001.12` messages.

* **Fastify Framework:** High-performance HTTP server with schema validation and Swagger documentation.

* **Authentication:** Optional JWT-based authentication for secure endpoints.

* **Caching & Database:** Integrates with Redis and database backends for transaction history and relationship management.

* **Clustering:** Utilizes Node.js clustering for multi-core scalability.

* **Observability:** Integrated APM and structured logging.

* **Swagger UI:** Interactive API documentation.

## Getting Started

### Prerequisites

* Node.js (v16+ recommended)

* Docker (for containerized deployment)

* Access to required private NPM packages (`@tazama-lf/frms-coe-lib`, etc.)

### Installation

1. **Clone the repository:**

   ```
   git clone https://github.com/lextego/EMMA_event_monitoring_api.git
   cd EMMA_event_monitoring_api
   ```

2. **Install dependencies:**

   ```
   npm install
   ```

3. **Configure environment variables:**

   * Set up required environment variables such as `PORT`, `QUOTING`, `AUTHENTICATED`, and any database/Redis credentials.

4. **(Optional) Build and run with Docker:**

   ```
   docker-compose up --build
   ```

### Running the Application

#### Development

```
npm run dev
```

#### Production

```
npm start
```

#### With Docker

```
docker-compose up
```

### API Endpoints

* `GET /health` — Health check endpoint.

* `POST /v1/evaluate/iso20022/pain.001.001.11` — Process `pain.001` messages.

* `POST /v1/evaluate/iso20022/pain.013.001.09` — Process `pain.013` messages.

* `POST /v1/evaluate/iso20022/pacs.008.001.10` — Process `pacs.008` messages.

* `POST /v1/evaluate/iso20022/pacs.002.001.12` — Process `pacs.002` messages.

* `GET /documentation` — Swagger UI for API documentation.

### Configuration

Configuration is managed via environment variables and the `src/config.ts` file. Key variables include:

* `PORT`: Port to run the server on.

* `QUOTING`: Enable/disable quoting mode.

* `AUTHENTICATED`: Enable/disable authentication.

### Project Structure

* `src/`

  * `app.controller.ts` — Main request handlers for each message type.

  * `clients/` — Fastify server, cache/database integration.

  * `logic.service.ts` — Core business logic for message processing.

  * `auth/` — Authentication middleware.

  * `router.ts` — API route definitions.

  * `utils/` — Utility functions (e.g., schema validation).

  * `schemas/` — JSON schemas for message validation.

### Development Notes

* The project uses private libraries from the Tazama ecosystem.

* Logging and APM are integrated for observability.

* Clustering is enabled for multi-core performance.

## License

Licensed under the Apache-2.0 License

<!-- @joggr:editLink(ba237134-5f94-4f00-b3fd-88fa515a66dc):start -->
---
<a href="https://app.joggr.io/app/documents/ba237134-5f94-4f00-b3fd-88fa515a66dc/edit">
  <img src="https://cdn.joggr.io/assets/static/badges/joggr-document-edit.svg?did=ba237134-5f94-4f00-b3fd-88fa515a66dc" alt="Edit doc on Joggr" />
</a>
<!-- @joggr:editLink(ba237134-5f94-4f00-b3fd-88fa515a66dc):end -->
