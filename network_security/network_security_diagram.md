flowchart TD
    subgraph VPC1[ERP Module VPC]
        A[ERP Module] -->|Publish Order| B[MQTT Broker]
    end
    
    subgraph VPC2[Scheduler Module VPC]
        B -->|Order Received| C[Scheduler Module]
        C -->|Create Job Jacket| D[MQTT Broker]
    end
    
    subgraph VPC3[Production Module VPC]
        D -->|Job Execution Details| E[Production Line]
        E -->|Status Update| F[MQTT Broker]
    end
    
    G[Central Monitoring & Logging] -->|Monitor Logs| F
    F -->|Feedback on Completion| C
    style VPC1 fill:#f9f,stroke:#333,stroke-width:2px
    style VPC2 fill:#ff9,stroke:#333,stroke-width:2px
    style VPC3 fill:#9f9,stroke:#333,stroke-width:2px
    
    classDef broker fill:#fff,stroke:#000,stroke-width:2px;
    class B,D,F broker;