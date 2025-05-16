<!--
Documentation research and outputs by LexTego Ltd.
Licensed under the Creative Commons Attribution-ShareAlike 4.0 International License.
See: https://creativecommons.org/licenses/by-sa/4.0/
-->
# SPDX-License-Identifier: Apache-2.0

# Folders and files to ignore when building the Docker image.
# This helps keep the image size small and avoids including unnecessary files.

# Node.js dependencies folder
node_modules

# Code coverage reports folder
coverage

# Template folders (often used for scaffolding or examples)
template
templates

# VSCode specific settings folder
.vscode

# Project documentation file (already present in the repository, no need to copy into the image)
README.md
# SPDX-License-Identifier: Apache-2.0
# EditorConfig helps maintain consistent coding styles for multiple developers working on the same project across various editors and IDEs.
# https://editorconfig.org

# Indicates this is the root EditorConfig file. EditorConfig clients will stop searching for .editorconfig files in parent directories.
root = true

# Apply these settings to all files
[*]
# Use spaces for indentation
indent_style = space
# Set indentation size to 2 spaces
indent_size = 2
# Set character set to UTF-8
charset = utf-8
# Remove whitespace characters from the end of lines
trim_trailing_whitespace = true
# Ensure files end with a newline character
insert_final_newline = true
# Use Line Feed (LF) as the end-of-line character
end_of_line = lf

# Override settings specifically for Markdown files
[*.md]
# Do not trim trailing whitespace in Markdown files (often significant)
trim_trailing_whitespace = false
# SPDX-License-Identifier: Apache-2.0
# Template for environment variables. Copy this file to .env and fill in the values for local development.
# Do NOT commit the actual .env file to version control.

# --- General Service Configuration ---
# Name of the function/service, used for identification (e.g., logging, APM)
FUNCTION_NAME=transaction-monitoring-service
# Node.js environment (e.g., dev, test, production)
NODE_ENV=dev
# Maximum number of CPU cores the process should use (relevant for clustering)
MAX_CPU=1

# --- NATS Configuration (Messaging System) ---
# URL of the NATS server(s)
SERVER_URL=0.0.0.0:4222
# Name of the NATS stream used for producing messages
PRODUCER_STREAM=event-director
# Defines how the service starts up (e.g., listening to NATS or HTTP)
STARTUP_TYPE=nats # Options: 'nats', 'http'

# --- Fastify Configuration (HTTP Framework) ---
# Port for the HTTP server to listen on (if STARTUP_TYPE is 'http')
PORT=3000

# --- Miscellaneous Configuration ---
# Cache Time-To-Live (TTL) in seconds for local data cache objects. 0 means cache forever.
CACHETTL=0
# Flag to indicate if quoting logic (related to pain.001/pain.013) is enabled
QUOTING='false' # Set to 'true' to enable quoting flow

# --- Authentication Configuration ---
# Path to the public certificate file for validating JWT tokens (if AUTHENTICATED is true)
CERT_PATH_PUBLIC=
# Flag to enable/disable API authentication
AUTHENTICATED=false # Set to 'true' to require authentication

# --- Redis Cache Configuration ---
# Redis database number to use
REDIS_DATABASE=0
# Authentication password for Redis
REDIS_AUTH="exampleAuth"
# Redis server connection details (JSON array of objects)
REDIS_SERVERS='[{"host":"127.0.0.1", "port":6379}, {"host":"127.0.0.1", "port":6380}]'
# Flag indicating if Redis is running in cluster mode
REDIS_IS_CLUSTER=false
# TTL in seconds for the distributed (Redis) cache
DISTRIBUTED_CACHETTL=300
# Flag to enable/disable the distributed (Redis) cache
DISTRIBUTED_CACHE_ENABLED=true

# --- Node Cache (In-Memory) Configuration ---
# TTL in seconds for the local (in-memory) cache
LOCAL_CACHETTL=300
# Flag to enable/disable the local (in-memory) cache
LOCAL_CACHE_ENABLED=true

# --- ArangoDB Configuration (Transaction History Database) ---
# Name of the database for transaction history
TRANSACTION_HISTORY_DATABASE=transactionHistory
# Connection URL for the transaction history database
TRANSACTION_HISTORY_DATABASE_URL=tcp://0.0.0.0:8529
# Username for the transaction history database
TRANSACTION_HISTORY_DATABASE_USER=root
# Password for the transaction history database
TRANSACTION_HISTORY_DATABASE_PASSWORD=''
# Path to the CA certificate file for secure connection (if needed)
TRANSACTION_HISTORY_DATABASE_CERT_PATH=

# --- ArangoDB Configuration (Pseudonyms Database) ---
# Name of the database for pseudonyms
PSEUDONYMS_DATABASE=pseudonyms
# Connection URL for the pseudonyms database
PSEUDONYMS_DATABASE_URL=tcp://0.0.0.0:8529
# Username for the pseudonyms database
PSEUDONYMS_DATABASE_USER=root
# Password for the pseudonyms database
PSEUDONYMS_DATABASE_PASSWORD=''
# Path to the CA certificate file for secure connection (if needed)
PSEUDONYMS_DATABASE_CERT_PATH=

