# IoT Landscape and Anatomy
## Market Segmentation
- IoT2C
	- Home
	- Lifestyle
	- Health
	- Mobility
- IoT2B
	- Retail
	- Health
	- Energy
	- Mobility
	- Cities
	- Manf.
	- etc.

## IoT anatomy
- Device: a piece of equipment with the mandatory capabilities of communication
- Thing: an object of the physical world or the information world, which is capable of being identified and integrated into communication networks

## IoT Device Lifecycle
- Device implementation
- Service Implementation
- Device and Service Deployment

## Anatomy

### Hardware
#### Selection criteria
- Needed performance
- IoT system as whole must be considered
- Organization requirements
- Security requirements (Separation of kernels, process isolation, information flow control)

### Operating Systems
#### Selection Criteria 
- Needed performance
- Needed functional and non-functional requirements, e.g.:
	- Security features 
	- Computing capabilities
	
#### RTOS examples
TinyOS, Contiki, Mantis, FreeRTOS, MbedOS

### Communication
#### Vertical Communication
Communication between layers in the IoT stack

#### Horizontal Communication
- D2D
- APIs used to interface connected workflows to diverse IoT product types

#### Protocols
##### Messaging Protocols (APP Layer)
- MQTT
- CoAP
- XMPP & XMPP-IoT (Extensible Messaging and Presence Protocol); based on XML
- DDS (Data Distribution Service)
- AMQP (Advanced Message Queuing Protocol)

##### Transport Protocols
- TCP
- UDP

##### Network Protocol 
- 6LoWPAN

##### Data Link & PHY 
- IEEE 802.15.4
- ZWave
- BLE and it derivitives
- PLC
- Cellular