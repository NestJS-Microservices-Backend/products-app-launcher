# Products App Launcher

This project is a backend microservices application orchestrated with Docker Compose. It includes services for products, orders, a client gateway, and a NATS messaging server.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/) must be installed on your system.

### Installation

1.  **Clone the repository:**
    ```sh
    git clone <repository-url>
    cd products-app-launcher
    ```

2.  **Set up environment variables:**
    Create a `.env` file by copying the template:
    ```sh
    cp .template.env .env
    ```
    You can modify the `CLIENT_GATEWAY_PORT` in the `.env` file if needed. The default is `3010`.

## Running the Application

To start all the services in detached mode, run the following command from the root of the project:

```sh
docker-compose up --build
```

The services will be built and started as defined in the `docker-compose.yml` file.

## Services

The application is composed of the following services:

-   **`client-gateway`**: The main entry point for client requests. It communicates with other microservices.
    -   Port: `${CLIENT_GATEWAY_PORT}` (default: 3010)
-   **`products-ms`**: Manages product-related operations.
-   **`orders-ms`**: Manages order-related operations. It uses a PostgreSQL database.
-   **`nats-server`**: A NATS messaging server for inter-service communication.
    -   Port: `8222` (for monitoring)
-   **`orders-db`**: A PostgreSQL database for the Orders microservice.
    -   Port: `5432`

## Stopping the Application

To stop all the running services, use the command:

```sh
docker-compose down
```
