# Kitsune: An Ensemble of Autoencoders for Online Network Intrusion Detection
> Based on ANNs

## Online 
- After the training or executing the model with an instance, the instance is immediately discarded

## Unsupervised
## Low Complexity
## ANNs
| Term   | Symbol |
| ------ | ------ |
| Weight | $$W$$  |
| Layer  | $$l$$  |
| Bias   | $$b$$  | 

$$
\theta \equiv (W,b)
$$
$\overrightarrow{x}$  is the normalized input vector (i.e., between [-1, 1]) using zscore normalization.

Let $\overrightarrow{a}^{(i)}$ be the $||l^{(i)}||$ vector of output from the neurons $l^{(i)}$
$$
\overrightarrow{a}^{i+1} = f (W^{(i)} . a\overrightarrow{a}^{(i)} + b^{(i)})
$$
Where $f$ is the neurons activation function (eg, sigmoid function)
$$
f (\overrightarrow{x}) = \frac{1}{1+e^\overrightarrow{x}}
$$

The output of the last layer is denoted as $\overrightarrow{y^`} = \overrightarrow{a}^{(L)}$ 
Let $h$ be the full layer-wise forward propagation from the inout $\overrightarrow{x}$  until the final output $\overrightarrow{y^`}$, denoted 

$$
h_\theta(\overrightarrow{x}) = \overrightarrow{y^`}
$$


### Training
- Training data set $X$ and the expected output set $Y$, where $\overrightarrow{x}\in X$ and $\overrightarrow{y}\in Y$
- Back propagation step is denoted as the function $b_\theta = (Y,Y^`)$
- Given some execution of $h_\theta$, let $A$ be every  neuron's activation and $\Delta$ be the activation errors of all neurons.
### Al 1
- Given the current $A$ and $\Delta$, and a set learning rate $l \in (0, 1]$
- This is referred to as batch-processing
- Both $W$ and $b$ are optimized by Gradient Descent (GD) algorithm
![[Pasted image 20220724065430.png]]

### Al 2
- Stochastic GD (SGD)
![[Pasted image 20220724070516.png]]

> The difference between GD and SGD is that GD converges on an optimum better than SGD, but SGD initially converges initially converges faster

## Autoencoders
- It tries to learn the function $h_\theta (\overrightarrow{x}) \approx \overrightarrow{x}$
- If the autoencoder is symmetric in layer sizes it can be used for decoding
- Root Mean Square Error (RSME)
$$
\operatorname{RMSE} = \sqrt{\frac{\sum _{i=1}^n (x_i-y_i)^2}{n}}
$$

### Anomaly Detection with Autoencoders
Let:
- $\phi$  be the anomaly threshold with initial value of -1
- $\beta \in [1, \infty)$ sensitivity parameter

#### Training phase
For each instance $x_i$ in the training set $X$
1. Execute $s = \operatorname{RMSE}(\overrightarrow{x}, h_\theta(\overrightarrow{x}))$
2. Update: if $(s \geq \phi)$ then $\phi \leftarrow s$
3. Train: update $\phi$ by learning from $x_i$

#### Execution phase
When an unseen instance $\overrightarrow{x}$ arrives:
1. Execute: $s = \operatorname{RMSE}(\overrightarrow{x}, h_\theta(\overrightarrow{x}))$
2. Verdict: if $(s \geq \phi\beta)$ then generate **ALERT**

## Architecture
![[Pasted image 20220724084000.png]]
- Features are mapped to visible neurons of the ensemble
- The autoencoders attempts to reconstruct the instance's features and compute the error in terms of Root Mean Square Error (RMSE)
- The RMSEs are forwarded to an output autoencoder, which acts as a non-linear voting mechanism for the ensemble

### Packet Capturer
![[Pasted image 20220724083946.png]]
- Acquiring the raw packets
- Examples: tshark, NFQueue

