<!--
Documentation research and outputs by LexTego Ltd.
Licensed under the Creative Commons Attribution-ShareAlike 4.0 International License.
See: https://creativecommons.org/licenses/by-sa/4.0/
-->

"External Client"
"Transaction Monitoring Service"
"Logger"
"ArangoDB"
"Valkey Cache"
"Event-Director"

```mermaid

```

alt
[Validation Error]
par
[save in ArangoDB]
par
[save in ArangoDB]
alt
[Error]
alt
[Validation Error]
par
[save in ArangoDB]
alt
[Error]
alt
[Validation Error]
par
[save in ArangoDB]
par
[save in ArangoDB]
par
[save in ArangoDB]
alt
[Quoting Enabled]
alt
[Error]
alt
[Validation Error]
alt
[cache miss]
alt
[Error]
POST /v1/evaluate/iso20022/pain.001.001.11: Pain001.001.11 Message
Validate Pain001
Logging of receipt
Logging of error
/v1/evaluate/iso20022/pain.001.001.11 POST Result
saveTransactionHistory(pain001)
addAccount(debtor)
addAccount(creditor)
addEntity(debtor)
addEntity(creditor)
saveTransactionRelationship(pain001)
addAccountHolder(debtor)
addAccountHolder(creditor)
Logging of error
Throw error
NATS handleResponse: Pain001 Message
Transaction sent to ED service
/v1/evaluate/iso20022/pain.001.001.11 POST Result
POST /v1/evaluate/iso20022/pain.013.001.09: Pain013.001.09 Message
Validate Pain013
Logging of receipt
Logging of error
/v1/evaluate/iso20022/pain.013.001.09 POST Result
saveTransactionHistory(pain013)
addAccount(debtor)
addAccount(creditor)
saveTransactionRelationship(pain013)
Logging of error
Throw error
NATS handleResponse: Pain013 Message
Transaction sent to ED service
/v1/evaluate/iso20022/pain.013.001.09 POST Result
POST /v1/evaluate/iso20022/pacs.008.001.10: Pacs008.001.10 Message
Validate Pacs008
Logging of receipt
Logging of error
/v1/evaluate/iso20022/pacs.008.001.10 POST Result
addAccount(debtor)
addAccount(creditor)
save Data Cache
addEntity(creditor)
addEntity(debtor)
addAccountHolder(creditor)
addAccountHolder(debtor)
saveTransactionRelationship
saveTransactionHistory(pacs008)
Logging of error
Throw error
NATS handleResponse: Pacs008 Message
Transaction sent to ED service
/v1/evaluate/iso20022/pacs.008.001.10 POST Result
POST /v1/evaluate/iso20022/pacs.002.001.12: Pacs002.001.12 Message
Validate Pacs002
Logging of receipt
Logging of error
/v1/evaluate/iso20022/pacs.002.001.12 POST Result
getCache
get Pacs008
rebuild cache
saveTransactionHistory
get Pacs008
saveTransactionRelationship
Logging of error
Throw error
NATS handleResponse: Pacs002 Message
Transaction sent to ED service
/v1/evaluate/iso20022/pacs.002.001.12 POST Result
Yes

Yes

No

No

Start

Accept the HTTP POST request (JSON)

Request accepted?

Swagger

Unsupported markdown: list
Is request format validated?

Swagger

Throw an error

Stop

Unsupported markdown: list
Error

Stop

Unsupported markdown: list
Create object

Unsupported markdown: list
Populate Database

Unsupported markdown: list
Send Message to Event-Director

Unsupported markdown: list
Response

Unsupported markdown: list
Stop

Syntax error in text
mermaid version 11.6.0
please can you provide the mermaid text only - i.e. do not wrap it in ```
CD Pipeline

CI Pipeline

Git Push/Merge Trigger

Checkout Code

Setup Node.js

Install Dependencies
(npm ci with GH_TOKEN)

Lint Code
(ESLint)

Run Tests
(Unit/Integration, e.g., Jest/nyc)
Generate Coverage

Build Application
(npm run build)

Static Analysis
(SonarCloud Scan)

Build Docker Image
(Multi-stage Dockerfile)

Push Docker Image
(To Registry e.g., example.io)

Deploy to Kubernetes
(Apply deployment.yaml, service.yaml)
Target: 'processor' namespace

What does this repository do?
Can you summarize the folder structure?
What programming languages are used in this project?
Send me prompt and request ai chat...


Project InfoClose menu
Statistics
Files:
65
Components:
12
Token Count:
"this is a copy of the TMS to test Dosu"
Technologies used
Shell

Dockerfile

JavaScript

TypeScript

Topics
Last Edited:
2021-10-10

Made By:
lextego

© 2025 Githubme™. All Rights Reserved.
