
## Information flows by framework

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': {
    'actorBkg': '#4CAF50',
    'actorTextColor': '#fff',
    'actorBorder': '#2E7D32',
    'actorLineColor': '#2E7D32',
    
    'participantBkg': '#2196F3',
    'participantTextColor': '#fff',
    'participantBorder': '#1976D2',
    
    'messageFontSize': '16px',
    'messageFontFamily': 'arial',
    'messageTextColor': '#333',
    
    'noteBkgColor': '#fff3bf',
    'noteTextColor': '#333',
    'noteBorderColor': '#FFB300',
    
    'loopTextColor': '#666',
    'loopBorderColor': '#FF9800',
    'loopBkgColor': '#FFF8E1',
    
    'sequenceNumberColor': '#fff',
    'sequenceNumberFontSize': '14px',
    
    'labelBoxBkgColor': '#F1F8E9',
    'labelBoxBorderColor': '#7CB342',
    'labelTextColor': '#333',
    
    'signalColor': '#2196F3',
    'signalTextColor': '#333',
    
    'activationBorderColor': '#E64A19',
    'activationBkgColor': '#FBE9E7',
    
    'mainBkg': '#FAFAFA'
}}}%%

sequenceDiagram
    actor Service
    participant Collector
    participant Storage
    participant Alert
    participant Dashboard
    
    activate Service
    Service->>+Collector: Send RED metrics
    Note over Service,Collector: Performance metrics
    Service->>+Collector: Send USE metrics
    Note over Service,Collector: Resource metrics
    Service->>+Collector: Send DUNE metrics
    Note over Service,Collector: Distributed metrics
    Service->>+Collector: Send DURESS metrics
    Note over Service,Collector: System health metrics
    deactivate Service
    
    Collector->>+Storage: Process & Store
    deactivate Collector
    
    loop Every minute
        Storage->>+Alert: Check thresholds
        Alert-->>-Dashboard: Update status
    end
    
    Dashboard->>+Storage: Query metrics
    Storage-->>-Dashboard: Return data
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

