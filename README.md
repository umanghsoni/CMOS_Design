# Basics of NMOS Drain current (Id) vs Drain-to-source Voltage (Vds)

## Introduction to Circuit Design and SPICE Simulation
### 0.	Why do we need SPICE simulations?

CIRCUIT DESIGN 

Logic Gates, Inverters, Buffers, etc. – Basic Entity is PMOS/NMOS – Connected in particular fashion – perform certain functionality 

Upon the completion of circuit design – fed with certain waveforms – identify output characteristics 

Example

<img width="236" height="235" alt="image" src="https://github.com/user-attachments/assets/71b71b0a-e215-4aef-9e1a-ba9936e1b06b" />
 	 
Circuit Design (Inverter)	

<img width="402" height="236" alt="image" src="https://github.com/user-attachments/assets/f2c1bab3-889b-4bfe-8997-e3a9659b9c43" />

Output Characteristics

<img width="368" height="181" alt="image" src="https://github.com/user-attachments/assets/506314df-279d-42e9-82f9-84eb2696d86f" />

 	
Delay dependency of Inverter	

Delay dependency - Obtained by simulating the NMOS/PMOS using the SPICE – Requires to tune ratio of W/L 

W/L ratio decides value of the current in the output characteristics – Current decides the delay profile of the circuit (Inverter, here)

To tune delay --> Tune W/L – SPICE Simulation 

NEED OF SPICE SIMULATION 

Consider the example – functionality of Clock tree synthesis on the buffer circuit – Drive the different capacitive load at the output

<img width="494" height="172" alt="image" src="https://github.com/user-attachments/assets/6396ad23-5c63-496f-9f3f-ac9a6e5e3123" />

(Buffers used in Clock Tree synthesis to drive the different capacitive load)	

Assume A,B,C – come up from calculation 

All the buffer made from the different PMOS/NMOS – Hence they have different delay profile


Objective – Prepare the delay table that don’t require to run the SPICE simulation every time

 	 
<img width="320" height="367" alt="image" src="https://github.com/user-attachments/assets/bbca2f19-e78b-45f0-9556-0fa9be2e3156" />
<img width="306" height="369" alt="image" src="https://github.com/user-attachments/assets/cdfd0edb-ad54-4f41-8f93-7cbd577df41d" />


Both Delay table – different W/L Ratio – causes different delay table - Intersection of Row and Column – Delay value for corresponding the slew input and output capacitive load

If any pair is not found – Interpolation can be used to find the nearest the estimation of delay value

3 Questions to Understand.

(1)	From where does the value of delay table comes? What is the source? 

(2)	How about their accuracy?

(3)	How to validate the static timing value? How to trust? 

Need of SPICE Simulation + Circuit Design + Characterizing of PMOS/NMOS

### 1.	Introduction to basic element in Circuit design – NMOS

NMOS – Basic Circuit element – 4 terminals – build using P substrate 

Source – Drain – Gate – Body

<img width="575" height="535" alt="image" src="https://github.com/user-attachments/assets/af672898-c965-4711-9560-2e482653fc80" />

<img width="572" height="115" alt="image" src="https://github.com/user-attachments/assets/43b72e50-8b5f-462a-b84a-fb6bbe4178bd" />

Threshold voltage – minimum voltage between gate and source that make the device turn-on – inversion channel forms 

Threshold voltage Equation 

<img width="519" height="221" alt="image" src="https://github.com/user-attachments/assets/cd63e415-c3ec-46ad-8d6d-ae4dbc4f7a6e" />

Channel (between source and drain) – very high resistance – as both junctions are connected to 0V – no connectivity between source & drain – Nothing conducting

When +VGS is given – Metal plate – become positive charge – device forms 2 terminal MOS capacitor - Positive charge carrier repelled deep into the substrate and replaced by immobile negative charge carrier – causes to have depletion region under the gate region