# --- Elastic APM (Application Performance Monitoring) Configuration ---
# Flag to enable/disable APM agent
APM_ACTIVE=false
# Service name reported to APM
APM_SERVICE_NAME=transaction-monitoring-service
# URL of the APM server
APM_URL=http://apm:8200
# Secret token for authenticating with the APM server
APM_SECRET_TOKEN=''

# --- Logging Configuration ---
# Hostname of the Logstash server
LOGSTASH_HOST=logstashhost
# Port of the Logstash server
LOGSTASH_PORT=8080
# Minimum log level to send to Logstash (e.g., 'info', 'warn', 'error')
LOGSTASH_LEVEL='info'
# Host and port for the sidecar service (if used)
SIDECAR_HOST=0.0.0.0:5000
# SPDX-License-Identifier: Apache-2.0

# General logs
logs
*.log
# Node.js specific debug logs
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Runtime data files
pids
*.pid
*.seed
*.pid.lock

# Directory for instrumented libs generated by jscoverage/JSCover (older coverage tool)
lib-cov

# Coverage directory used by tools like istanbul/nyc
coverage

# nyc test coverage intermediate output
.nyc_output

# Grunt intermediate storage (build tool)
.grunt

# Bower dependency directory (front-end package manager)
bower_components

# node-waf configuration (native addon build tool)
.lock-wscript

# Compiled binary addons output directory
build/Release
build # Also ignore the main build output directory

# Dependency directories
node_modules/
jspm_packages/ # JSPM package manager directory

# TypeScript v1 declaration files directory (typings tool)
typings/

# Optional npm cache directory
.npm

# Optional eslint cache file
.eslintcache

# Eslint configuration file (often committed, but can be ignored if generated)
# .eslintrc.json # Commented out as it's usually tracked

# Optional REPL (Read-Eval-Print Loop) history file
.node_repl_history

# Output of 'npm pack' command (creates tarballs)
*.tgz

# Yarn Integrity file (used by older Yarn versions)
.yarn-integrity

# dotenv environment variables file (contains secrets, should NOT be committed)
.env

# Next.js build output directory
.next

# Katalon test profiles directory (testing tool)
Katalon Tests/Profiles/

# Template directory (if used for generation and not part of source)
template

# Certificate files (often sensitive or environment-specific)
*.crt
# SPDX-License-Identifier: Apache-2.0

# Configure the scope @tazama-lf to use the GitHub Packages registry.
@tazama-lf:registry=https://npm.pkg.github.com

# Set the authentication token for accessing the GitHub Packages registry.
# The ${GH_TOKEN} variable should be set in the environment (e.g., CI/CD pipeline).
//npm.pkg.github.com/:_authToken=${GH_TOKEN}
# SPDX-License-Identifier: Apache-2.0

# Specifies files and directories that Prettier should ignore when formatting code.

# Ignore build artifacts:
build
coverage

# Ignore generated model files (if they are auto-generated and shouldn't be formatted)
src/models
# SPDX-License-Identifier: Apache-2.0
# Configuration file for SonarCloud analysis.

# Exclude test files from SonarCloud analysis metrics (coverage, duplication, etc.)
# This is common practice as test code often has different quality standards.
sonar.exclusions=**/__tests__/**/*
# SPDX-License-Identifier: Apache-2.0

# Changelog for the Transaction Monitoring Service

## v1.2.0 (future date, 2024)

*   Next change summary here

## v1.4.0 (June 14th, 2024)

*   Release last version.
    *   (Add specific changes for v1.4.0 here if known)
