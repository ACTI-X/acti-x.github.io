---
title: Threat Model
weight: 1
---

**Who acts, and on whose authority.**

ACTI-X brings many security modules together around one platform, OpenCTI.
The threat model looks at where trust is assumed and where it must be checked.

{{< callout type="info" >}}
This is a threat model, not a deployment design. By default, ACTI-X modules
exchange through OpenCTI. The threat model identifies the controls needed if
direct links or model-driven actions are introduced.
{{< /callout >}}

## Method: execution boundaries

Every module is an execution boundary, and so is OpenCTI. For each boundary
we make explicit what can be trusted and which inputs must be treated as
untrusted. From there we derive the requirements for **authentication,
authorization, communication and evidence provenance**.

![Not modules: execution boundaries, with OpenCTI as one of them](/images/docs/threat-model/boundaries.jpg)

A boundary is trusted by default (code reviewed and released by people), but
review and release reduce risk: they do not prove every execution correct.

## Three layers, distinct security contexts

| Layer          | Check                                                     |
| -------------- | --------------------------------------------------------- |
| Transport      | TLS, or mutual TLS when both peers authenticate           |
| Infrastructure | e.g. a message broker enforcing publisher permissions     |
| Application    | The receiving service identifies the principal and its authority |

These identities are not interchangeable: protecting one layer does not
protect the others.

![Three layers between two execution boundaries: transport, infrastructure, application](/images/docs/threat-model/layers.jpg)

## Key risks

| Risk | What happens | Control |
| --- | --- | --- |
| **Direct module-to-module calls** | OpenCTI can no longer vouch for the call | Service-to-service authentication and authorization |
| **Module impersonation** | A valid credential submits STIX claiming another module as creator | Cryptographic origin verification: signature bound to an authorized producer |
| **Wrong context** | Evidence from run B is attributed to run A, with valid signature and token | Trustworthy binding of each run to its execution context |
| **Authenticated ≠ authorized** | Knowing who calls does not mean the call is allowed | Authorization at every boundary |
| **Delegation** | A → B → C on someone's behalf: whose authority is used? | Verify delegated authority; it must never grow along the chain |
| **AI agent that acts** | Untrusted input redirects tool use (e.g. a hidden prompt) | Restricted tools, explicit authorization, independent checks |
| **False intelligence with valid credentials** | Invented, misattributed or unsupported evidence; flooding | Provenance checks, marking of unverified claims, rate limits and quotas |

A signature limits impersonation, but **verified provenance is not proof
that a claim is true**.

{{< tabs >}}
{{< tab name="Impersonation" >}}
![Valid access, forged creator claim: an attacker with a stolen credential submits STIX claiming module B as creator](/images/docs/threat-model/spoof.jpg)
{{< /tab >}}
{{< tab name="Origin verification" >}}
![Every signature binds content to a signing key: the origin verifier accepts module B and rejects the attacker](/images/docs/threat-model/origin.jpg)
{{< /tab >}}
{{< tab name="Wrong context" >}}
![Valid signature, wrong context: evidence from run B attributed to run A](/images/docs/threat-model/context.jpg)
{{< /tab >}}
{{< tab name="Delegation" >}}
![One module calls another: user, module A, module B, module C, on whose authority?](/images/docs/threat-model/delegation.jpg)
{{< /tab >}}
{{< tab name="AI agent" >}}
![An AI agent inside module C combines Alice's documents with Bob's messaging permission and sends them outside](/images/docs/threat-model/untrusted.jpg)
{{< /tab >}}
{{< /tabs >}}

## Posture

What the threat model asks of ACTI-X:

1. Secure the transport.
2. Authenticate on the infrastructure.
3. Identify the principal in the application.
4. Verify every origin against authorized producers.
5. Bind AI-generated evidence to its execution context.
6. Authorize at every boundary.
7. Never let delegated authority grow along the chain.
8. Limit abuse with rate limits, quotas and quarantine.
9. For untrusted executors, apply independent checks and human oversight
   proportionate to the risk. A human approves every high-impact action.

![Independent controls: the AI agent proposes within predefined limits, a human approves high-impact actions](/images/docs/threat-model/human.jpg)

## Five questions

| Question                                   | Topic          |
| ------------------------------------------ | -------------- |
| Who acts?                                  | Authentication |
| Who really sent it?                        | Origin         |
| What may it do?                            | Authorization  |
| On whose authority?                        | Delegation     |
| On what verifiable evidence does a claim rest? | Evidence   |