<img width="606" height="313" alt="image" src="https://github.com/user-attachments/assets/361af686-e0c5-4d20-a51b-ebf3cb137ff3" />

### 2.	Strong inversion and threshold voltage

When +VGS is given – accumulation of negative immobile ions in the depletion region under the gate – Besides – depletion region is formed under the source and drain region 

Depletion region – formed between source to gate to drain 

When +VGS is given – depletion area start depleting more majority charge carrier

<img width="550" height="229" alt="image" src="https://github.com/user-attachments/assets/58637ad5-2358-44b9-b567-b009cc6cf90e" />

Let us further increase +VGS - width of depletion area increase – at one value of VGS, surface near the Gate Oxide is inverted – known as surface inversion or strong inversion – surface near the Gate oxide is no more P type semiconductor – Becomes N Type semiconductor

<img width="508" height="258" alt="image" src="https://github.com/user-attachments/assets/dc4c2e17-87a7-4293-b739-a310c2ece1c5" />

VGS at which strong inversion happen – called as threshold voltage

When VGS is increased beyond threshold voltage – No more further width of the depletion region increase – No further Positive charge (of the substrate) carrier repelled deep into the substrate – causes to have attraction of minority charge carrier from the heavily doped source to channel – causes to increase width of channel

<img width="360" height="313" alt="image" src="https://github.com/user-attachments/assets/8ecac1c9-81f3-4c69-b1d7-a1fd9f9954a2" />

If VGS is continuously increasing, at one VGS value – continuous channel formation between source and drain – Now conductive path is formed – Resistance become decreased – allow the flow of the current between source and drain - 

<img width="384" height="222" alt="image" src="https://github.com/user-attachments/assets/c907e5a3-edd2-46c6-99bf-6438f729eac6" />

Effect of Body terminal on threshold – consider two scenarios  

Consider the VSB is positive – wider depletion region near the source region than drain side – due to additional reverse bias between substrate and source - 

<img width="377" height="302" alt="image" src="https://github.com/user-attachments/assets/a69bc3c6-9b9b-4cd6-a996-d1c024606ae8" />


### 3.	Threshold voltage with positive substrate potential

Two situations – (1) VGS with VSB = 0V (2) VGS with VSB = +VE voltage 

When +VGS is increases – width of depletion region increases in both cases – expected the accumulation of the negative charge carrier 

<img width="940" height="396" alt="image" src="https://github.com/user-attachments/assets/1c09bd9b-1eb5-4e91-ab68-92709887160c" />

In case (2), phenomena is different – Source to Substrate junction attract accumulated charge carrier from the channel – VGS is trying to form the channel whereas VSB is preventing 

<img width="374" height="274" alt="image" src="https://github.com/user-attachments/assets/11147bfb-3618-4e12-bd68-cc1b5e39cce8" />

In case (2), High VGS require to form the channel compare to (1) – Channel area near the drain is inverted whereas situation is not same at the source end

<img width="716" height="302" alt="image" src="https://github.com/user-attachments/assets/2101d39d-79b6-4916-b630-3009934ccbc4" />

High VGS require to form the channel compare to (1) – Channel area near the drain is inverted whereas situation

<img width="733" height="331" alt="image" src="https://github.com/user-attachments/assets/dbb939a1-0aec-4f67-88e1-cbe348ce76bb" />

<img width="463" height="177" alt="image" src="https://github.com/user-attachments/assets/355f20d9-6737-470a-ad07-832254571da7" />

Vt – Dependency on technological/device parameters – i.e. – Doping concentration of substrate – Doping concentration of n+ region 

γ — body effect coefficient — shows threshold voltage sensitivity to body bias — depends on substrate doping — depends on oxide capacitance

Other than VSB – rest values are constant – coming from foundry – these constants are fed to SPICE simulation  

<img width="318" height="158" alt="image" src="https://github.com/user-attachments/assets/9b66ac41-aefc-40c1-a5e0-2bff31aa07d5" />

