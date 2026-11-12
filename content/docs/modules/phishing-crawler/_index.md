---
title: Phishing Crawler
weight: 3
---

# Description

The ACTI-X Phishing Crawler module is responsible for the automated analysis of suspicious web content that may be associated with phishing campaigns. By continuously **crawling web resources**, the module collects indicators such as page content, hosting information, and embedded artifacts. This information is then processed to identify signs of credential theft, brand impersonation, or other phishing-related activities. 

Building on prior research conducted at Amadeus IT Group, the module enhances phishing detection capabilities through the application of scalable artificial intelligence and machine learning techniques. It leverages unsupervised learning methods to identify patterns, anomalies, and behavioral characteristics that may not be captured by traditional rule-based approaches. 

The module supports the automated detection and classification of phishing websites, as well as the identification of emerging attack techniques and previously unknown phishing infrastructure. By correlating technical, visual, and semantic indicators across multiple data sources, it enables the discovery of relationships between phishing artifacts.  

The resulting intelligence provides valuable support for threat hunting, incident response, and the continuous refinement of detection and analysis capabilities. The design emphasizes scalability and the ability to respond to the evolving nature of phishing threats. 
 

# How it contributes to ACTI-X

Organizations face a growing volume of phishing-related alerts, making email threat investigation one of the most resource-intensive activities for security operations teams. In parallel, phishing remains one of the most impactful cybersecurity threats facing organizations today. This challenge is further intensified by the increasing sophistication of modern campaigns. The ACTI-X Phishing Crawler module addresses these challenges by leveraging AI-driven analytics to uncover stealthy phishing attacks, correlate attacker infrastructures, and produce actionable threat intelligence. The resulting insights provide a deeper understanding of adversary operations, enabling faster detection, investigation, and response. Furthermore, the intelligence produced can be shared, correlated, and operationalized across the broader ACTI-X ecosystem, strengthening collective threat visibility and defense capabilities. 

- **Identifies emerging phishing threats:** The module continuously identifies phishing websites that target users, organizations, and critical infrastructures. This enables early detection of malicious activities, helping security teams reduce the risk of credential theft before threats can cause significant operational or financial damage. 

- **Adapts to evolving adversarial techniques:** It relies on AI-driven analytics and unsupervised learning to continuously identify emerging phishing tactics, techniques, and procedures (TTPs). By combining content analysis, visual similarity detection, infrastructure correlation, and campaign clustering, the tool can uncover previously unknown attack patterns and improve detection of sophisticated and rapidly changing phishing campaigns. 

- **Generates actionable threat intelligence:** The module automatically analyses phishing infrastructures, malicious content, and campaign relationships to produce high-value cyber threat intelligence. It generates campaign classifications, infrastructure indicators, and actor attribution insights in standardized STIX/TAXII formats, enabling seamless integration with the ACTI-X ecosystem.  

- **Is released as an open-source framework:** The module is made available as an open-source solution to encourage collaboration, transparency, and community-driven innovation. This approach enables organizations, researchers, and cybersecurity practitioners to adopt, extend, and contribute to the framework, fostering the wider dissemination of advanced phishing detection and threat intelligence capabilities. 

# Key Features


| Capability | Description |
|---|---|
| **AI-powered phishing detection** | Leverages unsupervised learning techniques to automatically identify phishing websites based on their visual appearance, content, structure, and behavioural characteristics. The detection engine uses AI-driven approaches to recognize both known and previously unseen phishing threats, improving coverage beyond traditional rule-based methods while reducing manual analysis efforts.  |
| **Scalable phishing correlation** | Automatically correlates technical, visual, and semantic indicators collected from phishing infrastructures. By identifying shared characteristics and recurring patterns, the module uncovers relationships between phishing entities, reveals infrastructure reuse, and supports the identification of broader malicious activities that may otherwise appear unrelated.  |
| **Large-scale advanced crawling capabilities** | ncorporates advanced crawling capabilities designed to bypass evasion techniques commonly used to restrict automated analysis. Its scalable architecture supports the efficient ingestion and processing of large volumes of input data, enabling continuous collection of phishing-related content.  |
| **Threat Intelligence generation and integration:** | Transforms the collected data into structured cyber threat intelligence (CTI) using the STIX standard. The generated CTI is shared through the ACTI-X CTI platform. This enables automated correlation with information generated by other ACTI-X components and facilitates intelligence-driven detection, threat hunting and investigation.    |

# Additional Resources

### GitHub repository and documentation
[ACTI-X phishing crawler repository](https://github.com/ACTI-X/actix-phishing-crawler)

### Related Articles

Boulila, Elyssa, et al. "A closer look at modern evasive phishing emails." 2025 55th Annual IEEE/IFIP International Conference on Dependable Systems and Networks (DSN). IEEE, 2025. Link: https://ieeexplore.ieee.org/abstract/document/11068798 


Boulila, Elyssa, et al. "Beyond Isolated Phishing Emails: Discovering Hidden Campaign Relationships with MCDA." 2026 28th International Conference on Information and Communications Securit (ICICS). Link: https://hal.science/hal-05681185v1/  