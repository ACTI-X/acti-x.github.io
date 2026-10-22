---
title: Incident Investigation and Response
weight: 4
---

![image](placeholder/img/iir_module_logo.jpg)
![image](placeholder/img/iir_module_schema.jpg)

**From an alert to an evidence-backed investigation, a validated verdict and a controlled response.**

# Description

The ACTI-X Incident Investigation and Response (IIR) module turns alerts, incidents and cyber threat intelligence into **structured, evidence-backed investigations** and **controlled response actions**. When a signal arrives from the ACTI-X CTI platform or from another module, IIR understands the incident, **retrieves the relevant logs and evidence** from the connected data sources, correlates them, checks them against the investigation procedure of the use case, and produces a **verdict, an explainable report and reusable threat intelligence**.

IIR is made of two parts:

- **AFIR (Automated Fraud Investigation and Reporting)**, the investigation engine. AFIR is an **existing open source project developed by Amadeus** that ACTI-X extends from fraud-focused investigation to a broader set of security incidents (phishing, account compromise, IOC matching, bot and application abuse, fraud).
- **IIR Response**, the response part, being designed within ACTI-X: it turns validated recommendations into **controlled response actions**, orchestrated through Cortex XSOAR playbooks and tracked in TheHive.

The investigation logic is generic: everything specific to a domain (entities, data sources, use cases, investigation playbooks, verdict rules, report wording) lives in a **knowledge pack**, so the same engine can be adapted to a new organisation or a new type of incident without changing the code. Analysts stay in control: runs can pause for **human approval**, every verdict is **validated by an analyst (4-eyes)** before it is shared, and high-impact actions always require approval.

As part of the ACTI-X ecosystem, IIR consumes intelligence from the CTI platform and publishes back **validated investigation outcomes in STIX 2.1** (incident, events, impacts, sightings, response tasks), so that what is confirmed during one investigation improves detection, investigation and response across the other modules. All exchanges with the platform go through a dedicated IIR connector: **raw evidence stays inside, only validated intelligence goes out**.

# How it contributes to ACTI-X

Security investigations often require analysts to collect information from several disconnected systems, rebuild the incident context by hand and coordinate actions with several teams. IIR provides a shared investigation and response layer for the ACTI-X ecosystem, from the first signal to the shared outcome.

- **Reduces fragmented and manual investigations**: IIR automatically identifies which data is needed, retrieves it from the connected sources (logs, SIEM, identity, endpoint and application data) and correlates it into a single timeline, instead of analysts navigating several portals.

- **Turns signals into explainable, evidence-backed verdicts**: each verdict is the result of the investigation procedure of the use case, with the checks that passed or failed, the evidence behind them and the anomalies found, so the analyst can verify the conclusion rather than trust it.

- **Connects investigation with threat intelligence sharing**: validated outcomes are published to the ACTI-X CTI platform in STIX 2.1, for example confirming that an indicator received from another module was actually seen inside the organisation, so other modules and partners can reuse it.

- **Supports controlled response**: recommended containment actions can be executed through response playbooks, with policy checks and human approval for consequential actions, and their outcome is tracked and reported back.

# Key Features

| Capability | Description |
|---|---|
| **AI-assisted incident understanding** | Uses language models to understand the incident, extract the affected users, accounts, assets and observables, and plan the investigation. |
| **Automated evidence retrieval** | Retrieves the relevant logs and evidence from the connected data sources (e.g. Databricks, Elasticsearch, REST APIs) for the right entities and time window. |
| **Correlation, anomaly detection and verdict** | Correlates evidence across sources, detects anomalies, compares with previous cases and adjudicates against the use-case procedure, with a confidence score. |
| **Knowledge packs** | Domain knowledge (entities, sources, playbooks, rules) is declared in packs, so the engine adapts to new organisations and incident types without code changes. |
| **Human in the loop** | Configurable run modes with approval gates, analyst feedback and 4-eyes validation before any intelligence is shared or any high-impact action is taken. |
| **Investigation reports** | Generates structured, evidence-backed reports (timeline, findings, verdict, recommended actions) for analysts and stakeholders. |
| **STIX 2.1 integration** | Consumes CTI from the ACTI-X platform and publishes validated outcomes in STIX 2.1, using the OASIS Incident Extension. |
| **Controlled response (in design)** | Orchestrates approved containment actions through Cortex XSOAR playbooks, with case management in TheHive and policy checks with the ACTI-X authorization module. |

# Additional Resources

### Source code

AFIR (Automated Fraud Investigation and Reporting): https://github.com/AmadeusITGroup/afir
