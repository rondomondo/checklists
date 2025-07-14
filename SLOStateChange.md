## [SLO] State Change Diagram

```mermaid
stateDiagram-v2
    [*] --> Green
    Green --> Yellow: 25% Consumed
    Yellow --> Orange: 50% Consumed
    Orange --> Red: 75% Consumed
    Red --> Green: Reset at Window End
    
    state Green {
        [*] --> FullSpeed
        state "Full Speed" as FullSpeed
        state "Normal Deployments" as Deployments
        state "Standard Reviews" as Reviews
    }
    
    state Yellow {
        [*] --> Caution
        state "Caution" as Caution
        state "Team Lead Review" as LeadReview
        state "Increased Monitoring" as Monitoring
    }
    
    state Orange {
        [*] --> Warning
        state "Warning" as Warning
        state "SRE Review Required" as SREReview
        state "Additional Testing" as Testing
    }
    
    state Red {
        [*] --> Stop
        state "Stop" as Stop
        state "Feature Freeze" as Freeze
        state "Executive Review" as ExecReview
        state "Crisis Management" as Crisis
    }

    classDef green fill:#4CAF50,stroke:#2E7D32,color:white
    classDef yellow fill:#FFC107,stroke:#FFA000,color:black
    classDef orange fill:#FF9800,stroke:#F57C00,color:black
    classDef red fill:#F44336,stroke:#D32F2F,color:white
    #classDef white fill:#FFFFFF,stroke:#000000,color:black

    class Green green
    class Yellow yellow
    class Orange orange
    class Red red
    class White white

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