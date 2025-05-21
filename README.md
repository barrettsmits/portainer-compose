# portainer-compose
Portianer docker compose repository for my homelab
## Overview
This repository contains Docker Compose configurations for various services running in my homelab, managed through Portainer.

## Structure
- `docker-compose/individual/` - Contains individual service configurations
  - `example.yml` - Template for new service configurations
  - Other service-specific compose files (gitignored for security)

## Applications
This Portainer Compose repository includes docker Compose for the follow applications:

### FoundryVTT
- Virtual Tabletop server running on port 32000
- Uses the felddy/foundryvtt:release image
- Persistent data stored in `/portainer/Files/AppData/Config/foundryvtt`

### DuckDNS
- Dynamic DNS service for domain updates
- Uses linuxserver/duckdns image
- Configured for devopsfables.duckdns.org

### SonarQube
- Code quality and security analysis platform
- Uses sonarqube:latest image
- Runs on port 9000
- Persistent data stored in NFS volume

### TeslaMate
- Tesla logging and analytics platform
- Uses teslamate/teslamate:latest image
- Runs on port 4000
- Requires database configuration
- Persistent data stored in NFS volume

### Prometheus
- Monitoring and alerting system
- Uses prom/prometheus:latest image
- Runs on port 9090
- Custom configuration via prometheus.yml
- Persistent data stored in NFS volume

### Grafana
- Data visualization and monitoring platform
- Uses grafana/grafana:latest image
- Runs on port 3000
- Persistent data stored in NFS volume

## Environment Variables
The following environment variables are required:
- `FOUNDRY_LICENSE_KEY` - License key for FoundryVTT
- `DUCKDNS_TOKEN` - Authentication token for DuckDNS service
- `SONARQUBE_JDBC_URL` - JDBC URL for SonarQube database connection
- `SONARQUBE_JDBC_USERNAME` - Username for SonarQube database
- `SONARQUBE_JDBC_PASSWORD` - Password for SonarQube database
- `TESLAMATE_DATABASE_URL` - Database URL for TeslaMate
- `TESLAMATE_DATABASE_USER` - Username for TeslaMate database
- `TESLAMATE_DATABASE_PASSWORD` - Password for TeslaMate database
- `PROMETHEUS_STORAGE_PATH` - Path for Prometheus data storage
- `GRAFANA_ADMIN_USER` - Admin username for Grafana
- `GRAFANA_ADMIN_PASSWORD` - Admin password for Grafana

## Network Configuration
Services are configured to use the `nginx-network` for reverse proxy capabilities.

## Security Notes
- Sensitive configuration files and environment variables are gitignored
- Individual service configurations are excluded from version control (except example.yml)
- Environment variables containing sensitive data are stored in `.env` files

## Usage
1. Clone this repository
2. Create necessary `.env` files with required variables
3. Deploy services through Portainer using the compose files


## Auto-Generating Docker Compose Files
You can automatically generate a `docker-compose.yml` file for a running container using the following command:

```bash
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock ghcr.io/red5d/docker-autocompose <container-name-or-id>
```

Replace `<container-name-or-id>` with the name or ID of the container for which you want to generate the compose file. This tool will output a `docker-compose.yml` file that you can use to recreate the container configuration.
