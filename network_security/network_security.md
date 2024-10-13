# Network Security Documentation

## **1. Overview**

This document outlines the network security architecture of the industrial simulator project, detailing the implementation of **inbound-only communication** via MQTT brokers, segmentation using VPCs, firewall configurations, and the overall strategy to maintain a secure environment while ensuring effective modular integration.

The goal is to achieve **strict access control**, reduce the **attack surface**, and facilitate **secure data flow** between all modules without compromising scalability or resilience.

## **2. Inbound Access Control**

### **A. MQTT Brokers for Module-Specific Ingress**
- **Inbound-only access** to the Google Cloud infrastructure is allowed through **module-specific MQTT brokers**.
- Each broker is assigned to a specific module (e.g., ERP, Scheduler, Production) and receives data only from designated sources.
- The MQTT brokers are configured with **TLS encryption** and **authentication** (username/password or certificates) to ensure that only authorized modules can communicate.

### **B. Firewall Rules and Network Segmentation**
- **Firewall rules** are implemented to restrict inbound and outbound traffic.
  - **Allow Rules**: Only allow traffic to MQTT brokers from designated sources.
  - **Deny Rules**: Deny all other inbound traffic by default.
- Each module is deployed in a separate **Virtual Private Cloud (VPC)** to ensure **network isolation**.
  - **VPC Peering** or **Cloud VPN** is used to facilitate communication between specific VPCs when cross-talk is needed.
- **Network tags** are used to easily apply firewall rules to specific resources, such as production, development, or test servers.

## **3. Authentication and Encryption**

### **A. MQTT Security Features**
- **TLS Encryption**: All MQTT communication is encrypted using TLS, ensuring that data exchanged between modules is secure from eavesdropping and tampering.
- **Authentication**: Modules authenticate to MQTT brokers using **username/password** or **client certificates** to prevent unauthorized access.
- **Topic-Level Access Control**: Fine-grained access control is enforced at the **topic level**. For example:
  - Only the **Scheduler Module** can publish job jackets to `scheduler/jobs/{batch_id}`.
  - The **Production Module** can only subscribe to topics relevant to its operation.

### **B. IAM Policies and Service Accounts**
- Each module uses a dedicated **service account** with assigned **IAM roles** to interact with Google Cloud resources.
- **Least Privilege Principle** is applied, where each service account is granted only the permissions necessary for its operation (e.g., the Scheduler module cannot modify ERP-related configurations).

## **4. Cross-VPC Communication**

### **A. When and Why Cross-Talk is Enabled**
- Cross-talk between VPCs is allowed in specific scenarios:
  - **Centralized MQTT Broker**: Certain operations require data to be shared centrally, such as common logging or monitoring systems.
  - **Shared Resources**: Resources like **BigQuery** for centralized data storage are accessed from multiple VPCs.
- **VPC Peering** or **Cloud VPN** is used to ensure **secure communication** between VPCs without exposing services to the public internet.

### **B. Security Measures for Cross-Talk**
- **Firewall Rules** for Cross-VPC communication restrict access only to necessary resources, ensuring that a breach in one module doesn’t affect the others.
- **IAM Policies** are enforced to manage which services or accounts are allowed to interact across VPCs.

## **5. Observability and Monitoring**

### **A. Centralized Logging and Monitoring**
- A **centralized logging system** (e.g., Google Cloud Logging or the ELK Stack) is deployed to collect logs from each module.
- Logs related to **network activity**, **authentication attempts**, and **MQTT traffic** are centrally collected and analyzed for anomalies.

### **B. Real-Time Dashboards and Alerts**
- **Grafana** is used to create **real-time dashboards** that monitor key metrics, such as MQTT broker activity, unauthorized access attempts, and module-specific KPIs.
- **Alerting Mechanisms** are configured to notify operators about security events, such as **excessive retries**, **failed authentication attempts**, or **high latency** in communication channels.

## **6. Risk Mitigation and Future Improvements**

### **A. Reduced Attack Surface**
- By limiting inbound access solely to **MQTT brokers** and using **firewall rules** to restrict traffic, the **attack surface** is minimized, reducing potential vulnerabilities.
- All other inbound and outbound access is **explicitly denied**, ensuring that only intended data flows are allowed.

### **B. Planned Enhancements**
- **Zero Trust Network Architecture**: Introduce a **Zero Trust** model for cross-VPC communication, requiring authentication and verification for each interaction.
- **Penetration Testing**: Regular **penetration tests** will be conducted to ensure that network isolation and authentication mechanisms remain robust against emerging threats.

## **7. Summary**
- The network security architecture ensures **controlled, inbound-only access** through **module-specific MQTT brokers**.
- **VPC segmentation** and **strict firewall rules** provide robust isolation between different components of the simulator.
- **Encryption**, **authentication**, and **topic-level access controls** ensure data integrity and confidentiality.
- The system's observability ensures that network activity is continuously monitored and any abnormal behavior is promptly detected and handled.

This security-focused architecture is designed to be **scalable, resilient**, and well-integrated with the overall goal of ensuring secure real-time data flow across modules, aligning with the Unified Namespace (UNS) approach.

