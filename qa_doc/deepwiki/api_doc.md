<!--
Documentation research and outputs by LexTego Ltd.
Licensed under the Creative Commons Attribution-ShareAlike 4.0 International License.
See: https://creativecommons.org/licenses/by-sa/4.0/
-->
I'll create an API documentation for the EMMA Event Monitoring API based on the codebase information available.

EMMA Event Monitoring API Documentation
Overview
The EMMA Event Monitoring API is a service that processes and validates ISO20022 financial transaction messages. It provides endpoints for evaluating different types of ISO20022 messages, storing transaction data, and forwarding validated transactions to an event director service.

Base URL
The API server listens on the configured port (specified in the configuration as PORT) and host 0.0.0.0.

Authentication
The API uses route privileges for endpoint access control. Each endpoint has specific privilege requirements defined in the router configuration.

API Endpoints
Health Check Endpoints
GET /
Checks if the service is running properly.

Response:

200 OK: Service is running
{  
  "status": "UP"  
}
GET /health
Alternative health check endpoint.

Response:

200 OK: Service is running
{  
  "status": "UP"  
}
Transaction Processing Endpoints
POST /v1/evaluate/iso20022/pain.001.001.11
Processes a Customer Credit Transfer Initiation (pain.001.001.11) message.

Request Body:

Content-Type: application/json
Schema: ISO20022Pain001 (Customer Credit Transfer Initiation)
Response:

200 OK: Transaction is valid
{  
  "message": "Transaction is valid",  
  "data": { /* Transaction data */ }  
}
400 Bad Request: Invalid request format
401 Unauthorized: Authentication failed
500 Internal Server Error: Processing error
POST /v1/evaluate/iso20022/pain.013.001.09
Processes a Creditor Payment Activation Request (pain.013.001.09) message.

Request Body:

Content-Type: application/json
Schema: ISO20022Pain013 (Creditor Payment Activation Request)
Response:

200 OK: Transaction is valid
{  
  "message": "Transaction is valid",  
  "data": { /* Transaction data */ }  
}
400 Bad Request: Invalid request format
401 Unauthorized: Authentication failed
500 Internal Server Error: Processing error
POST /v1/evaluate/iso20022/pacs.008.001.10
Processes a Financial Institution to Financial Institution Customer Credit Transfer (pacs.008.001.10) message.

Request Body:

Content-Type: application/json
Schema: ISO20022Pacs008 (FI to FI Customer Credit Transfer)
Response:

200 OK: Transaction is valid
{  
  "message": "Transaction is valid",  
  "data": { /* Transaction data */ }  
}
400 Bad Request: Invalid request format
401 Unauthorized: Authentication failed
500 Internal Server Error: Processing error
POST /v1/evaluate/iso20022/pacs.002.001.12
Processes a Payment Status Report (pacs.002.001.12) message.

Request Body:

Content-Type: application/json
Schema: ISO20022Pacs002 (Payment Status Report)
Response:

200 OK: Transaction is valid
{  
  "message": "Transaction is valid",  
  "data": { /* Transaction data */ }  
}
400 Bad Request: Invalid request format
401 Unauthorized: Authentication failed
500 Internal Server Error: Processing error
Request and Response Schemas
The API uses JSON schemas for validating request and response bodies. These schemas are defined in the src/schemas directory and are based on ISO20022 message formats.

Pain.001.001.11 (Customer Credit Transfer Initiation)
swagger.yaml:565-569
Pain.013.001.09 (Creditor Payment Activation Request)
This schema represents a creditor-initiated payment request.

Pacs.008.001.10 (FI to FI Customer Credit Transfer)
This schema represents a transfer between financial institutions.

Pacs.002.001.12 (Payment Status Report)
This schema represents a payment status report.

Error Handling
The API returns standard HTTP status codes to indicate the success or failure of a request:

200 OK: The request was successful
400 Bad Request: The request was malformed or contained invalid data
401 Unauthorized: Authentication failed
500 Internal Server Error: An error occurred while processing the request
Error responses include a message describing the error:

{  
  "message": "Failed to process execution request.",  
  "error": { /* Error details */ }  
}
API Implementation Details
Transaction Processing Flow
The API receives a transaction message via one of the endpoints
The message is validated against the appropriate JSON schema
The transaction data is processed and stored in the database
Transaction relationships are created and stored
The processed transaction is sent to the event director service
A success response is returned to the client
Database Operations
The API uses a cache database service for data persistence:

Transaction history is stored in ArangoDB
Transaction data is cached in Redis for quick retrieval
Account and entity information is stored for relationship tracking
Monitoring and Logging
The API includes comprehensive monitoring and logging:

APM (Application Performance Monitoring) spans track performance
Detailed logging of transaction processing steps
Error logging with context information
API Documentation Access
The API includes Swagger documentation accessible at:

/documentation: Swagger UI for interactive API documentation
/swagger: Raw Swagger specification fastify.ts:37-46
CORS Configuration
The API is configured with CORS to allow cross-origin requests: fastify.ts:71-75

Notes
The API is part of the Tazama Transaction Monitoring Service
It processes ISO20022 financial transaction messages
The QUOTING configuration determines which transaction types are supported
The API integrates with external systems like the event director service via NATS
Notes: This API documentation is based on the available code snippets from the EMMA Event Monitoring API repository. The documentation covers the main endpoints, request/response formats, and processing flow. The swagger.yaml file provides detailed schema information for the API endpoints, and the fastify.ts file shows how the API server is configured with Swagger documentation and CORS support.

Wiki pages you might want to explore:

GitHub Actions Workflows (lextego/EMMA_event_monitoring_api)