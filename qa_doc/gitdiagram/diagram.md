<!--
Documentation research and outputs by LexTego Ltd.
Licensed under the Creative Commons Attribution-ShareAlike 4.0 International License.
See: https://creativecommons.org/licenses/by-sa/4.0/
-->
```mermaid
flowchart TB
    EC[External Client]
    TMS [TMS API Server]
    EC -HTTP_POST-> TMS

    subgraph "API Server Layer"
        "TMS API Server":::server
        "Authentication Module":::auth
        "API Documentation/Validation":::validation
        "TMS API Server" -->|"OptionalAuth"| "Authentication Module"
        "TMS API Server" -->|"ReqValidation"| "API Documentation/Validation"
    end

    subgraph "Business Logic Layer"
        "Business Logic Service":::logic
        "TMS API Server" -->|"Route"| "Business Logic Service"
        "Business Logic Service" -->|"LogMessage"| "Logging Service":::logging
    end

    subgraph "Data Persistence Layer"
        "Database (ArangoDB)":::database
        "Caching Layer":::cache
        "Business Logic Service" -->|"SaveTransaction"| "Database (ArangoDB)"
        "Business Logic Service" -->|"CacheCheckUpdate"| "Caching Layer"
    end

    subgraph "Event Messaging"
        "Event Director (NATS)":::event
        "Business Logic Service" -->|"PublishEvent"| "Event Director (NATS)"
    end

    click "External Client" "src/clients/fastify.ts"
    click "TMS API Server" "src/index.ts"
    click "TMS API Server" "src/app.controller.ts"
    click "TMS API Server" "src/router.ts"
    click "Business Logic Service" "src/logic.service.ts"
    click "Authentication Module" "src/auth/authHandler.ts"
    click "Database (ArangoDB)" "src/clients/cache-database.ts"
    click "Caching Layer" "src/clients/cache-database.ts"
    click "API Documentation/Validation" "swagger.yaml"
    click "Logging Service" "src/apm.ts"

    classDef external fill:#AED6F1,stroke:#1F618D,stroke-width:2px;
    classDef server fill:#ABEBC6,stroke:#239B56,stroke-width:2px;
    classDef auth fill:#FAD7A0,stroke:#D68910,stroke-width:2px;
    classDef validation fill:#F9E79F,stroke:#B7950B,stroke-width:2px;
    classDef logic fill:#D2B4DE,stroke:#8E44AD,stroke-width:2px;
    classDef logging fill:#E6B0AA,stroke:#C0392B,stroke-width:2px;
    classDef database fill:#A3E4D7,stroke:#2874A6,stroke-width:2px;
    classDef cache fill:#F5B7B1,stroke:#A93226,stroke-width:2px;
    classDef event fill:#D5F5E3,stroke:#28B463,stroke-width:2px;
```