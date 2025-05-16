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
sequenceDiagram
    participant Client
    participant FastifyAPI as Fastify API Server
    participant Auth as Auth Handler
    participant Controller as Controller (app.controller)
    participant Logic as Logic Service
    participant CacheDB as Cache Database Service
    participant EventDirector as Event Director

    Client->>FastifyAPI: HTTP POST /v1/evaluate/iso20022/{messageType}
    alt Authentication Enabled
        FastifyAPI->>Auth: Validate JWT Token and Claims
        Auth-->>FastifyAPI: Auth Result
        FastifyAPI->>Controller: Forward Request if Authenticated
    else Authentication Disabled
        FastifyAPI->>Controller: Forward Request
    end
    Controller->>Logic: Call handle{MessageType}(transaction, type)
    Logic->>CacheDB: Save Transaction History
    Logic->>CacheDB: Save Transaction Relationship
    Logic->>CacheDB: Add Accounts/Entities
    Logic-->>Controller: Processing Result
    Controller->>Client: HTTP 200/500 Response
    Logic->>EventDirector: Notify with Transaction and Metadata
```

## Detailed Sequence Diagram

```mermaid
sequenceDiagram
    participant Client
    participant Fastify as Fastify Server
    participant Auth as Auth Handler
    participant Controller as app.controller
    participant Logic as logic.service
    participant CacheDB as CacheDatabaseService
    participant DB as Database/Redis
    participant EventDirector as Event Director
    participant Logger as LoggerService
    participant APM as APM

    Client->>Fastify: POST /v1/evaluate/iso20022/{messageType}
    Note right of Fastify: Receives HTTP request
    alt AUTHENTICATED enabled
        Fastify->>Auth: tokenHandler(claim)
        Auth->>Logger: Log authentication attempt
        Auth->>Auth: Validate JWT token and claims
        Auth-->>Fastify: 401 Unauthorized (if invalid)
        Auth-->>Fastify: Continue (if valid)
    end
    Fastify->>Controller: Call {MessageType}Handler(req, reply)
    Controller->>Logger: Log Start - Handle {transactionType} request
    Controller->>Logic: handle{MessageType}(transaction, transactionType)
    Logic->>Logger: Log Start - Handle transaction data
    Logic->>APM: Start APM span
    Logic->>CacheDB: saveTransactionHistory(transaction, redisKey)
    CacheDB->>DB: Save transaction to DB/Redis
    Logic->>CacheDB: addAccount(debtorAcctId)
    CacheDB->>DB: Save debtor account
    Logic->>CacheDB: addAccount(creditorAcctId)
    CacheDB->>DB: Save creditor account
    Logic->>CacheDB: addEntity(creditorId, CreDtTm)
    CacheDB->>DB: Save creditor entity
    Logic->>CacheDB: addEntity(debtorId, CreDtTm)
    CacheDB->>DB: Save debtor entity
    Logic->>CacheDB: saveTransactionRelationship(transactionRelationship)
    CacheDB->>DB: Save transaction relationship
    Logic->>CacheDB: addAccountHolder(creditorId, creditorAcctId, CreDtTm)
    CacheDB->>DB: Save creditor account holder
    Logic->>CacheDB: addAccountHolder(debtorId, debtorAcctId, CreDtTm)
    CacheDB->>DB: Save debtor account holder
    Logic->>APM: End APM span
    Logic->>Logger: Log Transaction sent to event-director
    Logic->>EventDirector: handleResponse({transaction, DataCache, metaData})
    Logic-->>Controller: Success or Error
    Controller->>Logger: Log End - Handle {transactionType} request
    Controller->>Client: HTTP 200/500 Response
```

<!-- @joggr:editLink(ce98551f-64b5-4d24-bd7e-d7b45a99aa51):start -->
---
<a href="https://app.joggr.io/app/documents/ce98551f-64b5-4d24-bd7e-d7b45a99aa51/edit">
  <img src="https://cdn.joggr.io/assets/static/badges/joggr-document-edit.svg?did=ce98551f-64b5-4d24-bd7e-d7b45a99aa51" alt="Edit doc on Joggr" />
</a>
<!-- @joggr:editLink(ce98551f-64b5-4d24-bd7e-d7b45a99aa51):end -->
