# Technology Selection

## MCUs and SoCs
- Based on functional requirements of the IoT device
- Considerations:
	- Cryptographic bootloader
	- Cryptographic HW accelerator
	- Secure memory protection
	- Built-in tamper protection
	- Protection against reverse engineering
	- Secure mechanisms in nonvolatile memory
	- Test/Debug ports protection

## Real-Time Operating Systems (RTOS)
| Category        | RTOS Requirement                     |
| --------------- | ------------------------------------ |
| Safety-Critical | Safety Certifications                |
| Industrial      | Reliability and Security             |
| Business        | Process Separation & additional Sec. |
| Consumer        | Performance and usability            | 

## IoT Relationship Platforms
- Solutions that support security features besides functional capabilities
- Used to build:
	- Asset management functions
	- Authentication and Authorization
	- Monitoring functions

## Cryptographic Security APIs
- Are called in the following instances:
	- Application data
		- Encryption
		- Authentication
		- Integrity protection
	- Network data/packet
		- Same as App data $\uparrow$
- Issues to *take into consideration*:
	- The need of secure communication to protect all application data "*end-to-end*"
	- Whether intermediate systems need access to data "*point-to-point*"
	- Whether security protection is only for data located on the device "*internal storage*"

## Authentication and Authorization
- The solution choice heavily depends on the deployment design
- Examples/Notes:
	- AWS Identity and Access Management (IAM) service to manage certificates
	- X.509 certificats
	- AWS SigV4
	- X.509 for MQTT for authenticating devices
	- Avoid using SSL for large scale IoT projects because they are not practical
	- Use IoT-specific certificates
	- Consider vendors that support **Identity Relation Management (IRM)**
- Another option is building your own security infrastructure
	- Very risky and should be attempted by organizations with considerable experience designing and securely deploying these infrastructures

## Security Monitoring
- It is very difficult 
- Use third party vendors and establish SLA with them 

# Safety and Security Design
## [[ThreatModeling|Threat Modeling]]
## Privacy Impact Assessment **PIA**
- Determine mitigations that must be included in the system design
- Determine any third-party agreement (SLA)
- For systems that store Privacy Protected Information (PPI), PIA will inform the design process as follows:
	- Provisioning of the device may require admin approval
	- Internal audit or compliance should be conducted to check the viability of storing PPI on the IoT device
	- Encryption of the data on the device should be sufficient
	- Data transmitted from/to the device should be encrypted
	- Access to the device should be restricted to authorized personal
	- End user should be aware of the use, transfer, disposal of PPI
- Link PIA outcomes to system requirements baseline, establish SLAs
## Safety Impact Assessment
- Items needs to be addressed:
		1. Is there anything harmful that could happen if the device stopped working? "*DoS Attack*"
		2. If the device is not safety critical, is there any device or service that depends on it?
		3. How could potential harm (from device failure) be minimized or avoided?
		4. What issues might others consider safety-related or harmful?
		5. Are there any other similar or related deployments that have been considered safety relevant or have done harm?
- It should take into consideration the various malfunctions or misbehaviors resulting from a device's vulnerabilities and possible compromises
## Compliance
- Depends on the specific industry regulatory environment 
- It is critical to examine **all of ** the physical and logical points of connection in the IoT deployment
- Some Compliance Regimens:
	- PCI (Payment Card Industry)
	- NERC (North America Electric Reliability Corp.)
	- USPS (US Postal Service)
	- SAE (Society of Automation Eng.)
	- NIST (National Institutes for Standards and Technology)
	- HIPPA
## Monitoring for Compliance
- **Pwnie** Provides security engineers with the ability to validate:
	- Policies
	- Configurations
	- Controls
## Security System Integration
This implies that devices can securely provision identities, credentials, undergo testing, monitoring, audit, and be securely upgraded

Artifacts from [[ThreatModeling|threat modeling]], [[#Privacy Impact Assessment PIA|PIA]], [[#Safety Impact Assessment|SIA]] and [[#Compliance|compliance]] should be used as inputs into an overarching IoT security system design.

### Secure Bootstrap
It concerns the process associated with initial provisioning of passwords, credentials...

Security process necessary to ensure that a new device undergoes the following:
- Receives a secure configuration that complies to a security policy
- Receives knowledge of its network, subnet, protocols, ports ...etc.
- Receives knowledge of the network and backend (trust anchors and paths) *installing cryptographic keys*
- Register its identity to the network

### Accounts and Credentials
- Consider the IoT devices's identity management in the larger enterprise
- Comes after provisioning of certificates

### Patching and Update
- Concerns how SW and FW are provisioned to IoT devices
- Musts for OTA activation and updating:
	- End-to-End SW/FW integrity and auth (in many cases confidentiality may also be needed)
	- The patching available for highly privileged roles and identities

### Audit and Monitoring
Concerns the enterprise security systems and their ability to capture and analyze for anomalies

# Process and Agreement
> Putting the right process and procedures in place is required to establish a strong security foundation
## Secure Acquisition Process
- Layout rules for acquiring new IoT devices
## Secure Update Process
- Design a secure update process
- Include the operational testing of updates and patches
## Establish SLAs
- Include security objectives in SLAs with IoT vendors:
	- Time to patch after a new critical update is available
	- The time to respond to an incident involving the device
	- IoT device availability
	- How the vendor handles privacy of data
	- Compliance targets
	- Incident response functions and collaboration agreements
	- How the vendor handles confidentiality of the data
	- Cloud SLA

## Establish Privacy Agreements
- Artifacts from [[#ThreatModeling|threat modeling]] should be used to understand the flow of data across all organizations, and agreements should be drawn up by all organizations involved in those data flows
- Content example of privacy agreement:
	- How the data will be processed
	- What regulations the data transfers fall under
	- ...etc

## Consider new liabilities and guard against risk exposure
- IoT is focused on network-enabled physical objects
- Organizations must begin to consider what new liability connected devices may introduce
## Establish an IoT physical security plan
- Spend time understanding the physical security needs of an IoT implementation
- It impacts architectural design, policies, and procedures and even technology acquisition approaches
- The output from the threat model should guide the plan creation and take into account IoT assets are placed in exposed location
- Deployment of monitoring solution