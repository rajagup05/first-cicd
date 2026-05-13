
## SLI

SLI (Service Level Indicator): A specific metric used to measure the performance of a service, such as request latency, error rate, or throughput.


### 📐 The Standard SLI Equation

Most SLIs are expressed as a percentage over a specific time window:

SLI=frac{Good Events} / {Total Events} *  100

- **Good Events**: Requests that meet a specific, predefined quality threshold.
- **Total Events**: The total valid requests received by the system.

### 🔍 4 Categories of SLIs (The Golden Signals)

Different types of architectures require different metrics. Google's Site Reliability Engineering (SRE) framework categorizes them into four primary signals:

- **Latency**: The time taken to service a request (e.g., duration of successful GET requests).
- **Traffic**: A measure of how much demand is being placed on the system (e.g., HTTP requests per second).
- **Errors**: The rate of requests that fail (e.g., HTTP 500 responses vs. total responses).
- **Saturation**: How "full" the service is, highlighting system constraints (e.g., CPU utilization percentage).
