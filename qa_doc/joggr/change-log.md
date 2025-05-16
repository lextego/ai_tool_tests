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
All notable changes to this project will be documented in this file.

## \[Unreleased]

* Initial changelog created.

## \[1.0.0] - 2024-06-11

### Added

* Initial release of EMMA Event Monitoring API.

* Fastify server setup with clustering and APM integration.

* Endpoints for ISO 20022 message types:

  * `pain.001.001.11` (Customer Credit Transfer Initiation)

  * `pain.013.001.09` (Creditor Payment Activation Request)

  * `pacs.008.001.10` (FI to FI Customer Credit Transfer)

  * `pacs.002.001.12` (Payment Status Report)

* JWT-based authentication (configurable via environment variable).

* Caching and database management for transaction history and relationships.

* Swagger UI for interactive API documentation.

* Health check endpoints.

* Structured logging and error handling.

### Changed

* N/A

### Fixed

* N/A

***

> *For future releases, add new sections with version, date, and details of changes, improvements, and bug fixes.*

<!-- @joggr:editLink(16fcb99d-edf0-406c-b55d-bddc4b34f652):start -->
---
<a href="https://app.joggr.io/app/documents/16fcb99d-edf0-406c-b55d-bddc4b34f652/edit">
  <img src="https://cdn.joggr.io/assets/static/badges/joggr-document-edit.svg?did=16fcb99d-edf0-406c-b55d-bddc4b34f652" alt="Edit doc on Joggr" />
</a>
<!-- @joggr:editLink(16fcb99d-edf0-406c-b55d-bddc4b34f652):end -->