```Dockerfile

Specify the Node.js version and base OS image for the build stage.
Using a specific version (node:20-bullseye) ensures reproducibility.
ARG BUILD_IMAGE=node:20-bullseye

Specify the minimal base image for the runtime stage.
Distroless images contain only the application and its runtime dependencies.
ARG RUN_IMAGE=gcr.io/distroless/nodejs20-debian11:nonroot

--- Build Stage ---
Use the build image defined above.
FROM ${BUILD_IMAGE} AS builder

Label this stage for clarity.
LABEL stage=build

This stage compiles TypeScript to JavaScript.
Set the working directory inside the container.
WORKDIR /home/app

Copy source code into the container.
COPY ./src ./src

Copy package manager files.
COPY ./package*.json ./

Copy TypeScript configuration file.
COPY ./tsconfig.json ./

Copy Swagger API definition file.
COPY ./swagger.yaml ./

Copy npm configuration file (needed for private packages).
COPY .npmrc ./

Argument to pass the GitHub token for accessing private npm packages during build.
ARG GH_TOKEN

Install all dependencies (including devDependencies) defined in package-lock.json.
--ignore-scripts skips potentially unsafe lifecycle scripts during install.
RUN npm ci --ignore-scripts

Compile TypeScript code to JavaScript based on tsconfig.json.
RUN npm run build

--- Dependency Resolver Stage ---
Use the build image again for installing production dependencies.
FROM ${BUILD_IMAGE} AS dep-resolver

Label this stage.
LABEL stage=pre-prod

This stage installs only production dependencies to keep the final image small.
Copy package manager files.
COPY package*.json ./

Copy npm configuration file.
COPY .npmrc ./

Argument for the GitHub token.
ARG GH_TOKEN

Install only production dependencies.
--omit=dev skips devDependencies.
RUN npm ci --omit=dev --ignore-scripts

--- Runtime Stage ---
Use the minimal distroless image defined earlier.
FROM ${RUN_IMAGE} AS run-env

Switch to the non-root user defined in the distroless image for security.
USER nonroot

Set the working directory.
WORKDIR /home/app

Copy production node_modules from the dep-resolver stage.
COPY --from=dep-resolver /node_modules ./node_modules

Copy compiled JavaScript code from the builder stage.
COPY --from=builder /home/app/build ./build

Copy package.json (might be needed for metadata or runtime scripts).
COPY package.json ./

Copy Kubernetes service definition (informational, not directly used by the container).
COPY service.yaml ./

Copy Kubernetes deployment definition (informational).
COPY deployment.yaml ./

Set npm log level to 'warn' to reduce noise in production logs.
ENV NPM_CONFIG_LOGLEVEL warn

--- Default Environment Variables for the Container ---
These can be overridden during container runtime (e.g., via docker run -e or Kubernetes config).
Watchdog/Process manager related variables (if applicable, seems like defaults for a specific setup)
ENV mode="http" ENV upstream_url="http://127.0.0.1:3000" ENV exec_timeout="10s" ENV write_timeout="15s" ENV read_timeout="15s" ENV prefix_logs="false"

Service Based variables
ENV FUNCTION_NAME=transaction-monitoring-service ENV NODE_ENV=production # Set environment to production ENV PORT=3000 # Default port for the service ENV QUOTING=false # Default quoting behavior ENV SERVER_URL= # NATS Server URL (needs to be provided at runtime) ENV MAX_CPU= # Max CPU (needs to be provided or defaults based on system)

Auth
ENV AUTHENTICATED=false # Authentication disabled by default ENV CERT_PATH_PUBLIC= # Path to public cert (required if AUTHENTICATED=true)

Redis
ENV REDIS_DATABASE=0 ENV REDIS_AUTH= # Redis password (provide at runtime if needed) ENV REDIS_SERVERS= # Redis server list (provide at runtime) ENV REDIS_IS_CLUSTER= # Redis cluster mode (provide at runtime) ENV DISTRIBUTED_CACHETTL=300 ENV DISTRIBUTED_CACHE_ENABLED=true

NodeCache (In-memory)
ENV LOCAL_CACHETTL=300 ENV LOCAL_CACHE_ENABLED=true

Nats
ENV SERVER_URL=0.0.0.0:4222 # Default NATS URL (likely overridden) ENV STARTUP_TYPE=nats # Default startup mode ENV PRODUCER_STREAM= # NATS Stream name (provide at runtime) ENV ACK_POLICY=Explicit # NATS Acknowledgement policy ENV PRODUCER_STORAGE=File # NATS Stream storage type ENV PRODUCER_RETENTION_POLICY=Workqueue # NATS Stream retention policy

Database (Transaction History)
Default path for CA cert within the container (volume mount needed if used)
ENV TRANSACTION_HISTORY_DATABASE_CERT_PATH='/usr/local/share/ca-certificates/ca-certificates.crt' ENV TRANSACTION_HISTORY_DATABASE_URL= # DB URL (provide at runtime) ENV TRANSACTION_HISTORY_DATABASE_USER='root' ENV TRANSACTION_HISTORY_DATABASE_PASSWORD= # DB Password (provide at runtime) ENV TRANSACTION_HISTORY_DATABASE='transactionHistory'

Database (Pseudonyms)
ENV PSEUDONYMS_DATABASE_CERT_PATH= # Path to cert (provide if needed) ENV PSEUDONYMS_DATABASE='pseudonyms' ENV PSEUDONYMS_DATABASE_USER='root' ENV PSEUDONYMS_DATABASE_URL= # DB URL (provide at runtime) ENV PSEUDONYMS_DATABASE_PASSWORD= # DB Password (provide at runtime)

Apm
ENV APM_ACTIVE=true # APM enabled by default in production image ENV APM_SERVICE_NAME=transaction-monitoring-service ENV APM_URL=http://apm-server.development.svc.cluster.local:8200/ # Default APM URL (likely overridden) ENV APM_SECRET_TOKEN= # APM Token (provide at runtime if needed)

Logstash
ENV LOGSTASH_HOST=logstash.development.svc.cluster.local # Default Logstash host (likely overridden) ENV LOG