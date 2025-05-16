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
```mermaid
flowchart TD
    A[Client Request] --> B[Fastify Server Receives Request]
    B --> C{Is Authentication Enabled?}
    C -- Yes --> D[Auth Handler Validates JWT Token]
    D -- Invalid --> E[Return 401 Unauthorized]
    D -- Valid --> F[Route to Controller]
    C -- No --> F[Route to Controller]
    F --> G[Controller Logs Start]
    G --> H[Controller Calls Logic Service]
    H --> I[Logic Service Starts APM Span]
    I --> J[Logic Service Extracts Transaction Data]
    J --> K[Save Transaction History CacheDatabaseService]
    K --> L[Save Transaction Relationship CacheDatabaseService]
    L --> M[Add Accounts and Entities CacheDatabaseService]
    M --> N[Add Account Holders CacheDatabaseService]
    N --> O[End APM Span]
    O --> P[Notify Event Director]
    P --> Q[Controller Logs End]
    Q --> R[Send HTTP Response to Client]

    style E fill:#faa,stroke:#d33,stroke-width:2px
    style R fill:#bbf,stroke:#33d,stroke-width:2px
```

<!-- @joggr:editLink(bb4bb109-e19e-4c37-a649-b9b8903af8f1):start -->
---
<a href="https://app.joggr.io/app/documents/bb4bb109-e19e-4c37-a649-b9b8903af8f1/edit">
  <img src="https://cdn.joggr.io/assets/static/badges/joggr-document-edit.svg?did=bb4bb109-e19e-4c37-a649-b9b8903af8f1" alt="Edit doc on Joggr" />
</a>
<!-- @joggr:editLink(bb4bb109-e19e-4c37-a649-b9b8903af8f1):end -->
