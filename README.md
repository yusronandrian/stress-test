# k6 Load Testing with InfluxDB and Grafana

## Overview

This project provides a robust and easy-to-use setup for load testing using k6, storing metrics in InfluxDB, and visualizing results with Grafana, all orchestrated via Docker Compose. It's designed to help you quickly spin up a performance testing environment and analyze your application's behavior under load.

## Features

*   **k6:** A modern load testing tool for scripting and running performance tests.
*   **InfluxDB:** A high-performance time-series database for storing k6 performance metrics.
*   **Grafana:** A powerful analytics and visualization platform for monitoring and analyzing load test results with a pre-configured dashboard.
*   **Docker Compose:** Simplifies the setup and management of all services (k6, InfluxDB, Grafana).
*   **Cross-platform scripts:** Easy execution on both Linux/macOS (Bash) and Windows (PowerShell).

## Prerequisites

Before you begin, ensure you have the following installed:

*   [Docker](https://docs.docker.com/get-docker/)
*   [Docker Compose](https://docs.docker.com/compose/install/) (usually comes with Docker Desktop)

## Getting Started

Follow these steps to run your first load test and view the results.

1.  **Clone the repository:**
    ```bash
    git clone [stress-test](https://github.com/yusronandrian/stress-test)
    cd stress-test
    ```
    *(Replace `[stress-test](https://github.com/yusronandrian/stress-test)` and `stress-test` with your actual repository details.)*

2.  **Run the Load Test:**
    Use the provided scripts to start the services and execute the k6 test.

    *   **On Linux/macOS:**
        ```bash
        ./run-load-test.sh
        ```

    *   **On Windows (PowerShell):**
        ```powershell
        ./run-load-test.ps1
        ```

    The script will perform the following actions:
    *   Start the `influxdb` and `grafana` containers in detached mode.
    *   Print the URL for the Grafana dashboard.
    *   Run the k6 test script (`scripts/ewoks.js`) within a temporary `k6` container.

3.  **Access Grafana Dashboard:**
    Once the script starts, you can access the Grafana dashboard at:
    [http://localhost:3000/d/k6/k6-load-testing-results](http://localhost:3000/d/k6/k6-load-testing-results)

    *   **Default Grafana Credentials:** `admin`/`admin` (you might be prompted to change the password on first login).
    *   The dashboard will automatically display the metrics from the k6 test run, allowing you to monitor the performance in real-time or review past results.

## Configuration

### k6 Test Script (`scripts/ewoks.js`)

The k6 test script (`scripts/ewoks.js`) is configured to run a simple load test against `https://swapi.dev/api/people/30/`.

You can adjust the number of virtual users (VUs) for the test by setting the `TARGET_VUS` environment variable before running the script.

*   **Example (Linux/macOS):**
    ```bash
    TARGET_VUS=20 ./run-load-test.sh
    ```

*   **Example (Windows PowerShell):**
    ```powershell
    $env:TARGET_VUS=20
    ./run-load-test.ps1
    ```

    If `TARGET_VUS` is not set, the script defaults to `5` virtual users.

### Grafana Dashboard

The project automatically provisions a Grafana dashboard designed for k6 results.
*   The datasource configuration for InfluxDB is defined in `grafana-datasource.yaml`.
*   The dashboard provisioning configuration is in `grafana-dashboard.yaml`.

## Project Structure

*   `docker-compose.yaml`: (Implied, not provided in context) Defines the `influxdb`, `grafana`, and `k6` services.
*   `scripts/ewoks.js`: The k6 load test script, targeting `https://swapi.dev/api/people/30/`.
*   `run-load-test.sh`: Bash script to orchestrate and run the load test.
*   `run-load-test.ps1`: PowerShell script to orchestrate and run the load test.
*   `grafana-datasource.yaml`: Configures InfluxDB as a datasource for Grafana.
*   `grafana-dashboard.yaml`: Configures Grafana to automatically provision dashboards.

## Customization

*   **Change the k6 test target:** Modify `scripts/ewoks.js` to target a different API endpoint, implement more complex test scenarios, or add custom checks.
*   **Add more k6 scripts:** Place additional k6 scripts in the `scripts/` directory and update `run-load-test.sh`/`.ps1` to execute them.
*   **Customize Grafana dashboard:** You can import other k6 Grafana dashboards, create your own, or modify the existing one to suit your specific monitoring needs.
