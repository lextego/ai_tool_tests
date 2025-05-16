<!--
Documentation research and outputs by LexTego Ltd.
Licensed under the Creative Commons Attribution-ShareAlike 4.0 International License.
See: https://creativecommons.org/licenses/by-sa/4.0/
-->
# Overview

## Introduction

Welcome to the EMMA_event_monitoring_api_dosu wiki! This repository houses the Transaction Monitoring Service (TMS), a critical component for ensuring healthy operations and regulatory compliance. Dive in to learn how TMS processes financial transactions, interacts with various systems, and helps organizations manage risk effectively.

## Description

The EMMA_event_monitoring_api_dosu repository provides a Transaction Monitoring Service (TMS) API. Its primary purpose is to process and validate ISO20022 financial messages (pain.001, pain.013, pacs.008, and pacs.002), store transaction data, and forward transactions to an Event-Director for further processing. The TMS API helps organizations monitor financial transactions for risk management and compliance purposes.

### Key functionalities include:

* ISO20022 Message Processing: Accepts and validates pain.001.001.11, pain.013.001.09, pacs.008.001.10, and pacs.002.001.12 messages. The pain.001 and pain.013 messages can be excluded based on the QUOTING environment variable.
* Data Storage: Saves transaction history, account details, and entity information in an ArangoDB database.
* Event Forwarding: Sends validated transactions to an Event-Director via NATS for subsequent actions.
* Caching: Uses Valkey Cache to store and retrieve Pacs008 messages to optimize Pacs002 processing.
* API Authentication: Supports API authentication using a public key, enabled via the AUTHENTICATED environment variable.

![API](api01.jpg)

## Architecture

The TMS architecture involves several core components working together:

* API Gateway (Fastify): Exposes the API endpoints for receiving ISO20022 messages. It uses Swagger for request validation.
* Logic Service (src/logic.service.ts): Contains the core business logic for processing transactions, interacting with the database, and forwarding events.
* Cache Database Service (src/clients/cache-database.ts): Manages interactions with the ArangoDB database and Valkey Cache.
* Event-Director: Receives validated transactions from TMS via NATS for further processing and analysis.
* ArangoDB: Stores transaction history, account details, and entity information.
* Valkey Cache: Caches Pacs008 messages for faster retrieval during Pacs002 processing.
* NATS: Messaging system used to communicate with the Event-Director.
* APM: Application Performance Monitoring, used for tracing and performance monitoring.

The interaction flow for processing an ISO20022 message is as follows:

1. A client sends an HTTP POST request containing an ISO20022 message to the TMS API.
2. The API gateway validates the request format using Swagger.
3. The Logic Service processes the message, saving relevant data to ArangoDB and Valkey Cache.
4. The Logic Service sends the transaction to the Event-Director via NATS.
5. The API gateway returns a response to the client.

## Usage Instructions

To use the TMS, follow these steps:

1. Installation:
   * Clone the repository: git clone <repository_url>
   * Install dependencies: npm install
1. Configuration:
   * Configure environment variables. Refer to the Dockerfile for a list of available environment variables and their descriptions. Key variables include:
     * `PORT`: The port the service listens on (default: 3000).
     * `QUOTING`: Enables/disables pain.001 and pain.013 message processing (default: `false`).
     * `AUTHENTICATED`: Enables/disables API authentication (default: `false`).
     * `CERT_PATH_PUBLIC`: Path to the public key for authentication.
     * `REDIS_SERVERS`: Redis server connection string.
     * `TRANSACTION_HISTORY_DATABASE_URL`: ArangoDB database URL.
     * `TRANSACTION_HISTORY_DATABASE_USER`: ArangoDB database username.
     * `TRANSACTION_HISTORY_DATABASE_PASSWORD`: ArangoDB database password.
     * `SERVER_URL`: NATS server URL.
     * `PRODUCER_STREAM`: NATS stream name.
   * Create a `.env` file in the root directory and set the required environment variables.
1. Running the Software:
   * Build the application: `npm run build`
   * Start the application: `npm start`
1. API Usage:
    * Send POST requests to the appropriate endpoints with ISO20022 messages in the request body.
    * The available endpoints are:
      * `/v1/evaluate/iso20022/pain.001.001.11`
      * `/v1/evaluate/iso20022/pain.013.001.09`
      * `/v1/evaluate/iso20022/pacs.008.001.10`
      * `/v1/evaluate/iso20022/pacs.002.001.12`
      * 
Refer to the "Pain001 Message" section in the README.md for a sample request body.