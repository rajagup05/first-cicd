
## what is TOIL

Toil refers to administrative or operational work associated with running production services that is manual, repetitive, automatable, tactical, and lacks long-term value, often scaling linearly with service growth. In SRE (Site Reliability Engineering), it represents tasks that distract from strategic engineering work, such as manual system restarts, repetitive ticket resolution, or handling routine alerts.


### Key Characteristics of Toil (SRE context)

- **Manual**: Requires human intervention, such as running a script, rather than automated system handling.
- **Repetitive**: Involves doing the same task over and over.
- **Automatable**: If a machine could do it, or if the task can be designed away, it is toil.
- **Tactical**: Interrupt-driven and reactive (e.g., responding to alerts), not proactive or strategic.
- **Linear Scale**: As the service or user base grows, the toil work increases proportionally.
