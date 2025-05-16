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
This glossary provides definitions for key terms and concepts used throughout the EMMA Event Monitoring API project.

***

**API (Application Programming Interface):** A set of rules and endpoints that allow different software applications to communicate with each other.

**APM (Application Performance Monitoring):** Tools and libraries used to monitor and trace the performance and health of applications.

**Authentication:** The process of verifying the identity of a user or system, often using tokens such as JWT (JSON Web Token).

**Authorization:** The process of determining if an authenticated user or system has permission to access a specific resource or perform an action.

**Bearer Token:** A type of access token used in HTTP authentication, typically passed in the `Authorization` header.

**Cache:** A temporary storage layer (such as Redis) used to store frequently accessed data for faster retrieval.

**Cluster/Clustering:** A technique to run multiple instances of a Node.js process to take advantage of multi-core systems and improve scalability.

**Controller:** A component that handles incoming HTTP requests, processes them, and returns responses.

**CORS (Cross-Origin Resource Sharing):** A security feature that allows or restricts resources on a web server to be requested from another domain.

**Docker Compose:** A tool for defining and running multi-container Docker applications using a YAML file.

**Endpoint:** A specific URL path on the API where clients can send requests (e.g., `/health`, `/v1/evaluate/iso20022/pacs.008.001.10`).

**Fastify:** A fast and low-overhead web framework for Node.js, used to build the API server.

**ISO 20022:** An international standard for electronic data interchange between financial institutions, defining message formats for payments, securities, and more.

**JWT (JSON Web Token):** A compact, URL-safe means of representing claims to be transferred between two parties, commonly used for authentication.

**Message Types:**

* **pain.001.001.11:** Customer Credit Transfer Initiation

* **pain.013.001.09:** Creditor Payment Activation Request

* **pacs.008.001.10:** FI to FI Customer Credit Transfer

* **pacs.002.001.12:** Payment Status Report

**Redis:** An in-memory data structure store, used as a database, cache, and message broker.

**Swagger UI:** A web-based interface for exploring and testing API endpoints, generated from OpenAPI/Swagger specifications.

**Transaction Relationship:** A data structure representing the connection between accounts/entities involved in a transaction, including metadata such as amount, currency, and timestamps.

**Validation:** The process of checking if incoming data (such as API requests) conforms to expected formats or schemas.

***

*This glossary is intended to help new contributors and users understand the terminology used in the EMMA Event Monitoring API project.*

<!-- @joggr:editLink(bf258b5e-a3f0-4e61-a801-5d7da685f542):start -->
---
<a href="https://app.joggr.io/app/documents/bf258b5e-a3f0-4e61-a801-5d7da685f542/edit">
  <img src="https://cdn.joggr.io/assets/static/badges/joggr-document-edit.svg?did=bf258b5e-a3f0-4e61-a801-5d7da685f542" alt="Edit doc on Joggr" />
</a>
<!-- @joggr:editLink(bf258b5e-a3f0-4e61-a801-5d7da685f542):end -->
