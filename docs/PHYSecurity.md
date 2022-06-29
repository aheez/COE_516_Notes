# Physical Layer Security

## Attacks
### Spoofing
- The masquerading of an illegitimate device as being legitimate
- This type of attack has several implications such as the intrusion of an adversary into the network

### Jamming
- The directed degradation of a legitimate device's receiver channel by an adversary
- By saturating the channel with noise

### Eavesdropping
- The unauthorized and undetected interception of the communication between devices
- The intercepted messages can be used for future malicious intents

## Defences
Using some kind of characteristic in the medium of communication.

### Directional Modulation
- By narrowing the signal to the legitimate receiver, the amount of information that an adversary can collect is substantially reduced
- It requires that knowledge of an adversary be known to the system as well costly directional antennas

### Artificial Noise
- It is a technique to protect the information relayed from one node to another by disguising it as noise or directly jamming an adversary's receiver with noise.
- It can be power-inefficient
- It requires MIMO antennas as well as knowledge of an adversary's location

### RF Fingerprinting
- Along with Intrusion Detection System (IDS), RF fingerprint-based schemes can be used to distinguish devices
- The RF finger prints are derived from the unique differences obtained by transceivers in the manufacturing process
- This leads to unique features that can be used to differentiate transceivers such as frequency deviation

### Spread Spectrum (SS) Coding
- Performed though pseudo-random operations such as hopping between frequency channels in FHSS
- CSS is used in LoRa networks and does not introduce pseudo-random elements to aid in disguising signals

### Beam-forming
- Include techniques that:
	- Minimize the information leakage of transmitted signals 
	- Hinder an adversary's channel
- Destructive interference:
	- Used by IoT devices while simultaneously canceling it and exchanging secret keys for encryption
	- No prior knowledge on the location of an adversary is needed
- Cooperative Jamming (CJ):
	- Uses 3rd device to actively targets adversaries in order interfere with their attemps
	- Precoding techniques are used to not affect the communication between legitimate devices
	- 