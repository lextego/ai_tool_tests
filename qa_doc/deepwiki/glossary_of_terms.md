<!--
Documentation research and outputs by LexTego Ltd.
Licensed under the Creative Commons Attribution-ShareAlike 4.0 International License.
See: https://creativecommons.org/licenses/by-sa/4.0/
-->
I'll create a glossary of terms for the EMMA Event Monitoring API based on the codebase information available.

EMMA Event Monitoring API - Glossary of Terms
ISO20022 Message Types
Pain.001.001.11
Customer Credit Transfer Initiation - A message sent by a customer to initiate a credit transfer to another party. Contains details about the debtor (sender), creditor (receiver), and payment information. swagger.yaml:565-569

Pain.013.001.09
Creditor Payment Activation Request - A message initiated by a creditor to request a payment from a debtor. This is essentially a "pull" payment request as opposed to the "push" model of Pain.001. swagger.yaml:1807-1814

Pacs.008.001.10
Financial Institution to Financial Institution Customer Credit Transfer - A message used between financial institutions to transfer funds on behalf of customers. Historically used in Mojaloop for transfer messages. swagger.yaml:93-96

Pacs.002.001.12
Payment Status Report - A message used to report on the status of a payment instruction. Contains information about whether a payment was accepted, rejected, or is in another state. swagger.yaml:983-988

Transaction Components
MsgId
Message Identifier - A unique identifier for a transaction message. pacs.002.json:10-12

CreDtTm
Creation Date Time - The timestamp when the transaction message was created. pacs.002.json:13-15

EndToEndId
End-to-End Identifier - A reference number that remains with a transaction throughout its lifecycle, allowing it to be tracked across different systems. swagger.yaml:1016-1020

TxSts
Transaction Status - The status of a transaction, which can be one of several predefined values (e.g., ACCC, ACCP, RJCT). swagger.yaml:1021-1024

Amt
Amount - The monetary value of the transaction. pacs.002.json:43-45

Ccy
Currency - The currency code for the transaction amount (e.g., USD, EUR). pacs.002.json:46-48

InstdAmt
Instructed Amount - The amount of money to be moved between the debtor and creditor, before deduction of charges. swagger.yaml:2079-2092

IntrBkSttlmAmt
Interbank Settlement Amount - The amount of money moved between financial institutions. swagger.yaml:462

XchgRate
Exchange Rate - The rate at which one currency is exchanged for another in a transaction involving different currencies. swagger.yaml:328-330

Party Identifiers
Dbtr
Debtor - The party from whose account the money is debited. swagger.yaml:466

Cdtr
Creditor - The party to whose account the money is credited. swagger.yaml:470

DbtrAcct
Debtor Account - The account from which the payment is made. swagger.yaml:467

CdtrAcct
Creditor Account - The account to which the payment is made. swagger.yaml:471

DbtrAgt
Debtor Agent - The financial institution servicing the debtor's account. swagger.yaml:468

CdtrAgt
Creditor Agent - The financial institution servicing the creditor's account. swagger.yaml:469

FinInstnId
Financial Institution Identifier - Identifies a financial institution. pacs.002.json:58-60

ClrSysMmbId
Clearing System Member Identifier - Identifies a member of a clearing system. pacs.002.json:163-173

MmbId
Member Identifier - The identifier of a member in a clearing system, often used to identify financial institutions in a payment system. pacs.002.json:166-168

Supplementary Data
SplmtryData
Supplementary Data - Additional information included in a transaction message. swagger.yaml:502-510

Glctn
Geolocation - Geographic coordinates (latitude and longitude) associated with a transaction. swagger.yaml:974-982

Lat
Latitude - The geographic latitude coordinate. swagger.yaml:977-979

Long
Longitude - The geographic longitude coordinate. swagger.yaml:980-982

System Components
CacheDatabaseService
A service that manages data persistence in both a database and a cache system, providing methods to store and retrieve transaction data.

DataCache
A structure that holds key transaction data for quick access, including debtor and creditor information.

TransactionRelationship
A structure that defines the relationship between accounts involved in a transaction, including the direction of money flow and transaction details.

APM
Application Performance Monitoring - A system used to track the performance of transaction processing through spans and metrics.

NATS
A messaging system used for communication between the EMMA API and the Event Director service.

Transaction Status Codes
ACCC
Accept Credit Completion - Settlement on the creditor's account has been completed.

ACCP
Accept Credit Clearing - Payment has been accepted for clearing.

ACSC
Accept Settlement Completed - Settlement on the debtor's account has been completed.

ACSP
Accept Settlement in Process - All preceding checks such as technical validation and customer profile were successful.

ACTC
Accept Technical Validation - Authentication and syntactical and semantic validation are successful.

RJCT
Reject - Payment has been rejected.

Notes
This glossary covers the key terms found in the EMMA Event Monitoring API codebase, focusing on ISO20022 message types, transaction components, party identifiers, and system components. The terms are derived from the JSON schemas and Swagger documentation in the repository, which define the structure and validation rules for the API's request and response bodies.