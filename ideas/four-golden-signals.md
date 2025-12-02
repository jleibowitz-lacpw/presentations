# The Four Golden Signals for Monitoring Public-Facing Web Applications

## Context / Our Current State
- Our organization doesn't really do observability
- Most people haven't heard of Google SRE or observability concepts
- Current monitoring: IIS logs → Azure Sentinel
- Current alerting: Above-average traffic alerts
- Need better approaches for monitoring and alerting

## The Four Golden Signals (from Google SRE)

### 1. Latency
- **Definition**: Time it takes to service a request
- **Key Point**: Distinguish between successful and failed request latency
  - HTTP 500 errors might be served quickly, but they're still failures
  - Slow errors are worse than fast errors
  - Track error latency separately from success latency
- **Why It Matters**: High latency = degraded user experience
- **For Our Shop**: Response times for public-facing web apps

### 2. Traffic
- **Definition**: Measure of demand being placed on your system
- **Metrics**: 
  - HTTP requests per second (for web services)
  - Break out by request type (static vs. dynamic content)
  - Network I/O rate, concurrent sessions (for other systems)
- **Why It Matters**: Understand load patterns, capacity planning
- **For Our Shop**: Track request volumes to public sites, understand usage patterns

### 3. Errors
- **Definition**: Rate of failed requests
- **Types**:
  - **Explicit**: HTTP 500s, 404s
  - **Implicit**: HTTP 200 with wrong content
  - **Policy-based**: Requests exceeding SLA thresholds (e.g., >1 second when committed to sub-second)
- **Why It Matters**: Direct indicator of user-facing problems
- **Monitoring Approaches**:
  - Load balancer catches HTTP 500s (completely failed requests)
  - End-to-end tests detect wrong content
- **For Our Shop**: Move beyond just traffic volume to actual failure rates

### 4. Saturation
- **Definition**: How "full" your service is
- **Focus**: Resources that are most constrained
  - Memory-constrained system → show memory
  - I/O-constrained system → show I/O
  - CPU utilization, network bandwidth
- **Key Point**: Many systems degrade **before** 100% utilization
- **Leading Indicators**: 
  - 99th percentile response times often signal saturation
  - "Will database fill hard drive in 4 hours?"
- **For Our Shop**: Understand resource constraints before they become outages

## Why These Four?
If you can **only measure four metrics** of your user-facing system, these are the ones. They provide comprehensive coverage of system health.

## Symptoms vs. Causes
- **Symptom**: "What's broken?" (e.g., serving HTTP 500s, slow responses)
- **Cause**: "Why?" (e.g., database refusing connections, CPU overload)
- **Monitoring Philosophy**: 
  - Alert on symptoms (black-box monitoring)
  - Use causes for debugging (white-box monitoring)
  - "What" vs "why" is critical for signal vs. noise

## Black-Box vs. White-Box Monitoring

### Black-Box
- Symptom-oriented
- Tests externally visible behavior (as user sees it)
- Represents active problems: "System isn't working right now"
- **Best for**: Paging/alerting

### White-Box
- Inspects system internals (logs, metrics, HTTP endpoints)
- Detects imminent problems, failures masked by retries
- **Best for**: Debugging, preventing future issues

### The Balance
- **Heavy use** of white-box monitoring
- **Critical but modest use** of black-box monitoring
- Black-box forces discipline: only alert when problem is ongoing AND contributing to real symptoms

## Setting Baselines and Thresholds
1. **Baseline**: Normal system behavior under typical conditions
   - Example: Average request latency is 100ms during normal usage
2. **Threshold**: Alert limits for acceptable performance
   - Example: Alert when latency exceeds 300ms
3. **Review Regularly**: Systems evolve, so must your baselines
   - What was acceptable may no longer be sufficient
   - Adjust as you grow or change architecture

## Good Alerting Principles

### Questions to Ask Before Creating an Alert
1. Does this detect an otherwise undetected condition that is **urgent, actionable, and user-visible**?
2. Will I ever ignore this alert knowing it's benign? (If yes, fix the alert)
3. Does this definitely indicate users are negatively affected?
4. Can I take action? Is it urgent or can it wait? Can it be automated?
5. Are other people getting paged for this? (Redundant pages are waste)

