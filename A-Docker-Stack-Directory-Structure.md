# Appendix A: Docker Stack Directory Structure

- [A.1. Main Directory Structure](#a1-main-directory-structure)
- [A.2. Grafana Directory](#a2-grafana-directory)
- [A.3. Nginx Directory](#a3-nginx-directory)
- [A.4. VSCode Directory](#a4-vscode-directory)



This appendix offers an organized breakdown of our Docker stack directory structure, delineating the function and organization of each component.

```
├── grafana
│   ├── dashboards
│   │   ├── dashboard-coinbase-matches.json
│   │   ├── dashboard-coinbase-trades.json
│   │   ├── dashboard-gps-tracker.json
│   │   └── dashboard-weather-station.json
│   ├── docs
│   │   └── assets
│   │       └── datasource
│   │           └── questdb_configuration.png
│   ├── provisioning
│   │   ├── dashboards
│   │   │   └── file.yaml
│   │   └── datasources
│   │       └── questdb.yml
│   └── README.md
├── nginx
│   ├── .well-known
│   │   └── .gitkeep
│   ├── certs
│   │   └── dhparam.pem
│   ├── conf.d
│   │   ├── default.conf
│   │   └── default.conf.template
│   ├── .htpasswd
│   ├── nginx.conf
│   └── nginx.env
├── vscode
│   ├── Dockerfile
│   ├── README.md
│   └── requirements.txt
├── docker-compose.yaml
├── init.yaml
└── README.md
```


# A.1. Main Directory Structure

- `docker-compose.yaml`: Contains the configuration for deploying the Docker services.
- `init.yaml`: Initial configuration file.
- `README.md`: Main documentation for the Docker stack.

## `docker-compose.yaml`

The `docker-compose.yaml` file defines multi-container Docker applications using Docker Compose. This configuration file describes services, networks, and volumes for the Docker stack.

### Services:

**1. VSCode Service (`vscode`):**

- **build**: 
  - `context`: Specifies the directory containing the Dockerfile.
  - `dockerfile`: Name of the Dockerfile.
- **ports**: Maps the container's port 8080 to the host's port 8080.
- **volumes**: 
  - Mounts the parent directory's `notebooks` folder to the `/home/coder/project` directory inside the container.
- **environment**: Sets the environment variable `PASSWORD` to `yourpassword`.
- **devices**: 
  - Maps I2C and Serial Interfaces inside the container to interact with the BME680 sensor and QUECTEL EG25-G 4G HAT cellular device.

**2. Grafana Service (`grafana`):**

- **image**: Uses the `grafana/grafana:9.5.1` Docker image.
- **ports**: Maps the container's port 3000 to the host's port 3000.
- **volumes**: 
  - Mounts several directories and named volumes for data persistence and configuration.
- **depends_on**: Specifies that the Grafana service depends on the `questdb` service.
- **environment**: Sets specific environment variables for Grafana configurations.

**3. QuestDB Service (`questdb`):**

- **image**: Uses the `questdb/questdb:7.3` Docker image.
- **ports**: Maps multiple ports between the container and the host for various QuestDB functionalities.
- **volumes**: 
  - Mounts the named volume `questdb-data` to the specified path in the container.
- **environment**: Sets specific environment variables for QuestDB configurations.

**4. Nginx Service (`nginx`):**

- **image**: Uses the `nginx:stable` Docker image.
- **volumes**: 
  - Mounts configuration files, SSL certificates, and other necessary data for the Nginx service.
- **ports**: Maps ports 80 and 443 between the container and the host.
- **env_file**: Loads environment variables from the `nginx.env` file.
- **command**: Executes a command on startup to handle Nginx configurations and then runs Nginx.
- **depends_on**: Specifies dependencies on other services: `vscode`, `grafana`, and `questdb`.

**5. Certbot Service (`certbot`):**

- **image**: Uses the `certbot/certbot` Docker image.
- **ports**: No ports are mapped.
- **volumes**: 
  - Mounts directories related to SSL certificates and letsencrypt configurations.

### Volumes:

- **grafana-data**: Named volume for persisting Grafana data.
- **questdb-data**: Named volume for persisting QuestDB data.



## `init.yaml`

The `init.yaml` file is designed to set up the initial SSL certificate generation using Certbot for your Docker stack. 

#### Services:

**Certbot Service (`certbot`):**

- **image**: Utilizes the `certbot/certbot` Docker image.

- **network_mode**: Operates in the host network mode. This means the Certbot service will share the network namespace with the host, making it equivalent to running the container's process directly on the host itself.

- **volumes**: 
  - Maps the host's letsencrypt directories to the container. These directories store generated SSL certificates and associated configurations.
  - Maps the `./nginx/.well-known/` directory from the host to the `/usr/share/nginx/html/.well-known/` directory inside the container. This directory is often used for domain validation during the SSL certificate generation process.

## `README.md`

The `README.md` provides an overview and access details of the Docker services set up in the repository.

---

#### **Docker Overview**

In this section, a brief overview is given about the Docker services present within the directory.

---

#### **Services**

This section elaborates on each individual service, including relevant links, access details, and configuration instructions.

**1. VSCode Service:**

- **Docker Image**: [codercom/code-server on Docker Hub](https://hub.docker.com/r/codercom/code-server)
  
- **GitHub Repository**: [code-server on GitHub](https://github.com/coder/code-server)
  
- **Access**: Navigate to [localhost:8080](http://localhost:8080) to access the VSCode service.

- **Authentication**: 
  - The default password for accessing the VSCode service is `yourpassword`.
  - This password can be modified within the [docker-compose.yaml file](docker-compose.yaml).
  
- **Configuration**: For configuring the VSCode service, refer to the [VSCode documentation](./vscode/README.md).

---

**2. QuestDB Service:**

- **Docker Image**: [questdb/questdb on Docker Hub](https://hub.docker.com/r/questdb/questdb)
  
- **GitHub Repository**: [questdb on GitHub](https://github.com/questdb/questdb)
  
- **Additional Documentation**: [QuestDB Docker Documentation](https://questdb.io/docs/get-started/docker/)
  
- **Access**: 
  - Access the QuestDB GUI via [localhost:9000](http://localhost:9000).
  - Database can be accessed at [localhost:8812](http://localhost:8812).
  
- **Authentication**: 
  - Default credentials are `admin:quest` for the QuestDB service.
  - Further details can be found in the [QuestDB documentation](https://questdb.io/docs/reference/configuration/#postgres-wire-protocol), and the default database name is `qdb`.

---

**3. Grafana Service:**

- **Docker Image**: [grafana/grafana on Docker Hub](https://hub.docker.com/r/grafana/grafana)
  
- **GitHub Repository**: [Grafana on GitHub](https://github.com/grafana/grafana)
  
- **Access**: Grafana service can be accessed via [localhost:3000](http://localhost:3000).
  
- **Authentication**: 
  - Default credentials for Grafana are `admin:admin`.
  - The password can be updated by setting the `GF_SECURITY_ADMIN_PASSWORD` environment variable.
  
- **Configuration**: For further configuration details of the Grafana service, see the [Grafana documentation](./grafana/README.md).

---


# A.2. Grafana Directory

- `dashboards`: Contains JSON configurations for various Grafana dashboards.
  - `dashboard-coinbase-matches.json`: Dashboard configuration for Coinbase matches.
  - `dashboard-coinbase-trades.json`: Dashboard configuration for Coinbase trades.
  - `dashboard-gps-tracker.json`: Dashboard configuration for GPS tracker.
  - `dashboard-weather-station.json`: Dashboard configuration for the weather station.

- `docs`: Contains documentation for Grafana.
  - `assets`: Contains asset files related to the documentation.
    - `datasource`: Contains images related to data sources.
      - `questdb_configuration.png`: Image showcasing the configuration of QuestDB.

- `provisioning`: Contains configuration files for provisioning Grafana.
  - `dashboards`: Contains YAML configurations for provisioning dashboards.
    - `file.yaml`: Configuration for provisioning a specific dashboard.
  - `datasources`: Contains YAML configurations for provisioning data sources.
    - `questdb.yml`: Configuration for provisioning QuestDB as a data source.

- `README.md`: Documentation for the Grafana directory.

## `dashboard-coinbase-matches.json`

### Dashboard Configuration: Coinbase matches ETH BTC

#### Overview

- **Title**: Coinbase matches ETH BTC
- **UID**: MNhO0-aKv
- **Version**: 3
- **Refresh Rate**: Every 5 seconds
- **Schema Version**: 38
- **Style**: Dark
- **Tags**: ETH-USD, BTC-USD

#### Timeframe

- **From**: The last hour (`now-1h`)
- **To**: Current time (`now`)

#### Annotations

- **Name**: Annotations & Alerts
- **Datasource**: Grafana (UID: -- Grafana --)
- **Icon Color**: rgba(0, 211, 255, 1)
- **Limit**: 100
- **Type**: Dashboard

#### Panels

##### 1. Price of ETH and BTC

- **ID**: 2
- **Description**: Coinbase live data for ETH and BTC
- **Grid Position**: Height: 17, Width: 24, X: 0, Y: 0
- **Datasource**: Postgres (UID: 2Bi8EToVz)
- **Legend**: Displayed at the bottom in list mode
- **Tooltip**: Single mode without sorting
- **SQL Queries**:
  - ETH Price: Extracts the price of ETH from `coinbase_matches` for the last 24 hours, sampling by 1 second.
  - BTC Price: Extracts the price of BTC from `coinbase_matches` for the last 24 hours, sampling by 1 second.

##### 2. Price and Volume of ETH

- **ID**: 3
- **Grid Position**: Height: 17, Width: 24, X: 0, Y: 17
- **Datasource**: Postgres (UID: 2Bi8EToVz)
- **Legend**: Displayed at the bottom in list mode
- **Tooltip**: Single mode without sorting
- **SQL Queries**:
  - ETH Price: Extracts the price of ETH from `coinbase_matches` for the last 24 hours, sampling by 1 second.
  - ETH Volume: Summarizes the volume of ETH from `coinbase_matches` for the last 24 hours, sampling by 1 second.

#### Additional Information

- **Editable**: True
- **Fiscal Year Start Month**: 0
- **Graph Tooltip**: 0
- **Live Now**: False


## `dashboard-coinbase-trades.json`

### Coinbase Trades Dashboard Configuration

#### Overview

- **Title**: Coinbase trades ETH BTC
- **UID**: MNhO0-aVk
- **Version**: 58
- **Refresh Rate**: 5s
- **Schema Version**: 38
- **Style**: Dark
- **Tags**: ETH-USD, BTC-USD
- **Editable**: True
- **Fiscal Year Start Month**: 0
- **Graph Tooltip**: 0
- **Live Now**: False

#### Timeframe
  - **From**: Last hour (`now-1h`)
  - **To**: Current time (`now`)


#### Annotations

- **Name**: Annotations & Alerts
- **Datasource**: Grafana (UID: -- Grafana --)
- **Icon Color**: rgba(0, 211, 255, 1)
- **Limit**: 100
- **Type**: Dashboard

#### Panels

##### 1. Price of ETH and BTC

- **Description**: Coinbase live data for ETH and BTC
- **Datasource**: Postgres (UID: 2Bi8EToVz)
- **Grid Position**: Height: 17, Width: 24, X: 0, Y: 0
- **Legend**: Displayed at the bottom in list mode
- **Tooltip**: Single mode without sorting
- **SQL Queries**:
  - ETH Price: Extracts the price of ETH from `trades` for the last 24 hours, sampling by 1 second.
  - BTC Price: Extracts the price of BTC from `trades` for the last 24 hours, sampling by 1 second.

##### 2. Price and Volume of ETH

- **Grid Position**: Height: 17, Width: 24, X: 0, Y: 17
- **Datasource**: Postgres (UID: 2Bi8EToVz)
- **Legend**: Displayed at the bottom in list mode
- **Tooltip**: Single mode without sorting
- **SQL Queries**:
  - ETH Price: Extracts the price of ETH from `trades` for the last 24 hours, sampling by 1 second.
  - ETH Volume: Summarizes the volume of ETH from `trades` for the last 24 hours, sampling by 1 second.

#### Additional Information

- **Editable**: True
- **Fiscal Year Start Month**: 0
- **Graph Tooltip**: 0
- **Live Now**: False


## `dashboard-gps-tracker.json`

### GPS Tracker Dashboard Configuration

#### Overview

- **Title**: GPS Tracker
- **UID**: b771f6fa-e4ad-4df8-a9a5-2c10b67f00f9
- **Version**: 9
- **Refresh Rate**: Not specified
- **Schema Version**: 38
- **Style**: Dark
- **Tags**: GPS
- **Editable**: True
- **Fiscal Year Start Month**: 0
- **Graph Tooltip**: 0
- **Live Now**: True

#### Timeframe
  - **From**: Last 6 hours (`now-6h`)
  - **To**: Current time (`now`)

#### Annotations

- **Name**: Annotations & Alerts
- **Datasource**: Grafana (UID: -- Grafana --)
- **Icon Color**: rgba(0, 211, 255, 1)
- **Type**: Dashboard

#### Panels

##### 1. GPS Tracker

- **Description**: GPS Tracker for Quectel EG25-G HAT
- **Datasource**: Postgres (UID: 2Bi8EToVz)
- **Grid Position**: Height: 19, Width: 24, X: 0, Y: 0
- **Map Type**: OpenStreetMap
- **Line Color**: Red
- **Point Color**: Royal Blue
- **Max Data Points**: 500
- **SQL Queries**:
  - Latitude Data: Extracts the latitude data from `gps_data` for the last 24 hours.
  - Longitude Data: Extracts the longitude data from `gps_data` for the last 24 hours.

#### Additional Information

- **Editable**: True
- **Fiscal Year Start Month**: 0
- **Graph Tooltip**: 0
- **Live Now**: True


## `dashboard-weather-station.json`

### Weather Station Dashboard Configuration

The provided JSON is a configuration for a dashboard, likely used in a tool like Grafana, given the nature and structure of the contents. Here's a summary of its key aspects:

 ### Overview
- **Title**: Weather Station Template BME680
- **UID**: d6dcc3ec-ef11-4d34-9fd3-bd8042ccf350
- **Version**: 71
- **Refresh Rate**: Every 1 minute
- **Time Range**: Last 24 hours
- **Style**: Dark
- **Tags**: Weather Station, BME680

#### Panels:

##### 1. Humidity Gauge Panel:
- **ID**: 3
- **Data Source**: Postgres with UID "2Bi8EToVz"
- **SQL Query**: Retrieves humidity data from the weather_data table for the past day.
- **Thresholds**:
  - 30% (Green)
  - 60% (Yellow)
  - 80% (Red)
- **Mapping**: Humidity levels are classified as:
  - Very Dry
  - Dry
  - Comfortable
  - Humid
  - Very Humid
- Display: Positioned at grid coordinates x=12, y=5 with a width of 4 units and a height of 5 units.

##### 2. Humidity Timeseries Panel:
- **ID**: 5
- **Data Source**: Postgres with UID "2Bi8EToVz"
- **SQL Query**: Same as the gauge, retrieves humidity data for the past day.
- **Display**: Positioned at grid coordinates x=16, y=5 with a width of 8 units and a height of 5 units.

##### 3. Temperature Gauge Panel:
- **ID**: 4
- **Data Source**: Postgres with UID "2Bi8EToVz"
- **SQL Query**: Retrieves temperature data from the weather_data table for the past day.
- Thresholds:
  - 0°C (Blue)  [Cold]
  - 20°C (Green)  [Comfortable]
  - 30°C (Yellow)  [Warm]
  - 40°C (Red)  [Hot]
- **Mapping**: Temperature levels are classified as:
  - Very Cold
  - Cold
  - Comfortable
  - Warm
  - Very Hot
- **Display**: Positioned at grid coordinates x=[specific x-coordinate], y=[specific y-coordinate] with a width of [specific width in units] units and a height of [specific height in units] units.


##### 4. Temperature Timeseries Panel:
- **ID**: 6
- **Data Source**: Postgres with UID "2Bi8EToVz"
- **SQL Query**: Retrieves temperature data from the weather_data table for the past day.
- **Display**: Positioned at grid coordinates x=0, y=0 with a width of 24 units and a height of 5 units.

##### 5. Pressure Gauge Panel:
- **ID**: 7
- **Data Source**: Postgres with UID "2Bi8EToVz"
- **SQL Query**: Retrieves pressure data from the weather_data table for the past day.
- **Thresholds**:
  - 980 (Yellow)
  - 1000 (Green)
  - 1025 (Blue)
- **Mapping**: Pressure levels are classified as:
  - Very Low
  - Low
  - Normal
  - High
- **Display**: Positioned at grid coordinates x=0, y=10 with a width of 5 units and a height of 8 units.

##### 6. Pressure Timeseries Panel:
- **ID**: 8
- **Data Source**: Postgres with UID "2Bi8EToVz"
- **SQL Query**: Same as the pressure gauge, retrieves pressure data for the past day.
- **Display**: Positioned at grid coordinates x=5, y=10 with a width of 19 units and a height of 8 units.

##### 7. Air Quality Gauge Panel:
- **ID**: 9
- **Data Source**: Postgres with UID "2Bi8EToVz"
- **SQL Query**: Retrieves air quality data from the weather_data table for the past day.
- **Thresholds**:
  - 0-50 (Green)  [Good]
  - 51-100 (Yellow)  [Moderate]
  - 101-150 (Orange)  [Unhealthy for Sensitive Groups]
  - 151-200 (Red)  [Unhealthy]
  - 201-300 (Purple)  [Very Unhealthy]
  - 300+ (Maroon)  [Hazardous]
- **Mapping**: Air quality levels based on AQI (Air Quality Index) are classified as:
  - Good
  - Moderate
  - Unhealthy for Sensitive Groups
  - Unhealthy
  - Very Unhealthy
  - Hazardous
- **Display**: Positioned at grid coordinates x=[specific x-coordinate], y=[specific y-coordinate] with a width of [specific width in units] units and a height of [specific height in units] units.


##### 8. Air Quality Timeseries Panel:
- **ID**: 2
- **Data Source**: Postgres with UID "2Bi8EToVz"
- **SQL Query**: Retrieves air quality data from the weather_data table for the past day.
- **Display**: Positioned at grid coordinates x=0, y=15 with a width of 24 units and a height of 5 units.

The configuration provides an understanding of how data is fetched from the database, the positioning of the visual elements on the dashboard, and the various thresholds and labels assigned for the visualization.



# A.3. Nginx Directory

- `.well-known`: Directory for well-known service information.
  - `.gitkeep`: Placeholder file to keep the directory in version control.

- `certs`: Contains certificate files.
  - `dhparam.pem`: Configuration file for Diffie-Hellman parameter.

- `conf.d`: Contains configuration files for individual Nginx sites.
  - `default.conf`: Default Nginx site configuration.
  - `default.conf.template`: Template for the default Nginx site configuration.

- `.htpasswd`: Password file for basic authentication in Nginx.
- `nginx.conf`: Main configuration file for Nginx.
- `nginx.env`: Environment variables for Nginx.

# A.4. VSCode Directory

- `Dockerfile`: Contains instructions for building the VSCode Docker image.
- `README.md`: Documentation for the VSCode directory.
- `requirements.txt`: Lists the requirements for the VSCode Docker image.



