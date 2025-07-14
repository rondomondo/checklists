# SRE [Error Budget]

## 1. [Error Budget]

### Definition
The error budget is the allowed threshold for errors or unavailability within your [SLO] period.

### Implementation Steps
1. [ ] Define SLO target
2. [ ] Calculate available error budget
3. [ ] Set up tracking
4. [ ] Define consumption rules
5. [ ] Create alerts for consumption
6. [ ] Document policy actions 

### Calculator

```python
def calculate_error_budget(slo_target, measurement_period_hours=720):  # 30 days
    """
    Calculate error budget for a given SLO target
    
    Parameters:
    slo_target (float): SLO target percentage (e.g., 99.9)
    measurement_period_hours (int): Hours in measurement period
    
    Returns:
    dict: Error budget in different units
    """
    total_minutes = measurement_period_hours * 60
    allowed_downtime_minutes = total_minutes * ((100 - slo_target) / 100)
    
    return {
        'minutes': round(allowed_downtime_minutes, 2),
        'hours': round(allowed_downtime_minutes / 60, 2),
        'percentage': round(100 - slo_target, 3)
    }

def calculate_error_budget_remaining(slo_target, current_availability, 
                                  measurement_period_hours=720):
    """
    Calculate remaining error budget
    
    Parameters:
    slo_target (float): SLO target percentage
    current_availability (float): Current availability percentage
    measurement_period_hours (int): Hours in measurement period
    
    Returns:
    dict: Remaining error budget in different units
    """
    total_budget = calculate_error_budget(slo_target, measurement_period_hours)
    consumed_minutes = measurement_period_hours * 60 * \
                      ((slo_target - current_availability) / 100)
    
    remaining_minutes = total_budget['minutes'] - consumed_minutes
    
    return {
        'minutes': round(remaining_minutes, 2),
        'hours': round(remaining_minutes / 60, 2),
        'percentage': round((remaining_minutes / (measurement_period_hours * 60)) * 100, 3)
    }
```

## 2. [Error Budget Policy]

### Definition
A policy that defines what actions to take when error budget is consumed.

### Implementation Steps
1. [ ] Define stakeholders
2. [ ] Set consumption thresholds
3. [ ] Define actions at each threshold
4. [ ] Create escalation paths
5. [ ] Document consequences
6. [ ] Get agreement from all parties
7. [ ] Set review periods

### Policy Template Structure

```python
class ErrorBudgetPolicy:
    def __init__(self, slo_target, measurement_period_days=30):
        self.slo_target = slo_target
        self.measurement_period = measurement_period_days
        self.thresholds = {
            'green': 100,
            'yellow': 75,
            'orange': 50,
            'red': 25
        }
        
    def get_policy_actions(self, error_budget_remaining):
        """
        Get policy actions based on remaining error budget
        
        Parameters:
        error_budget_remaining (float): Percentage of error budget remaining
        
        Returns:
        dict: Required actions and restrictions
        """
        actions = {
            'deployment_allowed': True,
            'required_reviews': [],
            'restrictions': [],
            'notifications': []
        }
        
        if error_budget_remaining <= self.thresholds['red']:
            actions['deployment_allowed'] = False
            actions['required_reviews'].append('Executive Review')
            actions['restrictions'].append('Feature Freeze')
            actions['notifications'].append('Executive Team')
            
        elif error_budget_remaining <= self.thresholds['orange']:
            actions['required_reviews'].append('SRE Review')
            actions['restrictions'].append('Increased Testing Required')
            actions['notifications'].append('Engineering Leadership')
            
        elif error_budget_remaining <= self.thresholds['yellow']:
            actions['required_reviews'].append('Team Lead Review')
            actions['notifications'].append('Team Lead')
            
        return actions
```

### Example Policy Implementation
```python
def implement_error_budget_policy(current_availability, slo_target):
    """
    Implement error budget policy
    
    Parameters:
    current_availability (float): Current service availability
    slo_target (float): SLO target
    
    Returns:
    dict: Policy actions to take
    """
    policy = ErrorBudgetPolicy(slo_target)
    
    budget_remaining = calculate_error_budget_remaining(
        slo_target, 
        current_availability
    )
    
    actions = policy.get_policy_actions(
        budget_remaining['percentage']
    )
    
    return {
        'budget_remaining': budget_remaining,
        'policy_actions': actions,
        'status': get_status_level(budget_remaining['percentage'])
    }
```

More [SLO]  [SLI]  [SLA] [SLO Document] [Error Budget Policy ]

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