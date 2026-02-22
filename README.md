# Microservices Observability Stack

This project implements a comprehensive observability solution for a microservices architecture. It demonstrates the integration of metrics and distributed tracing across REST and gRPC services using Prometheus, Grafana, and OpenTelemetry to monitor system health and performance in real-time.

## Project Overview

The system consists of a FastAPI-based REST gateway and a Python gRPC backend service backed by MongoDB. The primary goal was to implement a full observability pipeline to track the "Four Golden Signals" across multi-protocol communications.
<img width="1542" height="741" alt="image" src="https://github.com/user-attachments/assets/11fab66f-58db-499a-95f6-c732fccd8591" />
<img width="1920" height="839" alt="image" src="https://github.com/user-attachments/assets/6cab6d10-8806-4c46-a151-8bbe40694fdb" />
<img width="1920" height="517" alt="image" src="https://github.com/user-attachments/assets/1062ca3c-10f1-417e-87a2-8a77bcf39e59" />



### Key Components
*   **Infrastructure**: Containerized deployment using Docker Compose.
*   **Persistence**: MongoDB with unique indexing for data integrity.
*   **Fault Tolerance**: Circuit breaker pattern implemented in the REST gateway to handle backend service failures gracefully.

## Technical Implementation

### 1. Multi-Protocol Monitoring (Prometheus)
Implemented metric collection for both HTTP and gRPC protocols to provide a unified view of system performance.
*   **REST Instrumentation**: Integrated Prometheus middleware in FastAPI to capture total requests and processing duration.
*   **gRPC Interceptors**: Utilized server interceptors to automatically track internal service handling time and error rates.
*   **PromQL Queries**: Configured specific queries for real-time monitoring of p95 latency, request rates, and error percentages.

### 2. Distributed Tracing (OpenTelemetry & Jaeger)
Established end-to-end visibility of request flows across service boundaries via an OpenTelemetry Collector.
*   **End-to-End Spans**: Instrumented services to provide trace continuity from the REST entry point through the gRPC call to the MongoDB persistence layer.
*   **OTLP Integration**: Configured OTLP-gRPC exporters to transmit telemetry data efficiently to the Jaeger backend.

### 3. Visualization and Analysis
*   **Grafana Dashboards**: Built a centralized dashboard with real-time panels for cross-service latency and error monitoring.
*   **Load Simulation**: Developed a traffic generator to simulate concurrent requests and intentionally trigger conflict states, validating the observability of data integrity error spikes.

## Results and Insights

*   **Performance Analysis**: Measurement showed a 0.5ms (approx. 10%) latency overhead introduced by tracing instrumentation. This finding suggests implementing trace sampling for production-scale deployments to balance visibility and performance.
*   **System Resilience**: The implementation successfully captured circuit breaker state changes and identified backend bottlenecking under simulated load.
*   **Compatibility Handling**: Managed complex dependency conflicts between gRPC and OpenTelemetry libraries during the initial environment setup.

## Running the Project

Ensure you have Docker and Docker Compose installed.

1.  **Bring up the stack**:
    ```
    docker-compose up -d --build
    ```
2.  **Access the Dashboards**:
    *   **Grafana**: [http://localhost:3000](http://localhost:3000)
    *   **Prometheus**: [http://localhost:9090](http://localhost:9090)
    *   **Jaeger UI**: [http://localhost:16686](http://localhost:16686)

