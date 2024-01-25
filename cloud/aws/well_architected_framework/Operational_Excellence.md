# Operational Excellence

https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/operational-excellence.html

At Amazon, we define operational excellence as a commitment (engagement) to build software correctly while consistently delivering a great customer experience. 

## Design principles

- Perform operations as code: In the cloud, you can apply the same engineering discipline that you use for application code to your entire environment.
You can define your entire workload (applications, infrastructure, etc.) as code and update it with code.
- Make frequent, small, reversible changes: Design workloads that are scaleable and loosely coupled to permit components to be updated regularly. 
- Refine operations procedures frequently: As you evolve your workloads, evolve your operations appropriately. As you use operations procedures, look for opportunities to improve them.
- Anticipate failure: Perform “pre-mortem” exercises to identify potential sources of failure so that they can be removed or mitigated. Test your failure scenarios and validate your understanding of their impact.
- Test your response procedures to ensure they are effective and that teams are familiar with their process. Set up regular _game days_ to test workload and team responses to simulated events.
- Learn from all operational failures: Drive improvement through lessons learned from all operational events and failures. Share what is learned across teams and through the entire organization.
- Use managed services: Reduce operational burden (charge opérationnelle) by using AWS managed services where possible. Build operational procedures around interactions with those services.
- Implement observability for actionable insights: Gain a comprehensive understanding of workload behavior, performance, reliability, cost, and health.
Establish key performance indicators (KPIs) and leverage observability telemetry to make informed decisions and take prompt action when business outcomes are at risk.
Proactively improve performance, reliability, and cost based on actionable observability data.

