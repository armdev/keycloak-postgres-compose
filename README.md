```markdown
# PostgreSQL 16 Cluster & Keycloak Setup

This project sets up a PostgreSQL 16 database cluster alongside Keycloak for identity and access management. Both services are containerized using Docker, making it easy to deploy and manage.

## Prerequisites
- Docker installed on your machine
- Docker Compose installed (if not included with Docker)

## Running the Cluster

You can start the cluster by running the provided script or using Docker Compose:

### Option 1: Run with Script
```bash
./run.sh
```

### Option 2: Run with Docker Compose
```bash
docker compose --compatibility up -d --build
```

This command builds the images and starts the services in detached mode.

## Viewing Logs

To follow the logs of the running services, use the following commands:

### PostgreSQL Logs
```bash
docker logs --follow postgresql
```

### Keycloak Logs
```bash
docker logs --follow keycloak
```

## Accessing Keycloak

- **URL**: [http://localhost:9080](http://localhost:9080)
- **Admin Credentials**: 
  - **Username**: `admin`
  - **Password**: `admin`

### OpenID Connect Configuration

You can find the OpenID configuration endpoint here:

[http://localhost:9080/realms/master/.well-known/openid-configuration](http://localhost:9080/realms/master/.well-known/openid-configuration)

### Keycloak REST API Documentation

For more information on Keycloak's REST API, refer to the official documentation:

[https://www.keycloak.org/docs-api/latest/rest-api/index.html](https://www.keycloak.org/docs-api/latest/rest-api/index.html)

## Accessing PostgreSQL via pgAdmin

- **pgAdmin URL**: [http://localhost:5050/browser/](http://localhost:5050/browser/)
- **pgAdmin Credentials**: 
  - **Username**: `admin@gmail.com`
  - **Password**: `admin`

## Stopping the Cluster

To stop the running services, use the following command:
```bash
docker compose down
```

## Additional Information

- **PostgreSQL Version**: 16
- **Keycloak Version**: Latest
- **Ports**:
  - PostgreSQL: `5432`
  - Keycloak: `9080`
  - pgAdmin: `5050`

This setup provides a complete development environment for working with PostgreSQL and Keycloak. You can customize the configuration as needed for production environments.
```



### Important
 - Deployment with PostgreSQL 17 and Keycloak 26.0 failed
