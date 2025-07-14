## 1. Service Level Indicators ([SLI])

### Definition
SLIs are the actual measurements of service behavior that you use to determine if you're meeting [SLO]s.

### Implementation Steps
1. [ ] Choose what to measure:
   - Request latency
   - Error rate
   - System throughput
   - Availability
2. [ ] Define measurement points
3. [ ] Set up monitoring
4. [ ] Implement collection methods
5. [ ] Create dashboards
6. [ ] Set up alerts

### Common SLIs
- Availability = successful requests / total requests
- Latency = time to serve request
- Quality = successful executions / total executions
- Freshness = time since last update
- Coverage = percentage of data processed

Review which of the [Observability Frameworks] are relevent to your use case(s)

### Calculator
```python
def calculate_sli(good_events, total_events, sli_type="availability"):
    """
    Calculate SLI for different metrics
    
    Parameters:
    good_events (int/float): Number of good events or measurements
    total_events (int/float): Total number of events
    sli_type (str): Type of SLI (availability, latency, quality)
    
    Returns:
    float: SLI value
    """
    if total_events == 0:
        return 0.0
        
    sli = (good_events / total_events) * 100
    
    # Add specific handling for different SLI types
    if sli_type == "latency":
        # For latency, we might want to use percentiles instead
        sli = calculate_percentile(good_events, 95)  # 95th percentile
        
    return round(sli, 3)
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