Cox derived from the gate oxide thickness – others are constant or coming from the foundry – γ obtained – fed to find Vt – representing MOS with specified parameters 

<img width="355" height="88" alt="image" src="https://github.com/user-attachments/assets/aae01f63-fad4-4587-a5ad-ba0cdff7293b" />

Here – same case - parameters are either constant or coming from the foundry

SPICE Simulation – feed the parameter that represent particular NMOS – get ID-VD characteristics 

Reached to the threshold voltage – Observe resistive operation when (1) When increases VGS above threshold (2) When VDS is applied

## NMOS resistive region and saturation region of operation

### 4.	Resistive region of operation with small drain-source voltage

MOS Transistor operates – 3 regions – when VGS < Vt : Cut-off region 
                                                
Threshold voltage: minimum VGS that creates the strong inversion under the GATE between the Drain and Source 

Observe when VGS > Vt

<img width="668" height="411" alt="image" src="https://github.com/user-attachments/assets/0d114e43-ff3a-4f89-a302-3613bf6defb8" />

<img width="591" height="62" alt="image" src="https://github.com/user-attachments/assets/014754ad-bfa9-4874-844f-25fa5f1079a5" />

Assume the case when VDS is also given

 <img width="569" height="33" alt="image" src="https://github.com/user-attachments/assets/e27943d1-63e6-4fa1-965d-56067264278c" />

 <img width="474" height="352" alt="image" src="https://github.com/user-attachments/assets/80f02cbb-a369-4fce-936f-1ab756162fd9" />

 Voltage difference (Potential gradient) between the ends of the channel – one end connected to the source which is grounded – other end connected to Drain connected to +VE supply voltage 

 Voltage across the channel in the presence of VDS is not constant – was constant when VDS was 0

<img width="490" height="341" alt="image" src="https://github.com/user-attachments/assets/37349ef7-94d7-45c0-9d9e-203ba75fdb89" />

Voltage in channel is the function of distance (x) – At any point, voltage in the channel (In the presence of VDS) – Gate-to-Channel voltage is VGS-V(x)

### 5.	Drift current theory

Effective channel voltage at any point in the channel: VGS – V(X)

When X = 0 (source End) --> V(X) = 0

When X is considered at Drain end --> V(X) = VDS

<img width="493" height="342" alt="image" src="https://github.com/user-attachments/assets/e17f6882-e433-4cde-ad7a-c6b2724af678" />

Effective channel voltage – Ranges from 1V to 0.95V – Gradient – goes from higher (source) to lower (drain) 

 VGS > Vt  – create the equivalent amount of induced charge in the channel (When VDS = 0V)

 <img width="271" height="30" alt="image" src="https://github.com/user-attachments/assets/46568dfd-7e48-4515-ad54-41a6b6580aa1" />

 When VDS is connected to supply and VGS > Vt, induced charge at any point in the channel  

<img width="278" height="84" alt="image" src="https://github.com/user-attachments/assets/b5c9c834-62f1-473d-995f-8758e9e84136" />

Current Derivation

<img width="345" height="197" alt="image" src="https://github.com/user-attachments/assets/d0c0592e-e1be-408c-b848-bb8e2f8340c6" />

tox = constant - based on the technology node – example – 100 nm node – decided by foundary

eox = constant 

these are fed to SPICE simulation

Two types of current – diffusion current – Drift current 

As the channel ends have potential difference, drift current is considered – charge carrier flows from source to drain 

<img width="434" height="108" alt="image" src="https://github.com/user-attachments/assets/7310039b-d78d-4b85-af72-c4fcfee68b3c" />

<img width="940" height="509" alt="image" src="https://github.com/user-attachments/assets/65bb5f2e-a4f1-4c0f-ab38-b85b4a479402" />

Require to put value of velocity of charge, available charge – Integrate over whole channel width to have drain current value

