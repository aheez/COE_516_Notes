# IoT Vulnerabilities & Attacks
## Goals and Violations
- **Confidentiality**
- **Integrity**
- **Availability**
- Authentication
- Non-repudiation
## Threats vs Vulnerabilities
- **Threat**: a potential for an attack
- **Vulnerability**: a weakness in the design, integration, or operation of a system or device

## Attack Surface
- **What**
	- assets
- **How**
	- possible ways of attacks
- **Where**
	- entry point
- **Why**
	- what can be gained (motivation behind the attack)

## Attack Vectors
- **Def**: a sequence of attack steps/actions

## Threat Aspects
- **Agents/Actors**
	- Hacker
	- Network host
	- insider
- **Actions**
	- Code injection
	- Brute-force 
	- etc.
- **Consequence/Outcome**
	- privilege escalation
	- access to data
	- malware installation
	- MitM
- **Attack Goal**

## National Vulnerability Database
- **National Vulnerability Dataset (NIST)**
- **Common Vulnerabilities and Exposures (CVEs)**

# Taxonomy

## Device-Level
### Definition
- Attacks in which adversaries target an IoT's hardware and/or their software
### Outcome
- Abnormal operation of the target IoT system
- Exchange of information is affected
### How
- HW trojan attack
- HW ports
- ... etc.

## Infrastructure-Level
### Definition
Targets an IoT's "Backend" or infrastructure
### Outcome
Threaten either the physical integrity or availability of data or devices located at the edge of the network
### How
- Compromising sensitive data through weak passwords
- Data manipulation, corruption, insertion, loss, or scavenging

## Communication-Level
### Definition
Communication Layer of the IoT system
### Outcome
- Affect the exchange of information between IoT devices and the wider network
### How
- MitM
- DoS
- RFID cloning
- traffic Analysis

## Service-Level
### Definition
Targets IoT's inherent functionality and services
- Front-end, Analytics/reporting
### Outcome
- Maliciously manage IoT application
### How
- Phishing attacks, social engineering
- Malicious scripts
- Reverse engineering