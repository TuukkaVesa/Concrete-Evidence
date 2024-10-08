# Concrete-Evidence<<<<<<< HEAD
# Raw Material Module Project

## Overview

This project aims to simulate and manage a raw material manufacturing module composed of multiple machines, which operate in a coordinated way according to the ISA-95 framework. The module will simulate realistic manufacturing operations, collect time-series data, and stream that data to a centralized cloud infrastructure for analysis and long-term storage.

The current focus is on building the **Raw Material Module** with integration to **EMQ (Erlang MQTT Broker)**, **Kotori** for historical data collection, and **Google Cloud** for long-term data storage and analysis. This system will adhere to best practices for scalability, asynchronous operation, and modular design.

## Project Goals

- Develop a modular, simulation-based manufacturing system composed of sub-modules (machines).
- Collect high-frequency data (e.g., 10 ms intervals) from individual machines and centralize that data for real-time and historical analysis.
- Integrate with **EMQ** for MQTT-based communication between modules, **Kotori** for data historian functions, and **Google Cloud** for long-term storage.
- Build everything in adherence to **ISA-95 standards** for object modeling and interoperability between production operations and business operations.
- Implement data visualization using **Google Cloud tools** such as **Google Data Studio** and **Looker** to create interactive dashboards for real-time and historical data insights.
- Enable predictive maintenance and process optimization through **BigQuery ML** by analyzing collected historical data.

## Architecture

The project is composed of multiple functional layers, each defined as a separate module or sub-module:

1. **EMQ (Erlang MQTT Broker)**: Acts as the central MQTT broker for machine communication and data exchange.
2. **Kotori**: Functions as a data historian, collecting high-frequency data from machines via MQTT.
3. **RawMaterialModule**: The core module that simulates a raw material processing environment, including machines such as crushers, blenders, and conveyors.
4. **Google Cloud Integration**: All machine and historian data are streamed to Google Cloud services for storage and analysis.

## System Components

### 1. EMQ

- **Role**: Acts as the central broker for all MQTT communication in the system.
- **Configuration**: Defined in the `config/emq_config.json` file.

### 2. Kotori

- **Role**: Collects time-series data, processes, and stores it into a suitable time-series database like **InfluxDB**.
- **Configuration**: Defined in the `config/kotori_config.json` file.

### 3. RawMaterialModule

- **Role**: Handles the coordination of multiple machines, collecting real-time data from individual sub-modules (e.g., crusher, blender).
- **Components**:
  - **Crusher Module**: Responsible for simulating crushing operations.
  - **Conveyor Module**: Simulates the conveyor belt transporting raw materials.
  - **Packaging Module**: Handles packaging of final products.
- **Configuration**: Defined in the `config/config.json` and `config/isa95_config.json` for ISA-95 compliance.

### 4. Google Cloud Integration

- **Role**: Handles long-term storage and analysis of all manufacturing data.
- **Components**:
  - **Google Pub/Sub**: For streaming data.
  - **Google Cloud Storage**: For storing logs and historical JSON files.
  - **BigQuery**: For analyzing historical data.
  - **Google Data Studio / Looker**: For creating interactive dashboards to visualize both real-time and historical data.
  - **BigQuery ML**: For running machine learning models on collected historical data to support predictive maintenance and operational insights.

## Setup Instructions

### Prerequisites

- **Docker** and **Docker Compose** installed.
- **Python 3.8+** with dependencies listed in `requirements.txt`.
- **Google Cloud SDK** for integration.

### Installation Steps

1. **Clone the Repository**:

   ```sh
   git clone https://github.com/your-repo/raw_material_module.git
   cd raw_material_module_project
   ```

2. **Install Dependencies**:

   ```sh
   pip install -r requirements.txt
   ```

3. **Configure Settings**:

   - Update MQTT settings in `config/emq_config.json`.
   - Update **Kotori** settings in `config/kotori_config.json`.
   - Update **Google Cloud** settings in `src/cloud/google_cloud.py`.

4. **Running the System**:

   - Use Docker Compose to run all services:
     ```sh
     docker-compose up
     ```
   - This will spin up **EMQ**, **Kotori**, and **RawMaterialModule** containers.

### Project Structure

```
raw_material_module_project/
├── config/
│   ├── config.json                   # General configuration settings for the modules.
│   ├── isa95_config.json             # Configuration specific to ISA-95 compliance.
│   ├── emq_config.json               # Configuration for EMQ MQTT Broker settings.
│   ├── kotori_config.json            # Configuration for Kotori data historian settings.
├── data/                             # Directory for storing raw data generated during simulations.
├── logs/                             # Directory for application logs and event data.
├── src/
│   ├── raw_material_module/          # Core module that handles the raw material manufacturing processes.
│   ├── machines/                     # Sub-modules representing individual machines (e.g., crusher, conveyor).
│   ├── cloud/                        # Google Cloud integration scripts for data streaming and storage.
│   ├── database/                     # Database interfaces (e.g., for connecting to InfluxDB or other databases).
│   ├── utils/                        # Utility functions used throughout the project (e.g., data validation, helpers).
├── deployment/
│   ├── docker-compose.yaml           # Docker Compose configuration to run all components.
│   ├── Dockerfile                    # Dockerfile for building the application container.
├── tests/                            # Unit tests for modules and sub-modules to ensure system reliability.
├── requirements.txt                  # List of required Python packages.
└── README.md                         # Project documentation (this file).
```

## ISA-95 Compliance

This project is built around **ISA-95 standards** to ensure interoperability between different levels of automation (e.g., from enterprise to the shop floor). ISA-95 compliance provides:

- **Resource Models**: Personnel, equipment, and materials are defined in configuration files.
- **Activity Models**: Operations and workflows are tracked to ensure efficient manufacturing.
- **Object Models**: Machines are represented in detail, with attributes defined for their status, capabilities, and roles.

## Future Enhancements

1. **Scaling Up Modules**: Add new machine modules (e.g., mixers, filters) to expand manufacturing capability.
2. **Anomaly Detection with ML**: Integrate machine learning models for detecting anomalies in machine performance using the collected historical data.
3. **Integration with ERP**: Add connectors for **ERP systems** to achieve business-level integration, leveraging ISA-95.
4. **Advanced Visualization**: Utilize **Grafana** or Google Cloud tools such as **Google Data Studio** and **Looker** for advanced visualization of real-time and historical data streams.
5. **Predictive Maintenance**: Utilize **BigQuery ML** to predict potential machine failures and optimize maintenance schedules.

## Contributions

Please feel free to contribute! Whether it's bug fixes, suggestions for new features, or documentation improvements, we'd love to have your input.

1. **Fork the Repository**.
2. **Create a Feature Branch**.
3. **Submit a Pull Request**.

## Contact

For any questions or help, please reach out via **issues** in the GitHub repository.
=======
# Concrete-Evidence
>>>>>>> 01715ad921c9fbfed79ff1cf12a9f12e438e75e4
