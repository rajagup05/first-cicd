

## what is SLA

An SLA (Service Level Agreement) is a formal, legally binding contract between a service provider and a customer. It defines the level of service expected and the penalties if those levels aren't met.

### Relationship to SRE (Site Reliability Engineering):

- **The Guardrail**: SREs use SLIs (indicators) to measure and SLOs (objectives) to target, but the SLA is the final agreement that informs what SLIs/SLOs are business-critical.
- **Looser Objectives**: SREs often set internal SLOs (e.g., 99.95%) stricter than the SLA promise (e.g., 99.9%) to avoid breaching the contract.
- **Incident Management**: SLAs define the acceptable response time for incident resolution (e.g., P1 tickets).

### Relationship to DevOps:

- **Shared Responsibility**: While DevOps prioritizes fast delivery, the SLA provides the target reliability standard that the CI/CD pipeline must respect.
- **Accountability**: It forces DevOps teams to balance deployment speed with stability, as violating the SLA incurs financial penalties
