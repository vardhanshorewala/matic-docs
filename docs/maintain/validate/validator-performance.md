---
id: validator-performance-overview
title: Performance Metrics Overview
sidebar_label: Overview
description: Learn about the validator performance metrics that help validators self-regulate
keywords:
  - docs
  - matic
  - polygon
  - validator
  - performance
  - behavior
  - dashboard
  - staking
slug: validator-performance
image: https://wiki.polygon.technology/img/polygon-wiki.png
---


The Polygon Governance team administers an off-chain validator performance metric initiative that assists validators
in evaluating their network participation. Validators will eventually need to self-regulate network participation on
Polygon to an agreed set of on-chain parameters as the network continues to decentralize. The validator performance
metrics follow a benchmark calculation that evaluates validator performance.

## What it means to self-regulate

Self-regulation refers to setting and administering the conditions for admission, participation, and, if necessary,
the forced exit of validators from the active validator set - with the last part formalizing previously-achieved consensus
on the subject.

Successfully engaging in self-regulation requires setting parameters with fair, transparent, and self-enforcing
standards for:
- Measuring performance;
- Compliance with conditions of participation;
- Choosing and acting on remedial measures; and
- Addressing compliance breaches if and when they arise.

Under the proposed parameters, a validator who **underperforms the benchmarks for 700 checkpoints has a second 700
checkpoint period to correct the deficiency before a process to unbound its stake is implemented**.

:::note

The current parameters were chosen following feedback from the validator community, specifically
and the Polygon community at large.

:::

The framework allows for further decentralization of the network using validator self-regulation.
As a result of the increased amount of validator churn that may occur due to the new on-chain validator management
mechanism, the process for admitting new validators into the active set promotes network health and aligns with the notion
of gradual decentralization. Increasing the validator set to 105 also increases the economic security and decentralization
of the network.

## Validator performance framework

### Proposed Potential Parameters

Individual validator performance is measured based on checkpoints signed over a specified period, performed on a
rolling basis at each new checkpoint. This is then measured against a benchmark of the total network performance in that
same period, as detailed below:

- Monitoring Period (“MP") = previous 700 checkpoints, updated every new checkpoint.
- Take % of checkpoints signed by each validator in the MP, combine all % values and find the median average.
- Multiply the median average by an agreed multiple = Performance Benchmark (PB).
- At each checkpoint, calculate the % of checkpoints signed in the MP by individual validators and measure against the PB.

### Performance Benchmark

To transition validators into the process requiring the satisfaction of the proposed potential parameters, there
will be a slightly lower benchmark around the first two months while validators become accustomed to the parameters.

- PB1 → 95% of the median average of the last 700 checkpoints signed by the validator set (first 2,800 checkpoints)
- PB2 → 98% of the median average of last checkpoints signed by validator set (continues thereafter)

### Validator Performance Dashboard

A public dashboard provides live monitoring of individual and overall validator performance.
The dashboard serves the functions listed below.
- Provides real-time visual representations of validator performance telemetry.
- Displays validator notices and updates on their status, either meeting performance benchmarks or being deficient.

:::note In a future release

The dashboard will provide direct notifications to validators, alerting them to their
deficient status.

:::

### Notice to Validators

Validators are given 24 hours' notice of the commencement of performance monitoring, with the data set beginning 24 hours
after the notice is sent.

## Falling below performance benchmarks

### Remedial measures and corrective action

**Deficient Validator Process:**
- If validator <PB in the MP → Grace Period (“GP”).
- If validator in GP <PB after 700 checkpoints → Notice of Deficiency (“NOD”), enters into Grace Period 2 (“GP2”).
- If the validator in GP2 <PB after 700 checkpoints → Final Notice (“FN”), the validator will be unstaked with no further resource.

:::info Definition

The GP is 700 checkpoints long and allows a validator time to bring its performance back above the PB. If the deficiency is
corrected within the GP, there will be no further action. Failure to comply with the GP would result in issuing a public NOD
from the Performance Monitor (“PM”). The operator would have a 700 checkpoint period to correct the deficiency
in GP2. If the deficiency is fixed within the NOD period, then no further action will occur. However, the NOD would remain
public. Failure to comply with the GP2 would result in issuing an FN of the community's intent to implement a
forced exit procedure by offboarding the validator from the network by unbonding their stake.

:::

### Forced Unstaking

The unstaking of the deficient validator would be done as follows:

**Call ForceUnstake function in Polygon Commitchain Contract: 0xFa7D2a996aC6350f4b56C043112Da0366a59b74c**

## Validator Admission

To repopulate the validator slots that may become vacant as a result of the forced unstaking, below are the
proposed roadmap for the admission and onboarding of new validators into the set:

- Phase 1 (current) - The multi-sig holders would set the admission parameters and choose the validators.
- Phase 2 (next step) - The governance and validator communities set and approve the parameters, and the multi-sig holders
  implement those parameters.
- Phase 3 (end state) - The governance and validator communities set the parameters and admit and onboard validators themselves.

### Irregular joining

Joining the validator network consists of two steps: **admission and onboarding**. These steps and specific parameters
relating to each will ultimately be controlled by the governance community. This community approach enhances network security with
a level of certainty about the intent of the actors trying to join the network, and introduces social ramifications, which can ensure
proper functioning of the network, e.g., validator onboarding and education, participation in off-chain and on-chain governance,
efficient communication on critical updates and node performance issues.

Irregular joining occurs when a new validator joins the network but does not follow or circumvents the community-approved admissions
and onboarding process. Bot sniping of a node is an example of irregular joining.

As irregularly-joining validators do not participate in the onboarding process, they cause massive issues for the network's health.
In particular, the inability to communicate on critical updates and node performance issues is problematic.

As a result:
- Participation in the admission process will be viewed as obligatory;
- The above validators will be unstaked from the network;
- Any future participants who circumvent the process will be unstaked from the network;
- The minimum MATIC staked will be increased from 1 to 10,000 to deter snipers.

## Increasing the validator set

A situation may arise where an underperforming validator has already been offboarded following a Final Notice,
but a new one still needs to be onboarded to the network. This means that the active validator count may occasionally
drop below 100. Additionally, validators that underperform effectively reduce the active set for prolonged periods.

To maintain network integrity and guarantee an active set of 100 efficient validators, the validator set has increased to 105.
As the network has matured and seen wide adoption, it seems warranted to provide new validator slots for added decentralization and security.
