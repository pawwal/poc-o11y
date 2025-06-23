# POC-O11Y: Observability Proof of Concept

This project demonstrates a comprehensive observability stack using modern open-source tools. It provides a complete environment for monitoring, logging, tracing, and metrics collection for applications, with a focus on Java applications running in Tomcat.

## Overview

POC-O11Y (Proof of Concept - Observability) is a Docker-based environment that sets up a complete observability pipeline including:

- Metrics collection and visualization
- Distributed tracing
- Log aggregation
- Application performance monitoring

The stack includes a sample application (Orbeon Forms) that is fully instrumented with OpenTelemetry to demonstrate the capabilities of the observability tools.

## Components

### Monitoring & Visualization

- **Grafana**: Dashboard and visualization platform for metrics, logs, and traces
  - Port: 3000
  - Default credentials: admin/admin

### Metrics Collection

- **Prometheus**: Time-series database for metrics storage and querying
  - Port: 9090
  - Collects metrics from applications via OpenTelemetry exporters

### Observability Pipeline

- **Grafana Alloy**: Observability pipeline for collecting, transforming, and routing telemetry data
  - Port: 12345 (UI)
  - Ports: 4317, 4318 (OTLP receivers)
  - Handles logs and traces routing

### Distributed Tracing

- **Tempo**: Distributed tracing backend for storing and querying traces
  - Port: 3200 (HTTP API)
  - Port: 4317 (OTLP gRPC receiver)
  - Collects traces from applications via OpenTelemetry

### Log Aggregation

- **Loki**: Log aggregation system designed for Grafana
  - Port: 3100
  - Collects logs from applications via Grafana Alloy

### Sample Application

- **Orbeon Forms**: Enterprise web forms solution running on Tomcat
  - Port: 8081
  - Port: 9465 (Prometheus metrics)
  - Port: 8686 (JMX)
  - Fully instrumented with OpenTelemetry for metrics, logs, and traces

### Database

- **PostgreSQL**: Database for Orbeon Forms
  - Port: 5432
  - Default credentials: orbeon/orbeon

## Instrumentation

The project uses OpenTelemetry for instrumentation:

- **OpenTelemetry Java Agent**: Automatic instrumentation for Java applications
- **JMX Metrics Collection**: Configured to collect Tomcat and application metrics
- **Custom Metrics**: Additional metrics configuration for specific application components

## Getting Started

### Prerequisites

- Docker and Docker Compose
- At least 4GB of RAM available for Docker

### Installation

1. Clone this repository:
   ```
   git clone https://github.com/yourusername/poc-o11y.git
   cd poc-o11y
   ```

2. Start the stack:
   ```
   cd docker
   docker-compose up -d
   ```

3. Access the services:
   - Grafana: http://localhost:3000
   - Prometheus: http://localhost:9090
   - Grafana Alloy: http://localhost:12345
   - Orbeon Forms: http://localhost:8081/orbeon
   - Tempo: http://localhost:3200
   - Loki: http://localhost:3100

## Configuration

The project includes several configuration files:

- `docker/config/prometheus.yaml`: Prometheus configuration
- `docker/config/tempo.yaml`: Tempo configuration
- `docker/config/loki.yaml`: Loki configuration
- `docker/config/config.alloy`: Grafana Alloy configuration
- `docker/config/orbeon/`: Orbeon Forms configuration
- `docker/config/opentelemetry-javaagent.properties`: OpenTelemetry Java agent configuration

## Environment Variables

The following environment variables can be used to customize the deployment:

- `ORBEON_POSTGRES_PORT`: PostgreSQL port (default: 5432)
- `ORBEON_POSTGRES_DB`: PostgreSQL database name (default: orbeon)
- `ORBEON_POSTGRES_USER`: PostgreSQL username (default: orbeon)
- `ORBEON_POSTGRES_PASSWORD`: PostgreSQL password (default: orbeon)
- `ORBEON_POSTGRES_VOLUME`: PostgreSQL volume name (default: orbeon_pgdata)
- `ORBEON_PROPERTIES_FILE`: Path to Orbeon properties file
- `ORBEON_TOMCAT_CONTEXT_FILE`: Path to Orbeon Tomcat context file

## License

This project is licensed under the MIT License - see the LICENSE file for details.