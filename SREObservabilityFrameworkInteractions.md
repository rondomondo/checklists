
## Relationship between frameworks
```mermaid
flowchart TB
    subgraph Primary Methods
        direction LR
        subgraph RED Framework
            direction TB
            R[Rate]:::rateMetric --> RED:::redMethod
            E1[Errors]:::errorMetric --> RED
            D1[Duration]:::durationMetric --> RED
        end
        
        subgraph USE Method
            direction TB
            U1[Utilization]:::utilizationMetric --> USE:::useMethod
            S1[Saturation]:::saturationMetric --> USE
            E2[Errors]:::errorMetric --> USE
        end
        
        subgraph DUNE Method
            direction TB
            D2[Delay]:::durationMetric --> DUNE:::duneMethod
            U2[Utilization]:::utilizationMetric --> DUNE
            N[Noise]:::noiseMetric --> DUNE
            E3[Errors]:::errorMetric --> DUNE
        end
    end
    
    RED --> ServiceHealth[Service Health]:::healthMetric
    USE --> SystemHealth[System Health]:::healthMetric
    DUNE --> DistributedHealth[Distributed Systems Health]:::healthMetric
    
    ServiceHealth --> Aggregation[Health Metrics Aggregation]:::aggregationNode
    SystemHealth --> Aggregation
    DistributedHealth --> Aggregation
    
    Aggregation --> DURESS
    
    subgraph DURESS System
        direction LR
        D3[Downstream]:::downstreamMetric & U3[Uptime]:::uptimeMetric & R1[Resources]:::resourceMetric --> DURESS:::duressMethod
        E4[Errors]:::errorMetric & S2[Saturation]:::saturationMetric & S3[Staleness]:::stalenessMetric --> DURESS
    end
    
    DURESS --> OverallHealth[Overall Health]:::healthMetric
    OverallHealth --> MonitoringStrategy[Monitoring Strategy]:::strategyNode

    classDef rateMetric fill:#ff9999,stroke:#ff0000,color:#000
    classDef errorMetric fill:#ffcccc,stroke:#ff0000,color:#000
    classDef durationMetric fill:#99ff99,stroke:#00ff00,color:#000
    classDef utilizationMetric fill:#9999ff,stroke:#0000ff,color:#000
    classDef saturationMetric fill:#ffff99,stroke:#ffff00,color:#000
    classDef noiseMetric fill:#ff99ff,stroke:#ff00ff,color:#000
    classDef downstreamMetric fill:#99ffff,stroke:#00ffff,color:#000
    classDef uptimeMetric fill:#ffcc99,stroke:#ff9900,color:#000
    classDef resourceMetric fill:#99ccff,stroke:#0099ff,color:#000
    classDef stalenessMetric fill:#cc99ff,stroke:#9900ff,color:#000
    
    classDef redMethod fill:#ffe6e6,stroke:#ff0000,color:#000
    classDef useMethod fill:#e6e6ff,stroke:#0000ff,color:#000
    classDef duneMethod fill:#e6ffe6,stroke:#00ff00,color:#000
    classDef duressMethod fill:#ffe6ff,stroke:#ff00ff,color:#000
    
    classDef healthMetric fill:#e6ffee,stroke:#00ff00,color:#000
    classDef aggregationNode fill:#f0f0f0,stroke:#666666,color:#000
    classDef strategyNode fill:#e6f3ff,stroke:#0066cc,color:#000
```

[Frameworks]: https://alertstack.io/frameworks

[Observability Frameworks]: https://alertstack.io/frameworks

[SLO]: https://sre.google/sre-book/service-level-objectives/

[SLI]: https://www.sumologic.com/glossary/sli-service-level-indicator/

[SLA]: https://sre.google/sre-book/service-level-objectives/

[MTTR]: https://www.blameless.com/blog/mttr

[MTBF]: https://www.blameless.com/blog/mttr

[MTTA]: https://www.blameless.com/blog/mttr

[MTTR]: https://www.blameless.com/blog/mttr

[RED]: https://www.splunk.com/en_us/blog/learn/red-monitoring.html

[DURESS]: https://sre.google/sre-book/service-level-objectives/

[DUNE]: https://sre.google/sre-book/service-level-objectives/

[USE]: https://sre.google/sre-book/service-level-objectives/

[CELTE]: https://sre.google/sre-book/service-level-objectives/

[4 Signals]: https://sre.google/sre-book/monitoring-distributed-systems/#xref_monitoring_golden-signals

[Error Budget Policy]: https://sre.google/workbook/error-budget-policy

[SLO Document]: https://sre.google/workbook/slo-document/

[Error Budget]: https://handbook.gitlab.com/handbook/engineering/error-budgets/