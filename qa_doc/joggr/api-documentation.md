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
## Overview

The EMMA Event Monitoring API is a Fastify-based HTTP service for processing, validating, and monitoring ISO 20022 financial transaction messages. It supports multiple message types and provides endpoints for health checks and interactive documentation.

***

## Authentication

* **Type:** Bearer JWT (configurable via `AUTHENTICATED` environment variable)

* **Header:** `Authorization: Bearer <token>`

* **Required Claims:** Varies by endpoint (see below)

***

## Endpoints

### 1. Health Check

* **GET /**

* **GET /health**

* **Description:** Returns service status.

* **Response:**

  ```json
  { "status": "UP" }
  ```

***

### 2. Process ISO 20022 Messages

#### a. pain.001.001.11

* **POST /v1/evaluate/iso20022/pain.001.001.11**

* **Description:** Process a Customer Credit Transfer Initiation message.

* **Authentication Claim:** `POST_V1_EVALUATE_ISO20022_PAIN_001_001_11` (if enabled)

* **Request Body:** JSON matching `pain.001.001.11` schema

* **Response:**

  ```json
  {
    "message": "Transaction is valid",
    "data": { ...original request... }
  }
  ```

#### b. pain.013.001.09

* **POST /v1/evaluate/iso20022/pain.013.001.09**

* **Description:** Process a Creditor Payment Activation Request message.

* **Authentication Claim:** `POST_V1_EVALUATE_ISO20022_PAIN_013_001_09` (if enabled)

* **Request Body:** JSON matching `pain.013.001.09` schema

* **Response:**

  ```json
  {
    "message": "Transaction is valid",
    "data": { ...original request..., "TxTp": "pain.013.001.09" }
  }
  ```

#### c. pacs.008.001.10

* **POST /v1/evaluate/iso20022/pacs.008.001.10**

* **Description:** Process a FI to FI Customer Credit Transfer message.

* **Authentication Claim:** `POST_V1_EVALUATE_ISO20022_PACS_008_001_10` (if enabled)

* **Request Body:** JSON matching `pacs.008.001.10` schema

* **Response:**

  ```json
  {
    "message": "Transaction is valid",
    "data": { ...original request... }
  }
  ```

#### d. pacs.002.001.12

* **POST /v1/evaluate/iso20022/pacs.002.001.12**

* **Description:** Process a Payment Status Report message.

* **Authentication Claim:** `POST_V1_EVALUATE_ISO20022_PACS_002_001_12` (if enabled)

* **Request Body:** JSON matching `pacs.002.001.12` schema

* **Response:**

  ```json
  {
    "message": "Transaction is valid",
    "data": { ...original request... }
  }
  ```

***

## Error Responses

* **401 Unauthorized:**

  ```json
  { "error": "Unauthorized" }
  ```

* **500 Internal Server Error:**

  ```json
  "Failed to process execution request. <error details>"
  ```

***

## Interactive Documentation

* **Swagger UI:**

  * **URL:** `/documentation`

  * **Description:** Interactive API documentation and testing interface.

***

## Notes

* All POST endpoints require a valid ISO 20022 message body matching the respective JSON schema.

* Authentication is optional and controlled by the `AUTHENTICATED` environment variable.

* CORS is enabled for all POST endpoints.

***

## References

* [ISO 20022 Message Definitions](https://www.iso20022.org/iso-20022-message-definitions)

* [Fastify Documentation](https://www.fastify.io/docs/latest/)

<!-- @joggr:editLink(9d7c4877-8ebe-4003-89c9-18eca78a61ad):start -->
---
<a href="https://app.joggr.io/app/documents/9d7c4877-8ebe-4003-89c9-18eca78a61ad/edit">
  <img src="https://cdn.joggr.io/assets/static/badges/joggr-document-edit.svg?did=9d7c4877-8ebe-4003-89c9-18eca78a61ad" alt="Edit doc on Joggr" />
</a>
<!-- @joggr:editLink(9d7c4877-8ebe-4003-89c9-18eca78a61ad):end -->
