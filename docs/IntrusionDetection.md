# Intrusion Detection Systems (IDS)
## Network Intrusion Detection Systems (NIDS)
- A device or software which monitors all traffic passing a strategic point for malicious activities
- When such an activity is detected, an alert is generated and set to the admin

## Taxonomy
### Placement Strategy
#### Centralized / Network-based
- The agent is hosted at the edge of the network
- The main advantages:
	- Availability of richer computing
	- Availability of communication and storage resources
	- Leveraging the advances in edge computing
	- Efficient detection of attacks originating externally

#### Distributed / Host-based
- The agents are hosted at the devices
- A number of NIDS may be connected to a set of strategic routers and gateways

#### Hybrid
- The agents are distributed in a hierarchical fashion

### Detection approach
#### Signature-based
- Based on previous attack signatures, patterns or behaviors
- Detect known attacks

#### Anomaly-based
- Based on deviations from normal / benign behaviors or patterns
- Detect unknown attacks