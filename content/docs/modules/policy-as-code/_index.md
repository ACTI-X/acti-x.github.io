---
title: Policy as Code
weight: 1
---

**Policy as Code becomes threat intelligence.**

Infrastructure already shares what it sees in STIX. Applications do not, yet
many attacks pass through them: who accessed what, who gained a privilege,
which automated action was allowed. This module gives applications a way to
join threat intelligence, without sharing raw data.

## What exists today: Permguard

[Permguard](https://github.com/permguard) is an **existing open source Policy
as Code engine (Apache-2.0), developed outside ACTI-X**. ACTI-X extends it.

- Policies are written as code (Cedar and Rego), versioned and published as
  immutable, signed versions.
- Applications, API gateways and AI agents ask Permguard through its SDKs:
  *can this principal perform this action on this resource?*
- Permguard returns **permit** or **deny**; the caller enforces it.
- Every decision is recorded in an attributable **decision log**.

{{< tabs >}}
{{< tab name="How it works" >}}
![Author once, decide close to the workload: author, publish, mirror, decide, prove](/images/docs/permguard/steps.jpg)
{{< /tab >}}
{{< tab name="Policy as code" >}}
![A Cedar policy: who may do what on documents](/images/docs/permguard/policy.jpg)
{{< /tab >}}
{{< tab name="Decisions" >}}
![Every answer names the policies that decided it: Alice is permitted, Bob is denied](/images/docs/permguard/decision.jpg)
{{< /tab >}}
{{< tab name="Architecture" >}}
![One system, any shape: Permguard Server with control plane, data plane and trust plane](/images/docs/permguard/planes.jpg)
{{< /tab >}}
{{< tab name="Three rules" >}}
![Three rules: a version never changes, decisions stay near the workload, an answer leaves evidence](/images/docs/permguard/rules.jpg)
{{< /tab >}}
{{< /tabs >}}

To learn more about Permguard: [github.com/permguard](https://github.com/permguard).

## What ACTI-X adds: the extension

{{< callout type="info" >}}
The extension is being developed within ACTI-X and will be released as open
source.
{{< /callout >}}

Raw decision logs cannot be shared: they are large, contain sensitive data
and differ between vendors. The extension turns them, **locally**, into
behavioral signals and delivers them to OpenCTI.

![Inside the organization: decision logs are normalized, anonymized, aggregated and analyzed into a behavioral signal, mapped to STIX 2.1 and delivered over TAXII 2.1 to OpenCTI](/images/docs/policy-as-code/pipeline.jpg)

**Raw logs stay inside. Only intelligence goes out.**

### A common pattern for applications

A proposal of seven fields per decision, to be validated:

| Field       | Meaning                                  |
| ----------- | ---------------------------------------- |
| `principal` | Who asked, pseudonymised                 |
| `action`    | What was asked                           |
| `resource`  | The resource class, not the record       |
| `decision`  | Permit or deny                           |
| `policy`    | The rule and version applied             |
| `time`      | When it happened                         |
| `context`   | Tenant, application, risk level          |

### Share the behavior, not the data

Instead of `user X → server Y → file Z → 14:32`, the organization shares
the behavior, for example: *privilege escalation sequence, severity high*.
No user, no hostname, no internal address.

### Machine learning

| Purpose | Model                  | Use                                         |
| ------- | ---------------------- | ------------------------------------------- |
| Detect  | LSTM                   | Access pattern analysis                     |
| Detect  | Isolation Forest       | Outlier detection                           |
| Protect | k-means                | k-anonymity of the data                     |
| Protect | Random Forest          | Context-aware data masking                  |
| Protect | Federated learning     | Secure transfers; training data stays local |
| Adapt   | Reinforcement learning | Permissions adjusted to the threat level    |

Machine learning flags what matters; **the privacy policy decides what may
leave**. AI-generated outputs are marked and remain under human oversight.

### Verifiable provenance (proposed)

A valid STIX object is not necessarily verified intelligence. The proposal:
the Policy Decision Point signs decision logs and binds them to trusted
request contexts, and an independent verifier checks the provenance of what
an AI agent publishes. See the [Threat Model](../../threat-model/).

![Every claim carries verifiable provenance: PDP, execution controller, AI agent, independent verifier, OpenCTI](/images/docs/policy-as-code/continuity.jpg)

### Back to Permguard

Permguard does not only produce STIX: it also consumes it. Intelligence
returning from OpenCTI updates the context, and permissions can be adjusted
to the threat level.

![OpenCTI at the center of the ACTI-X correlation fabric, connected to the other modules and to the Policy Decision Point](/images/docs/policy-as-code/fabric.jpg)

A sample application will be integrated end to end within ACTI-X.

![From a request to a decision: any component asks Permguard through its SDK, Permguard returns permit or deny and records it in the decision log](/images/docs/policy-as-code/usecase.jpg)
