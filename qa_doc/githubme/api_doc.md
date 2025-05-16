<!--
Documentation research and outputs by LexTego Ltd.
Licensed under the Creative Commons Attribution-ShareAlike 4.0 International License.
See: https://creativecommons.org/licenses/by-sa/4.0/
-->
# Transaction Monitoring Service (TMS) API Documentation

## 1. Overview

The Transaction Monitoring Service (TMS) is responsible for receiving, validating, and processing financial transaction messages, primarily in ISO 20022 formats. It persists transaction details and related entity/account information into databases (ArangoDB) and forwards the messages to the Event-Director (via NATS) for further processing or rule evaluation.

### Key Functions:

Accepts specific ISO 20022 messages via HTTP POST requests.
Validates the format and structure of incoming messages against Swagger definitions.
Persists transaction data, account details, and entity information.
Utilizes caching (Redis/Valkey, Node Cache) for performance optimization (especially for Pacs.002 processing).
Publishes received messages to a NATS stream (event-director) for downstream consumption.
Provides health check endpoints.

**Configuration Notes:**

**Quoting Mode (QUOTING env var)**: If set to 'false' (default in .env.template), the endpoints for pain.001 and pain.013 might be effectively disabled or bypassed in certain logic flows, focusing the service on pacs.008 and pacs.002. If 'true', pain.001 and pain.013 are processed.
**Authentication (AUTHENTICATED env var)**: Defaults to false. If set to true, the service expects JWT tokens validated against a public key specified by CERT_PATH_PUBLIC. Unauthorized requests will receive a 401 Unauthorized response.

### 2. API Base

**Scheme**: http (as defined in swagger.yaml)
**Port**: 3000 (default, configurable via PORT env var)
The base URL would typically be http://<host>:<port>.

### 3. Endpoints

### 3.1 Health Checks

GET /
**Summary**: Check the status of the service.
**Description**: If the service is up and running correctly, the response will indicate 'UP'.
**Produces**: application/json
**Responses**:
200 OK: Service is operational.
Body: {"status": "UP"} (Matches Health definition)
500 Internal Server Error: Service is experiencing issues.
Body: (Matches Error definition)

GET /health
**Summary**: Check the status of the service (alternative endpoint).
**Description**: Same as GET /.
**Produces**: application/json
**Responses**:
200 OK: Service is operational.
**Body**: {"status": "UP"} (Matches Health definition)
500 Internal Server Error: Service is experiencing issues.
**Body**: (Matches Error definition)

### 3.2 ISO 20022 Message Evaluation

POST /v1/evaluate/iso20022/pain.001.001.11
**Summary**: Process an ISO 20022 pain.001.001.11 message.
**Description**: Accepts and processes a Customer Credit Transfer Initiation message (pain.001.001.11). Historically related to Mojaloop Quote messages. Processing might be conditional based on the QUOTING environment variable.
**Consumes**: application/json
**Produces**: application/json
Request Body:
Required: true
Schema: ISO20022Pain001 (defined in swagger.yaml)
Sample: <details> <summary>Click to view Pain.001.001.11 Sample</summary>

```json { "CstmrCdtTrfInitn": { "GrpHdr": { "MsgId": "24988b914e3d4cf98a7659b2c45ce063258", "CreDtTm": "2021-12-03T12:40:14.000Z", "NbOfTxs": 1, "InitgPty": { "Nm": "April Blake Grant", "Id": { "PrvtId": { "DtAndPlcOfBirth": { "BirthDt": "1968-02-01", "CityOfBirth": "Unknown", "CtryOfBirth": "ZZ" }, "Othr": [ { "Id": "+27730975224", "SchmeNm": { "Prtry": "MSISDN" } } ] } }, "CtctDtls": { "MobNb": "+27-730975224" } } }, "PmtInf": { "PmtInfId": "5ab4fc7355de4ef8a75b78b00a681ed2569", "PmtMtd": "TRA", "ReqdAdvcTp": { "DbtAdvc": { "Cd": "ADWD", "Prtry": "Advice with transaction details" } }, "ReqdExctnDt": { "Dt": "2021-12-03", "DtTm": "2021-12-03T12:40:14.000Z" }, "Dbtr": { "Nm": "April Blake Grant", "Id": { "PrvtId": { "DtAndPlcOfBirth": { "BirthDt": "1968-02-01", "CityOfBirth": "Unknown", "CtryOfBirth": "ZZ" }, "Othr": [ { "Id": "+27730975224", "SchmeNm": { "Prtry": "MSISDN" } } ] } }, "CtctDtls": { "MobNb": "+27-730975224" } }, "DbtrAcct": { "Id": { "Othr": [ { "Id": "+27730975224", "SchmeNm": { "Prtry": "MSISDN" } } ] }, "Nm": "April Grant" }, "DbtrAgt": { "FinInstnId": { "ClrSysMmbId": { "MmbId": "dfsp001" } } }, "CdtTrfTxInf": { "PmtId": { "EndToEndId": "2c516801007642dfb892944dde1cf845" }, "PmtTpInf": { "CtgyPurp": { "Prtry": "TRANSFER BLANK" } }, "Amt": { "InstdAmt": { "Amt": { "Amt": 31020.89, "Ccy": "USD" } }, "EqvtAmt": { "Amt": { "Amt": 31020.89, "Ccy": "USD" }, "CcyOfTrf": "USD", "XchgRate": 1.00 } }, "ChrgBr": "DEBT", "CdtrAgt": { "FinInstnId": { "ClrSysMmbId": { "MmbId": "dfsp002" } } }, "Cdtr": { "Nm": "Felicia Easton Quill", "Id": { "PrvtId": { "DtAndPlcOfBirth": { "BirthDt": "1935-05-08", "CityOfBirth": "Unknown", "CtryOfBirth": "ZZ" }, "Othr": [ { "Id": "+27707650428", "SchmeNm": { "Prtry": "MSISDN" } } ] } }, "CtctDtls": { "MobNb": "+