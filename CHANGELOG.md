# Project Changelog

## Version 1.0.0 - Initial Setup

**Date:** 2024-10-08

### Overview
This version marks the initial setup and structure for the Raw Material Module project. It includes setting up the core components, configuration files, and project goals.

### Added
- **Project Architecture**: Defined a modular structure based on ISA-95 standards for simulating a raw material manufacturing module.
- **Project Goals**: Documented the goals including modular design, data collection, integration with EMQ, Kotori, and Google Cloud.
- **System Components**:
  - **EMQ (Erlang MQTT Broker)** for handling MQTT communication.
  - **Kotori** for historical data collection.
  - **Google Cloud Integration** for long-term storage and analysis.
  - **RawMaterialModule**: Simulated crusher, conveyor, and packaging processes.
- **Docker Setup**: Configured `docker-compose.yaml` for running **EMQ**, **Kotori**, and **InfluxDB** in containers.

### Changed
- **JSON Configuration**: Developed an initial JSON configuration for the machine parameters and attributes, including crusher speed, load, torque, power consumption, and more.
- **External Influence**: Added the concept of **external influence**, specifically integrating real-world data (e.g., outside temperature) to influence the simulation parameters.
- **Readme Documentation**: Provided an extensive README including setup instructions, architecture overview, and ISA-95 compliance details.

### Improvements
- **Standardized Attributes**: Updated JSON configuration by:
  - Removing redundant fields for static parameters like `machine_id`.
  - Standardizing **randomization styles**.
  - Grouping parameters into categories for better readability and scalability.
  - Expanding the **external influence** representation for more detailed interaction.

## Version 1.1.0 - Attribute Refinements and Machine Integration

**Date:** 2024-10-09

### Added
- **Detailed Machine Attribute Definitions**: Incorporated attributes for `crusher`, `conveyor`, `kiln`, and `blender` machines based on median values from typical real-world scenarios.
- **New Parameters for Crusher**: Defined additional metrics like **machine wear**, **advanced vibration monitoring**, and **remaining useful life** for proactive maintenance and better monitoring.
- **Changelog**: Created and documented the changelog for tracking project progress.

### Changed
- **Parameter Relationships**: Defined and validated relationships between parameters to ensure realistic behavior in simulation. For example, **crusher torque** is influenced by **crusher load**, and **bearing temperature** is influenced by **outside temperature**.
- **External Data Handling**: Enhanced the handling of **external influence** data with clear formulas and descriptions for better clarity.

### Removed
- **Unused Fields**: Removed unnecessary fields in the JSON for attributes that did not require a **range** or **units**.

## Planned Features for Next Version

- **Modular Machine Design**: Break down each machine into distinct sub-modules for easier maintenance and testing.
- **MQTT Integration**: Set up MQTT topics and messaging structure for the various machine modules.
- **Data Validation and Monitoring**: Implement a data validation layer to ensure that input parameters are within realistic limits.
- **Visualization Tools**: Develop integration with **Grafana** or Google Cloud tools for visualizing historical and real-time data.

