# Products App Launcher

This project orchestrates a backend microservices application using Docker Compose. The architecture is designed for scalability and separation of concerns, featuring dedicated services for products, orders, payments, authentication, and a client-facing API gateway. Communication between services is handled via a NATS messaging server.

## Architecture Overview

The application is composed of the following services:

-   **`client-gateway`**: The main entry point for all client requests. It acts as a reverse proxy, routing traffic to the appropriate microservice.
-   **`products-ms`**: Manages all product-related operations, including creation, retrieval, updates, and deletion.
-   **`orders-ms`**: Manages all order-related operations. It communicates with the products service to validate items and uses its own PostgreSQL database for data persistence.
-   **`payments-ms`**: Responsible for processing payments and handling payment-related events.
-   **`auth-ms`**: Handles user authentication, token generation, and verification.
-   **`nats-server`**: A lightweight messaging server for high-performance, asynchronous communication between the microservices.
-   **`orders-db`**: A PostgreSQL database instance dedicated to the Orders microservice.

## Project Structure

This repository uses **Git Submodules** to manage the microservices. Each service (`client-gateway`, `products-ms`, `orders-ms`, `payments-ms`, `auth-ms`) is a separate repository included here as a submodule. This approach allows for independent development and versioning of each microservice.

## Getting Started

Follow these instructions to get the project running on your local machine.

### Prerequisites

-   [Docker](https://docs.docker.com/get-docker/)
-   [Docker Compose](https://docs.docker.com/compose/install/)
-   [Git](https://git-scm.com/downloads)

### Installation & Setup

1.  **Clone the repository:**
    ```sh
    git clone <repository-url>
    cd products-app-launcher
    ```

2.  **Initialize and update Git Submodules:**
    This command clones the source code for all the microservices.
    ```sh
    git submodule update --init --recursive
    ```

3.  **Set up environment variables:**
    Create a `.env` file by copying the provided template. This file contains the configuration for the client gateway port.
    ```sh
    cp .template.env .env
    ```
    You can modify the `CLIENT_GATEWAY_PORT` in the `.env` file if needed (default is `3010`). Each microservice also contains its own `.template.env` for further configuration.

## Running the Application

To build and start all services in detached mode, run the following command from the project root:

```sh
docker-compose up --build
```

The services will be available at the following ports:

-   **Client Gateway**: `http://localhost:${CLIENT_GATEWAY_PORT}` (default: `3010`)
-   **NATS Monitoring**: `http://localhost:8222`
-   **Orders DB (PostgreSQL)**: `localhost:5432`

## Stopping the Application

To stop all running services and remove the containers, use the command:

```sh
docker-compose down
```