### Packet Parser
![[Pasted image 20220724083934.png]]
- To obtain the meta information required be [[#Feature Extractor FE| (FE)]]
- Example: Packet++, tshark

### Feature Extractor (FE)
![[Pasted image 20220724083839.png]]
- The component responsible for extracting $n$ features from the arriving packets to create the instance $\overrightarrow{x} \in \mathbb{R}^n$
- The features of $\overrightarrow{x}$ describe the packet

### Feature Mapper (FM)
![[Pasted image 20220724084026.png]]
- Forms a set of of smaller instances $(v)$ from $\overrightarrow{x}$ and passing $v$ to [[#Anomaly Detector AD| AD]]
- Learns the mapping from $\overrightarrow{x}$ to $v$
- The map groups features of $\overrightarrow{x}$ into sets with maximum size of $m$ each
- Nothing is passed to [[#Anomaly Detector AD| AD]] until the map is complete
- At the end of the train-mode the map is passed to [[#Anomaly Detector AD| AD]]
- The learned mapping is used to form a collection of small instances $v$ from $\overrightarrow{x}$, which is then passed to the respective autoencoders in the ensemble layer of the [[#Anomaly Detector AD| AD]]

### Anomaly Detector (AD)
![[Pasted image 20220724085018.png]]
- Responsible for detecting abnormal packets given a packet's representation $v$
- The RMSE of the forward propagation is then used to train the output layer
- The largest RMSE of the output layer is set as $\phi$  and stored for later use
- In testing, $v$ is executed across all layers, and if the output layer RMSE exceeds $\phi\beta$, an alert is logged with packet detailed
- The original packet, $\overrightarrow{x}$ and $v$ are discarded

## Kitsune 
### [[#Feature Extractor FE]]
- Use incremental Statistics maintained over a damped window
- Which means the extracted features are temporal 

#### Damped Statistics 
-  Statistics whose computation involves one and two incremental statistics are referred to as 1D and 2D statistics respectively.
- Maintains a tuple: $\mathrm{IS} := (N,LS,SS)$, where $N,\ LS\mathrm{and}\ SS$ are the number, linear sum and squared sum of instances seen respectively
- Update procedure for inserting $x_i$ into $\mathrm{IS} \leftarrow (N+1, LS+x_i + SS +x_i^2)$
- The statistics at any given time are:
$$
\mu_S = \frac{LS}{N}, \ \ \sigma_S^2 = \Bigg|\frac{SS}{N}-\left(\frac{LS}{N}\right)^2\Bigg|, \ \ \sigma_S = \sqrt{\sigma_S^2}
$$
- In damped window model, the weights of older values are exponentially decreased over time using a decay function $d_\lambda(t) = 2 ^{-\lambda t}$, where $\lambda > 0$ 
- The tuple of a damped incremental statistics is defined as:
$$\mathrm{IS}_{i,\lambda}:= (w, LS,SS,SR_{i,j},T_{last})$$
- Where:
	- $w$ is the current weight
	- $T_{last}$ is the timestamp of the last update of $\mathrm{IS}_{i,\lambda}$ and $SR_{i,j}$ is the sum of residual products between streams $i$ and $j$
- To update $\mathrm{IS}_\lambda$ with $x_{cur}$ at time $t_{cur}$, Algorithm 3 is preformed

 ![[Pasted image 20220724093512.png]]
 
 ![[Pasted image 20220724111209.png]]

- Whenever a packet arrives we extract a behavioral snapshot
- The snapshot consist of 115 traffic statistics capturing a small window into:
	1. Packet sender in general
	2. The traffic between the packet's sender and receiver
- The statistics summarize all of the traffic:
	- Source MAC and IP address (SrcMAC-IP)
	- Source IP (SrcIP)
	- sent between a given packet's source and destination IPs (Channel)
	- sent between a given packet's source and destination TCP/UDP socket (Socket)
- A total of 23 features can be extracted from a single time window $\lambda$
- Five time windows:
	- 100ms
	- 500ms
	- 1.5sec
	- 10sec
	- 1min
	
 ![[Pasted image 20220724111347.png]]