### Philosophy on Paging
- Every page should trigger **sense of urgency**
- Can only react with urgency a few times/day before fatigue
- Every page must be **actionable**
- Every page requires **intelligence** (not robotic response)
- Pages should be about **novel problems**

### Red Flags
- **Rote, algorithmic responses** = should be automated
- **Alert fatigue** = too many low-quality alerts
- **Email alerts** = rarely read or acted on, favor dashboards instead

## Measurement Considerations

### The Tail Matters (Percentiles)
- **Don't rely on averages/means alone**
- Example: 100ms average latency @ 1,000 req/sec
  - BUT 1% of requests might take 5 seconds!
  - User experiences compound across multiple services
  - Backend's 99th percentile → frontend's median
- **Solution**: Collect request counts bucketed by latency (histograms)
  - 0-10ms, 10-30ms, 30-100ms, 100-300ms, etc.
  - Exponential boundaries help visualize distribution

### Resolution / Granularity
- Different aspects need different measurement frequencies
- Examples:
  - CPU load: Per-second to catch spikes driving tail latency
  - Uptime checks: Once or twice per minute is sufficient for 99.9% target
  - Disk fullness: Every 1-2 minutes is plenty
- **Trade-off**: High resolution is expensive (collection, storage, analysis)
- **Strategy**: Internal sampling on server, external collection/aggregation

## Tools and Techniques

### From the Articles
- **PFLB**: Performance/load testing, simulates real-world conditions
- **Prometheus**: Time-series data collection, real-time alerts
- **Grafana**: Visualization, dashboards for trends
- **Datadog, New Relic**: Full-stack monitoring platforms
- **Jaeger, Istio**: Distributed tracing for microservices

### For Our IIS Environment
- Explore Azure Monitor integration
- Application Insights for detailed telemetry
- Move from simple Sentinel logs to structured metrics
- Consider starting with Azure native tools before third-party

## Practical Recommendations for Our Shop

### Short-Term (What We Can Do Now)
1. **Audit Current Monitoring**: What are we actually measuring?
2. **Identify Gaps**: Which of the 4 signals are we missing?
3. **Start with Errors**: Easiest to implement and highest signal
4. **Add Latency Tracking**: Particularly for public-facing endpoints
5. **Review Alert Quality**: Are current alerts actionable? Do they indicate user impact?

### Medium-Term
1. **Implement Histograms**: Move beyond means to understand distribution
2. **Set Proper Baselines**: Establish what "normal" looks like
3. **Create Dashboards**: One place to see all 4 signals
4. **Reduce Alert Noise**: Remove non-actionable alerts

### Long-Term
1. **Build SLO Culture**: Define what reliability means for each service
2. **Capacity Planning**: Use saturation metrics proactively
3. **Automation**: Automate responses to known issues
4. **Continuous Improvement**: Regular reviews of monitoring effectiveness

## Key Takeaways for Talk

### The Problem
- We're flying blind with only traffic volume alerts
- No visibility into actual user experience
- Reactive instead of proactive

### The Solution
- Four Golden Signals provide comprehensive system health view
- Focus on **symptoms** (what users see) for alerting
- Use **causes** (internal metrics) for debugging
- Keep it simple: complexity is the enemy

### The Benefits
- Catch problems before users report them
- Understand system behavior and capacity
- Reduce alert fatigue with high-signal monitoring
- Make data-driven decisions about reliability

### The Path Forward
- Start small: pick one signal, implement well
- Build incrementally: add signals as you learn
- Keep it actionable: every alert should matter
- Make it visible: dashboards over email

## References
- [Google SRE Book - Chapter 6: Monitoring Distributed Systems](https://sre.google/sre-book/monitoring-distributed-systems/)
- [PFLB: Mastering Reliability - The 4 Golden Signals SRE Metrics](https://pflb.us/blog/4-golden-signals-sre/)
- Google SRE Book: Free online at sre.google
- Related: Site Reliability Engineering concepts, SLOs, Error Budgets

## Notes to Self
- Emphasize that this isn't about adding complexity - it's about adding **the right** visibility
- Use analogies: "You wouldn't drive a car with only a speedometer - you need fuel gauge, temp, oil pressure"
- Make it relatable: "Have you ever found out from a user that something was broken?"
- Show the contrast: Traffic alerts vs. actual user impact
- Keep it practical: What can we do with Azure/IIS stack we already have?
