# IoT Threat Modeling
## Why?
- To evaluate security of a system or system design
- Helps to develop a thorough understanding of the actors, entry points, and assets within a system
- Helps develop a detailed view of the threats to which the system is exposed

## Definitions 
- **Threat Modeling**: the larger exercise of identifying threats and their sources
- **Attack Modeling**: attacker-focused and designed to show how vulnerabilities may be exploited

## Threat Modeling Process
1. [[#Identifying the Assets]]
2. [[#Create an IoT System Architecture]]
3. [[#Decompose the IoT System]]
4. [[#Identify Threats]]
5. [[#Document Threats]]
6. [[#Rate the Threats]]

### Identifying the Assets
- The process of identifying and documenting what must be protected in the system.
- Examples:
	- Sensors
	- Sensors Data
	- Video Streams
	- Apps
	- Analytics System
	- Infrastructure Communications Equipment

### Create an IoT System Architecture
- To develop solid foundation for understanding the system functionalities
- Three sub-steps:
	1. Documenting expected functionality
	2. Architectural diagram that details the new IoT system
	3. Identify technologies used within the IoT system

### Decompose the IoT System
- Understand data lifecycle and its flow path though the system
- Identify vulnerable or weak points that must be addressed within the security architecture
- How:
	1. Identify and document the entry points for data within the system
	2. Trace the flow of data from the entry point and document all components that interact with it throughout the system
	3. Identify high-profile targets for attackers
	4. A detailed under standing of the system's attack surface emerges
- Identify the trust boundaries

>**Trust Boundaries**: a location on the data flow diagram where data changes its level of trust


### Identify Threats
- Apply the **STRIDE** model of Garg & Kohnfelder:
	- Spoofing
	- Tampering
	- Repudation
	- Information disclosure
	- Denial of service
	- Elevation of privilege
- Physical Security Bypass
- Social Engineering
- Supply Chain Issues

### Document Threats
Follow this format:

| Threat Description #<Threat_No> | "The Description"                |
| ------------------------------- | -------------------------------- |
| Threat Target                   | "Targeted Component"             |
| Attack Techniques               | "E.G., Social Engineering, MITM" |
| Counter Measure                 | "E.G., 2FA"                      |

### Rate the Threats
- Evaluating the likelihood and impact of each threat
- Conventional threat-rating methods can be used at this step
- **DREAD** model assigns a score (1 - 10) for each type of risk that emerges from a particular threat:
	- Damage: the amount of damage incurred by a successful attack
	- Reproducibility: what level of difficulty is involved in reproducing the attack
	- Exploitability: is the attack can be done easily
	- Affected users: what percentage of people/stakeholders would be affected
	- Discoverability: can the attack be discovered easily
- Calculate the average score of the previous and assign it to the threat
- Do it for all threats 