### 6.	Drain current model for linear region of operation

Velocity of the charge carrier – not constant due to voltage gradient in the channel 

<img width="384" height="258" alt="image" src="https://github.com/user-attachments/assets/3c50f840-a44e-4f24-bd84-624807d1c977" />

dV – change in the channel voltage – can go from 0 to VDS

dX – change in the channel – can go from 0 to L

<img width="386" height="121" alt="image" src="https://github.com/user-attachments/assets/f9ee50ba-e390-4a54-b6b4-aa3ff3bb0fba" />

By Integrating over respective ranges in RHS and LHS

<img width="355" height="187" alt="image" src="https://github.com/user-attachments/assets/a300a703-3da6-4acd-9bd9-6e954a4a5a2f" />

Equation – model of MOSFET - µn, Cox, W/L, kn’, kn – Constant - technological parameter – model parameter – require to pass to SPICE simulation to computer drain current

We can’t say that Id is in linear region as Id is quadratic function of Vds. 

Let us put the values in the derived equation

<img width="642" height="173" alt="image" src="https://github.com/user-attachments/assets/be637b7a-8ed0-49a1-8d53-a51a91692bc6" />

(Vds)2 is almost zero when Vds <= (Vgs-Vt) 

Condition for the linear region - Vds <= (Vgs-Vt)

<img width="322" height="75" alt="image" src="https://github.com/user-attachments/assets/b87c5bc7-782b-4201-8946-e570f69306e9" />

As long as condition is satisfied – Id is said to be linear function of Vds – Small value of Vds generally satisfy this condition

### 7.	SPICE conclusion to resistive operation

Requires to see the impact of Vgs and Vds on Id when both are varied – How the device behave when these two voltages are getting changed

Analyse effect of VGS and VDS on ID — use multiple voltage values — device stays in linear region when VDS < (VGS − Vt) — fix VGS — sweep VDS from 0 to (VGS − Vt) — compute ID using linear-region equation — verify ID–VDS curves with SPICE simulations

<img width="629" height="184" alt="image" src="https://github.com/user-attachments/assets/b657f191-c27e-47d5-93d7-1d26a89a5f04" />

### 8.	Pinch-off region condition

Channel voltage at drain-end: VGS – VDS

Channel voltage > Vt to form surface inversion – requirement to turn on the device 

<img width="464" height="316" alt="image" src="https://github.com/user-attachments/assets/8ce267fc-8737-4217-9961-1fc9c977e81e" />

Varying the VDS while keeping VGS and Vt constant – feed to SPICE simulator 

Important to understand when channel voltage (VGS – Vt) < Vt 

As long as channel voltage (VGS – Vt)  > Vt – valid conducting channel exist in between source and drain

<img width="589" height="286" alt="image" src="https://github.com/user-attachments/assets/44834c2f-ec92-47b1-9597-0d656d37b800" />

When channel voltage (VGS – Vt)  = Vt – two different scenario at source end and drain end –Surface inversion at source end has already happened as channel voltage at source end is higher than Vt – Surface inversion is just happened as channel voltage at Drain end is exactly at Vt – mix and max of two concepts -  channel will start disappear from the drain side – this phenomena is known as pinch-off situation   

<img width="609" height="302" alt="image" src="https://github.com/user-attachments/assets/de41f7f0-e1d2-4768-8ebc-ad6888abc1f5" />


<img width="352" height="352" alt="image" src="https://github.com/user-attachments/assets/c50ea869-2672-471a-acb3-009af5a9a653" />

On or After the pinch-off situation – further increase in VDS cause MOSFET to drive in saturation - current will not stop flowing – linearity will change 

<img width="678" height="333" alt="image" src="https://github.com/user-attachments/assets/b2792174-c8bb-46a3-b742-d7f497acd298" />

Pinch-off situation – converted in model or current equation – feed the SPICE simulator

