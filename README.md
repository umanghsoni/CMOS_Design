# 📑 Table of Contents

- [Basics of NMOS Drain Current (Id) vs Drain-to-Source Voltage (Vds)](#basics-of-nmos-drain-current-id-vs-drain-to-source-voltage-vds)
  - [Introduction to Circuit Design and SPICE Simulation](#introduction-to-circuit-design-and-spice-simulation)
    - [0. Why do we need SPICE simulations?](#0-why-do-we-need-spice-simulations)
    - [1. Introduction to basic element in Circuit design – NMOS](#1-introduction-to-basic-element-in-circuit-design--nmos)
    - [2. Strong inversion and threshold voltage](#2-strong-inversion-and-threshold-voltage)
    - [3. Threshold voltage with positive substrate potential](#3-threshold-voltage-with-positive-substrate-potential)

  - [NMOS Resistive Region and Saturation Region of Operation](#nmos-resistive-region-and-saturation-region-of-operation)
    - [4. Resistive region of operation with small drain-source voltage](#4-resistive-region-of-operation-with-small-drain-source-voltage)
    - [5. Drift current theory](#5-drift-current-theory)
    - [6. Drain current model for linear region of operation](#6-drain-current-model-for-linear-region-of-operation)
    - [7. SPICE conclusion to resistive operation](#7-spice-conclusion-to-resistive-operation)
    - [8. Pinch-off region condition](#8-pinch-off-region-condition)
    - [9. Drain current model for saturation region of operation](#9-drain-current-model-for-saturation-region-of-operation)

  - [Introduction to SPICE](#introduction-to-spice)
    - [10. Basic SPICE setup](#10-basic-spice-setup)
    - [11. Circuit description in SPICE syntax](#11-circuit-description-in-spice-syntax)
    - [12. Define technology parameters](#12-define-technology-parameters)
    - [13. First SPICE simulation](#13-first-spice-simulation)
    - [14. SPICE Lab with sky130 models](#14-spice-lab-with-sky130-models)

- [Velocity Saturation and Basics of CMOS Inverter VTC](#velocity-saturation-and-basics-of-cmos-inverter-vtc)
  - [SPICE Simulation for Lower Nodes and Velocity Saturation Effect](#spice-simulation-for-lower-nodes-and-velocity-saturation-effect)
    - [15. SPICE Simulation for lower nodes](#15-spice-simulation-for-lower-nodes)
    - [16. Drain Current vs Gate Voltage](#16-drain-current-vs-gate-voltage-for-long-and-short-channel-device)
    - [17. Velocity saturation at lower and higher electric fields](#17-velocity-saturation-at-lower-and-higher-electric-fields)
    - [18. Velocity saturation drain current model](#18-velocity-saturation-drain-current-model)
    - [19. Labs sky130 Id-Vgs](#19-labs-sky130-id-vgs)
    - [20. Labs Sky130 Vt](#20-labs-sky130-vt)

  - [CMOS Voltage Transfer Characteristics (VTC)](#cmos-voltage-transfer-characteristics-vtc)
    - [21. MOSFET as a switch](#21-mosfet-as-a-switch)
    - [22. Introduction to standard MOS voltage current parameters](#22-introduction-to-standard-mos-voltage-current-parameters)
    - [23. PMOS/NMOS drain current vs drain voltage](#23-pmosnmos-drain-current-vs-drain-drain-voltage)
    - [24. Step 1 - Convert PMOS gate-source voltage to Vin](#24-step-1---convert-pmos-gate-source-voltage-to-vin)
    - [25. Step2 & Step3 – Convert voltages to Vout](#25-step2--step3--convert-pmos-and-nmos-drain-source-voltage-to-vout)
    - [26. Step4 – Merge PMOS–NMOS load curves](#26-step4--merge-pmos--nmos-load-curves-and-plot-vtc)

- [CMOS Switching Threshold and Dynamic Simulations](#cmos-switching-threshold-and-dynamic-simulations)
  - [Voltage Transfer Characteristics -- SPICE simulations](#voltage-transfer-characteristics----spice-simulations)
    - [27. SPICE deck creation for CMOS inverter](#27-spice-deck-creation-for-cmos-inverter)
    - [28. SPICE simulation for CMOS inverter](#28-spice-simulation-for-cmos-inverter)
    - [29. Labs Sky130 SPICE simulation for CMOS](#29-labs-sky130-spice-simulation-for-cmos)
  - [Static behavior evaluation -- CMOS inverter robustness -- Switching](#static-behavior-evaluation----cmos-inverter-robustness----switching)
    - [30. Switching Threshold, Vm](#30-switching-threshold-vm)
    - [31. Analytical expression of Vm](#31-analytical-expression-of-vm-as-a-function-of-wlp-and-wln)
    - [32. Analytical expression of W/L](#32-analytical-expression-of-wlp-and-wln-as-a-function-of-vm)
    - [33. Static and dynamic simulation](#33-static-and-dynamic-simulation-of-cmos-inverter)
    - [34. Increased PMOS width effect](#34-static-and-dynamic-simulation-of-cmos-inverter-with-increased-pmos-width)
    - [35. Applications in clock network and STA](#35-applications-of-cmos-inverter-in-clock-network-and-sta)

- [CMOS Noise Margin Robustness Evaluation](#cmos-noise-margin-robustness-evaluation)
  - [Static behaviour evaluation -- Noise margin](#static-behaviour-evaluation----cmos-inverter-robustness----noise-margin)
    - [36. Introduction to noise margin](#36-introduction-to-noise-margin)
    - [37. Noise margin voltage parameters](#37-noise-margin-voltage-parameters)
    - [38. Noise margin equation and summary](#38-noise-margin-equation-and-summary)
    - [39. Rail Error variation](#39-noise-marginrail-error-variation-with-respect-to-pmos-width)
    - [40. Sky130 Noise margin labs](#40-sky130-noise-margin-labs)

- [CMOS Power Supply and Device Variation Robustness Evaluation](#cmos-power-supply-and-device-variation-robustness-evaluation)
  - [Static behaviour evaluation -- CMOS inverter robustness -- Power supply variation](#static-behaviour-evaluation----cmos-inverter-robustness----power-supply-variation)
    - [41. Smart SPICE simulation for power supply variations](#41-smart-spice-simulation-for-power-supply-variations)
    - [42. Advantages and disadvantages using low supply voltage](#42-advantages-and-disadvantages-using-low-supply-voltage)
    - [43. Sky130 Supply Variations Labs](#43-sky130-supply-variations-labs)
  - [Static behaviour evaluation -- CMOS inverter robustness -- Device variation](#static-behaviour-evaluation----cmos-inverter-robustness----device-variation)
    - [44. Sources of variation -- Etching process](#44-sources-of-variation----etching-process)
    - [45. Sources of variation -- oxide thickness](#45-sources-of-variation----oxide-thickness)
    - [46. Smart SPICE simulation for device variations](#46-smart-spice-simulation-for-device-variations)
    - [47. Conclusion](#47-conclusion)
    - [48. Sky130 Device Variation Labs](#48-sky130-device-variation-labs)

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

### 9.	Drain current model for saturation region of operation

On or After the pinch-off situation – further increase in VDS cause MOSFET to drive in saturation – voltage over the channel – constant – (VGS – Vt) – no dependency on VDS

Saturation region – channel voltage remains constant = (VGS – Vt) 

Linear region – channel voltage depends on VDS = (VGS – V(X))

Effective channel length is smaller than effective gate length 

Effective channel length – modulated by VDS

<img width="450" height="336" alt="image" src="https://github.com/user-attachments/assets/792a70ee-aee6-4bad-bcb0-4975da651674" />

Deriving the current equation in saturation region, we can have following equations from the drain current model for linear region of operation

In linear region – Square of VDS – very near to 0 – Ignored

In saturation region – channel voltage – (VGS – Vt) – Replacing VDS by (VGS – Vt)

<img width="378" height="382" alt="image" src="https://github.com/user-attachments/assets/39150c73-1d63-46d4-af93-c2e3c15d4664" />

 Seems like – Id constant current – all parameters are constant - Not true – but has dependency on L and L has dependency VDS – Accurate equation requires to incorporate the effect of VDS

<img width="471" height="90" alt="image" src="https://github.com/user-attachments/assets/10ea1ee1-1c6f-449a-bdaa-84ab75a22ba2" />

Above equation – constant current equation in saturation region 

## Introduction to SPICE

### 10.	Basic SPICE setup

SPICE - Software – Simulation engine – has predefined model – requires to feed the values of input – requires to feed correct netlist – spice derive the waveform – used to calculate the delay of the cell – I & V waveforms are the backup for delay – accurate delay used to derive Static time analysis

Correct set up require 

Model equations represent the MOSFET device

<img width="490" height="277" alt="image" src="https://github.com/user-attachments/assets/2ea5cf80-e0ca-4486-a9e0-34d580963d28" />

Technological Constants (λ, γ, Vto, kn’) in the equations – coming from the foundry - based on 180nm node or 1.2 µm node – each technological node has unique value – these values require to provide to SPICE engine in terms of model files – these values should be accurate to have correct current and voltage

<img width="645" height="290" alt="image" src="https://github.com/user-attachments/assets/51d162a7-fff5-4f13-8cda-66c75ba63b24" />

SPICE Netlist – feed to SPICE engine in special format with certain syntax

<img width="426" height="198" alt="image" src="https://github.com/user-attachments/assets/7b7018c4-b447-4c10-af21-18774ebc9a50" />

Protection resistor to prevent the Gate – Two voltage supplies require to vary in order to get current voltage characteristics in a single shot using the SPICE Simulation  

### 11.	Circuit description in SPICE syntax

SPICE – own its syntax

Netlist – define the node – any component must be in between two nodes – name the nodes – no restriction in naming the nodes – can be text or numerical values

<img width="668" height="253" alt="image" src="https://github.com/user-attachments/assets/5061f06d-de12-47fc-a808-8e9f0d29df6c" />

<img width="523" height="56" alt="image" src="https://github.com/user-attachments/assets/0771ce34-b19d-44fd-8de6-61de55115b14" />

Anything starts with M is recognised as MOSFET with sequence of Drain, Gate, Source, Substrate

nmos – name coming from the technology file – exact name – followed by W and L

Anything starts with R is recognised as resistor, Anything starts with V is recognised as voltage source - 

<img width="384" height="64" alt="image" src="https://github.com/user-attachments/assets/aa9a2850-a695-40a5-ad1a-d8eef93f6cb4" />

For voltage source – sequence is important – positive terminal, negative terminal

<img width="534" height="130" alt="image" src="https://github.com/user-attachments/assets/6f4e9702-d6e9-433c-bdac-77f348ac973d" />

Netlist – represent the MOSFET

Next to define the technological file for the constant of the model

### 12.	Define technology parameters

Netlist file – nmos – particular device – having its own models 

<img width="453" height="110" alt="image" src="https://github.com/user-attachments/assets/be46f8b3-952c-4a0c-a026-2c82b1d70d36" />

nmos – when plug-in SPICE engine/simulator understand – from when it requires to picked – what are the constants/model parameters for the nmos – based on the constants it, evaluate threshold voltage and drain current

<img width="313" height="339" alt="image" src="https://github.com/user-attachments/assets/edc81f6e-9946-44a1-9eab-acca458eab92" />

Constants/model parameters are specific to technological node – example – 1.2µm, constants are different than other technological node – coming from the foundry – model equations for other technological node will remain almost same but equations might be modified for very small technological node

<img width="606" height="249" alt="image" src="https://github.com/user-attachments/assets/65e67e37-325c-4c3d-ac47-9c12fbbaffc0" />

You may have more than one devices in the netlist file

<img width="425" height="132" alt="image" src="https://github.com/user-attachments/assets/c9e5f94f-260c-40f9-b433-a57ff047af14" />

<img width="376" height="234" alt="image" src="https://github.com/user-attachments/assets/dcb2432f-73a9-4a5d-8890-eb4a4bbe8b83" />

Save this file with .mod extension – call this .mod file in top level netlist

<img width="382" height="154" alt="image" src="https://github.com/user-attachments/assets/4049e31e-bae4-40c8-9287-2ea6fde336d0" />

Here, CMOS_MODELS is the section in .lib from where it finds nmos – device constants are used evaluated threshold voltage, Drain current, etc. 

Anything between two set of *** is comment – will not be considered

Add simulation command – means – the way it voltage level is provided -  how VGS and VDS can sweep – SPICE simulation neede

<img width="591" height="233" alt="image" src="https://github.com/user-attachments/assets/e47383dc-f74b-4acf-a5e1-c75b2b1a54a7" />

Require to add sweep command that tell SPICE simulator to sweep VDS for a range

### 13.	First SPICE simulation

<img width="702" height="292" alt="image" src="https://github.com/user-attachments/assets/655a51b8-76bc-4b85-b037-58fca76505e3" />

Double click and virtual box manager window pop-up

<img width="611" height="531" alt="image" src="https://github.com/user-attachments/assets/50e12ae7-9465-49f1-9511-f308d5713232" />

Click on New – another window pop-up

<img width="447" height="308" alt="image" src="https://github.com/user-attachments/assets/d5f138dc-9e10-440b-83d5-aef5f06638c2" />

virtual box manager window pop – enter the details as per the image – Name can be as per user choice – click on finish

<img width="537" height="471" alt="image" src="https://github.com/user-attachments/assets/f60ffe4d-a354-48cd-b145-b6493b970f22" />

Select virtual machine 

<img width="608" height="536" alt="image" src="https://github.com/user-attachments/assets/be4fa549-c946-45c7-a1c7-6c591fb6df50" />

Ensure 7nm.vdi is selected in storage SATA Port 0 – click on start – new window with ubuntu machine will pop up – enter pwd – vsdiat

<img width="409" height="253" alt="image" src="https://github.com/user-attachments/assets/7d85b9d6-7f44-46e0-a871-92fbd1201714" />

Require to open the browser and go to the github to download the directory

<img width="599" height="380" alt="image" src="https://github.com/user-attachments/assets/60cfbcfa-5c8a-43b9-b573-8086839f6840" />

Open the terminal window

<img width="594" height="372" alt="image" src="https://github.com/user-attachments/assets/1b478ed8-1f3d-4aa9-bfd1-54039d25b2d7" />

go for git clone

<img width="573" height="363" alt="image" src="https://github.com/user-attachments/assets/f513a0e6-6b93-49fc-af9b-438533c0e1cf" />

Directory/folder will be saved in local PC

<img width="940" height="110" alt="image" src="https://github.com/user-attachments/assets/5ca83e15-e8c9-412d-92b5-77a5a2dca19a" />

Go to design folder - - > All SPICE File + folder (Has all tech files, cells and models)

<img width="940" height="109" alt="image" src="https://github.com/user-attachments/assets/01f53740-ae5a-4ed9-a0bb-c30558eee100" />

Let us visit the cells folder

<img width="940" height="66" alt="image" src="https://github.com/user-attachments/assets/57f9ce9f-d787-45ef-ac22-34bfeee41168" />

nfet_01V8, pfet_01V8 – entire workshop – these two cells will be used

Let us go to nfet_01v8 folder

<img width="940" height="113" alt="image" src="https://github.com/user-attachments/assets/4ffbc8b2-a91c-4684-a826-71bcb7b089ad" />

Different Library files for nfet_01v8 like ff, fs, corner, etc.  

Let us open library file in the viewer safe mode

<img width="940" height="102" alt="image" src="https://github.com/user-attachments/assets/20b74b39-a5cf-48c5-880f-d2b87382a82d" />

Will open typical corner nfet 

<img width="825" height="517" alt="image" src="https://github.com/user-attachments/assets/08075eff-fac5-42f0-90dd-d1cd6cf7906e" />

Model parameters coming 

Corner library files have different W-L values – has already pre-characterized few W-L values – In the design file, chose W-L values which are already pre characterized – any outside value of W-L will give error 

Now come out of cells directory and go to the models directory and open sky130.lib.spice file

<img width="940" height="78" alt="image" src="https://github.com/user-attachments/assets/f01338f4-2ebd-4523-a1b8-7a531d892d89" />

The model file has all library 

<img width="586" height="423" alt="image" src="https://github.com/user-attachments/assets/703426f3-fecd-4ac6-993a-d3e3842f522e" />

It contains all the library files for both nfet and pfet for different corner such as tt, ff, sf, etc

This is common files for both nfet and pfet at different corner

Now go back to design folder/directory and open the day1_nfet_idvds_L025_W065.spice using the vim editor

<img width="940" height="95" alt="image" src="https://github.com/user-attachments/assets/199f954f-d1b7-426a-a118-287cb09f0b3b" />

This command will open the file

<img width="388" height="541" alt="image" src="https://github.com/user-attachments/assets/2d5827a3-c3c1-42f0-9eb8-0931f9bf8679" />

Give commands to run day1 file using ngspice

<img width="649" height="454" alt="image" src="https://github.com/user-attachments/assets/06889722-b636-42ad-8744-7e5c85a9a452" />

Ngspice -command require to give

Type: plot -vdd#branch  - will pop up one window showing the graph

<img width="422" height="336" alt="image" src="https://github.com/user-attachments/assets/75f7a5c0-1e6f-4da7-a481-3f6f2ebf6292" />


To see id value from the graph, left click and go to the terminal window to see the value

<img width="461" height="183" alt="image" src="https://github.com/user-attachments/assets/584e7801-9545-474e-8930-68b83a2ddbc6" />

### 14.	SPICE Lab with sky130 models



# Velocity Saturation and basics of CMOS inverter VTC

## SPICE Simulation for lower nodes and velocity Saturation Effect
### 15.	SPICE Simulation for lower nodes

<img width="1204" height="466" alt="image" src="https://github.com/user-attachments/assets/ba831e80-bf28-484b-98af-fa110773b07d" />

•	Linear Region = Resistive Region – Condition for Saturation region condition – Current model for both region – Id = 0 in Cut-off region when VGS < Vt

•	If W/L ratio is constant from 1200 nm (1.2 µm) to 250 nm (0.250 µm) for different technological node – Id in saturation current seems same irrespective of the technological node but the case is not the true for the lower node

•	Observable things in two technological node – Current in saturation for 1.2 µm is higher than shorter node – The gap between adjacent curves for different Vgs is almost constant for shorter node while it is not constant for 1.2 µm.

### 16.	Drain Current vs Gate Voltage for long and short channel device

•	For longer node, at Vds = 2.5 (saturation region), the quadratic dependence – Id quadratic increase with increase in Vgs as per the Id equation (Consider the W/L ratio is maintained in both cases)

•	Reason behind different behaviour in saturation region is velocity saturation in short channel

<img width="939" height="453" alt="image" src="https://github.com/user-attachments/assets/4144cfff-f7b5-468b-a625-4efdf0508d11" />

•	Anything less than 250 nm is considered as short channel device

<img width="940" height="381" alt="image" src="https://github.com/user-attachments/assets/269364b3-002a-47c1-b895-372235dac861" />

•	Id-Vgs with Vds = 1.8V – L = 1.2 µm (long channel) is more curved than L = 0.25 µm (short channel) – L = 0.25 µm is more linear than L = 1.2 µm – Comparison is done for same W/L

<img width="940" height="347" alt="image" src="https://github.com/user-attachments/assets/97730a35-504c-4ace-ba5c-bffe42c8d864" />


### 17.	Velocity saturation at lower and higher electric fields

<img width="940" height="378" alt="image" src="https://github.com/user-attachments/assets/afdb1d5c-514f-4416-92eb-4b828f2d02c8" />

•	Short channel – initial behaviour still follows the quadratic relation followed by linear region operation due to velocity saturation

•	Concept of velocity saturation – for lower values of electric field, it follows the linear behaviour but after some critical electric field Ɛc, it tends to constants

<img width="940" height="410" alt="image" src="https://github.com/user-attachments/assets/897cf83f-5300-43e5-b72b-a0313ea2da54" />

•	Formula directly taken from the device physics

•	Rederiving the drain current – come up with complex formula – not good for hand calculation – Need for simple model equation

<img width="940" height="293" alt="image" src="https://github.com/user-attachments/assets/4e7e645e-ce22-4c1b-87cb-b6e35eeba298" />

•	Region of operation for long channel device is 3 whereas for short channel device, velocity saturation is the 4th region of operation

<img width="939" height="379" alt="image" src="https://github.com/user-attachments/assets/0ba17800-386e-4bba-b030-2ac2f543ebbd" />

### 18.	Velocity saturation drain current model

•	One drain equation represents all the regions by considering the minimum of Vgt, Vds and Vdsat. 

•	Earlier section, the effect of (1 + λVds) is considered in only saturation region but here it will be kept as for lower value of Vds, it will be vanished. 

•	Vdsat – voltage at which device velocity saturate – technological parameter – independent of Vgs and Vds – foundry parameter – open model file when the node is less than 250 nm to check the Vdsat value

<img width="515" height="186" alt="image" src="https://github.com/user-attachments/assets/ab267620-18e8-4202-9eda-ca2a5c063b15" />

•	When Vgt is minimum, it implies that Vds and Vdsat is higher – device goes in saturation – applicable for bot short channel and long channel device

•	When Vds is minimum – lower values of Vds, the device will operate in resistive/linear region of operation – due to smaller value of Vds, the term (1 + λVds) will be ignored – applicable for both short and long channel device

<img width="527" height="101" alt="image" src="https://github.com/user-attachments/assets/caa50389-1070-4bb7-b17a-379e2c022455" />

•	When Vdsat is minimum – device enter in velocity saturation – only in short channel device – when node is less than 250 nm 

<img width="532" height="99" alt="image" src="https://github.com/user-attachments/assets/35d98453-9117-46ae-97c3-a6d204d4044d" />

•	For short channel, peak saturation current is always lower than peak saturation current of long channel device – Compared on same W/L

<img width="940" height="406" alt="image" src="https://github.com/user-attachments/assets/cc04b56c-ec62-4a88-8e25-ac04a5e13f7f" />

 
•	Open source reference for SPICE Simulation

<img width="940" height="134" alt="image" src="https://github.com/user-attachments/assets/fd9ddd51-f659-41ea-b828-6caa165af4d5" />

### 19.	Labs sky130 Id-Vgs

•	Go for simulation – Open the file

<img width="940" height="32" alt="image" src="https://github.com/user-attachments/assets/24d8781b-e59a-4408-91a0-37bc3a3a9b96" />

•	Check the code – DC Simulation is going on – Vds is varied from 0 to 1.8V with sweep of 0.2 V – Vgs is also sweep from 0 to 1.8V in range of 0.2 V

<img width="485" height="413" alt="image" src="https://github.com/user-attachments/assets/32223b85-22a5-4d6d-998e-d458b7f42818" />

•	Run this file using the ngspice

<img width="929" height="34" alt="image" src="https://github.com/user-attachments/assets/b7ff5b89-320a-4a50-aea0-dbce5cbd03bb" />

•	Ngspice simulator will ask for plots – 

<img width="940" height="213" alt="image" src="https://github.com/user-attachments/assets/709aa293-e50b-4766-8b3f-679b4e4da556" />

•	Graph will open

<img width="622" height="391" alt="image" src="https://github.com/user-attachments/assets/f57a24d3-2a66-4fdc-a976-b6bf7ec932ad" />

•	Can be seen that lower values of Vgs shows the quadratic behaviour whereas for higher values of Vgs it shows the linear behaviour

•	Open – IdVgs for day2 – Keeping Vds constant for 1.8 V while sweeping Vgs from 0 to 1.8V with step of 0.2V

<img width="572" height="440" alt="image" src="https://github.com/user-attachments/assets/2d27a7ae-91da-4afa-8205-ad49cdae6c99" />

•	Will open ngspice and give command : plot -vdd#branch – Graph window will pop up

<img width="940" height="583" alt="image" src="https://github.com/user-attachments/assets/5e8185a5-18c3-4855-8e24-37cae0048450" />

### 20.	Labs Sky130 Vt

•	Finding the threshold voltage – take the tangent and extend the linear line on X axis – inceptor at X axis is the threshold voltage Vt

<img width="620" height="389" alt="image" src="https://github.com/user-attachments/assets/d109c3cd-62d7-4a07-a261-7bade9015351" />

## CMOS Voltage Transfer Characteristics (VTC)

### 21.	MOSFET as a switch

•	We have seen NMOS and PMOS with device physics point of view – need the change the perspective – focus on device properties for a MOSFET switch 

•	Below is the MOS transistor – irrespective of the n-channel or p-channel – condition for turning on - |Vgs| > |Vt|

<img width="940" height="316" alt="image" src="https://github.com/user-attachments/assets/6a5b3954-49b5-4235-8401-16515cb735ba" />

<img width="509" height="107" alt="image" src="https://github.com/user-attachments/assets/bcedbd93-65b5-4754-8b94-0ae87d3d929c" />

•	Let us connect NMOS and PMOS to have CMOS – Complementary MOS – NMOS is at Bottom – PMOS is at Top – Source of NMOS is connected to Vss (Ground) and PMOS is connected Vdd (Supply) – Drain of both MOS are connected and Output is taken from that junction – Gate of both MOS is connected and is considered as Vin

<img width="390" height="368" alt="image" src="https://github.com/user-attachments/assets/2c88ebe4-f833-4760-9f02-dad336133f47" />

•	When Vin = Vdd (High) ---> NMOS will turn on as |Vgs| > |Vt| satisfied for NMOS but not for PMOS – PMOS will turn off

•	When Vin = Vss (Low) ---> PMOS will turn on as |Vgs| > |Vt| satisfied for PMOS but not for NMOS – NMOS will turn off

### 22.	Introduction to standard MOS voltage current parameteres

•	We try to have equivalent circuit when Vin = Vdd and Vin = Vss – Merge those two cases to derive the VTS of CMOS – VTC will be used to evaluate the delay of any cell – Here, cell is inverter but it could be any Logic gate

•	Here connecting wires are used – they are not ideal, they are physical - they would have finite width, depth and length – Hence, resistance must be taken into consideration – It is not a regular resistor, it is having the non-linear function of your drain current – Here, ohm’s law is not applicable

<img width="525" height="565" alt="image" src="https://github.com/user-attachments/assets/9c610296-7006-4e79-aad0-1f1e1418595d" />

•	Turn off transistor is shown with open switch – when input is Vdd, NMOS is turn on – Output voltage Vout is zero – Capacitor totally discharge through Rn – Direct current path exist from Vout to Vss

•	When Vin = 0, direct current flow from Vdd to Vout – Capacitor charge to Vdd – Vout = Vdd 

•	Let us make names to the nodes for SPICE circuit 

<img width="409" height="354" alt="image" src="https://github.com/user-attachments/assets/b2570fa4-8bbe-47ff-9129-120e352558c7" />

### 23.	PMOS/NMOS drain current v/s drain drain voltage

•	Let us have some equation for VTC – what is input voltage provided and what is the output voltage received 

<img width="370" height="408" alt="image" src="https://github.com/user-attachments/assets/9cc51c32-dfa4-4fba-adfd-a7216a95c655" />

•	Pls be noted that IdsP and IdsN direction is opposite. Here NMOS curve is in first quadrant and PMOS is in the third quadrant. 

<img width="633" height="342" alt="image" src="https://github.com/user-attachments/assets/493f639e-6487-4539-9afb-1291622d031d" />

•	These two curves are very important to derive the VTC for the CMOS. 

### 24.	Step 1 - Convert PMOS gate-source voltage to Vin

•	Here in CMOS inverter, we have Vin as input and Vout as output – Internal node voltages are not visible – CMOS inverter is only the function of Vin and Vds – At what value of Vin, what value of Vout is expected – This is needed for VTC

•	Let us make VTC by considering any one of IdsN and IdsP – Convert IdsN v/s VdsN and IdsP v/s VdsP into IdsN v/s VdsP and IdsN v/s VdsN

•	Convert the VgsN and VgsP into Vin – Considering IdsN from IdsN and IdsP

<img width="611" height="474" alt="image" src="https://github.com/user-attachments/assets/f4d5fd78-ff2d-408e-9491-ee8cadf02c1c" />

•	Here, IdsP is negative of IdsN. Hence Negative axis converted into positive axis.

<img width="940" height="300" alt="image" src="https://github.com/user-attachments/assets/36d0bd51-6c5e-4199-a461-a287d238ddcf" />

•	When Vout = 2V, output capacitor is fully charges, there is no charging current flowing to output capacitor, there is 0 current. 

•	Here, the load curve is in form of Vin, Vout and IdsN for PMOS

### 25.	Step2 & Step3 – Convert PMOS and NMOS drain-source-voltage to vout

•	Load Curve for NMOS

<img width="708" height="301" alt="image" src="https://github.com/user-attachments/assets/175dbf31-d78d-47ff-9763-cf6a601b4931" />

•	Consider the Load curve for NMOS and PMOS and merging both two curves for VTC

### 26.	Step4 – Merge PMOS – NMOS load curves and plot VTC

•	Load curves of PMOS and NMOS along with CMOS inverter circuit

<img width="940" height="339" alt="image" src="https://github.com/user-attachments/assets/341cfd5e-ad6a-47f3-98a8-d7a6618d0b04" />

•	Superimpose load curve of NMOS on the load curve of PMOS

<img width="940" height="581" alt="image" src="https://github.com/user-attachments/assets/45106a5b-9744-4943-a1a3-fd59364340bd" />

# CMOS Switching threshold and dynamic simulations

## Voltage transfer characteristics -- SPICE simulations

### 27. SPICE deck creation for CMOS inverter

-   SPICE Deck -- Connectivity information about the netlist -- has
    input provided to the simulation -- has tap point from where the
    output is taken

-   Upper part PMOS -- Below NMOS -- input, output, connections, etc
    information will be defined in netlist --

-   Define the component values -- capacitor value comes with
    calculation but here it is assumed

-   Identify the nodes - What is node? -- those two points in between
    component present -- name the nodes -

![](/media_day3/media/image1.png)

![](/media_day3/media/image2.png)

-   Anything start 3 starts \*\*\* are comments -- MOSFET sequence --
    Drain, Gate, Substrate and Source

### 28. SPICE simulation for CMOS inverter

-   Model file has all technological parameters, foundry level
    parameters -- it comprises all both PMOS and NMOS -- Both MOS

-   Netlist file -- code file

![](/media_day3/media/image3.png)

-   Model parameters for pmos, nmos used here in the netlist file are
    mentioned in the model library

-   Here, W/L ration for the PMOS and NMOS are kept constant of 1.5 --
    Ideally W/L ratio of PMOS is expected 2 to 2.5 times higher than the
    W/L ratio of the NMOS

![](/media_day3/media/image4.png)

-   Difference -- Graph with same W/L is not centred -- Graph with
    higher W/L for PMOS is centred

### 29. Labs Sky130 SPICE simulation for CMOS

-   Open the SPICE netlist file for the VTC characteristic

![](/media_day3/media/image5.png)

-   This command will open the SPICE netlist file in the terminal
    itself.

![](/media_day3/media/image6.png)

-   Here, pls check the W/L of both NMOS and PMOS -- Input voltage is
    sweep from 0 to 1.8V with step of 0.01

![](/media_day3/media/image7.png)

-   Run the file using the ngspice command

![](/media_day3/media/image8.png)

-   It will open the plot for the given command and find the threshold
    voltage where vin and vout are same

![](/media_day3/media/image9.png)

-   Find the coordinates where vin and vout are same

-   Look for Transient analysis -- open the SPICE netlist file and run
    it using the ngspice command

-   Vin in 0 PULSE(0V 1.8V 0 0.1ns 0.1ns 2ns 4ns) - This defines a
    time-varying voltage applied to node in (gate of inverter)

-   Syntax - PULSE(Vlow Vhigh Tdelay Trise Tfall Ton Tperiod) -- Low
    level = 0 V --- logic 0 --- High level = 1.8 V --- logic 1 --- Delay
    = 0 --- starts immediately --- Rise time = 0.1 ns --- smooth rising
    edge --- Fall time = 0.1 ns --- smooth falling edge --- ON time = 2
    ns --- stays high 2 ns --- Period = 4 ns --- full cycle

-   .tran 1n 10n --- Simulate circuit behavior from 0 to 10 ns ---
    Record/output results every 1 ns

-   .tran Tstep Tstop --- Tstep = 1 ns → time resolution (printing
    interval) --- Tstop = 10 ns → total simulation time

![](/media_day3/media/image10.png)

-   Run the file using ngspice

![](/media_day3/media/image11.png)

-   Plot will be opened

![](/media_day3/media/image12.png)

-   Calculate the rise delay and fall delay -- Consider the half of Vdd
    i.e. 0.9V

-   Consider the output curve rising edge -- calculate the time
    difference between the input and output when output crosses 0.9 V
    (Half of Vdd) -- Click on the graph on input graph and output graph

![](/media_day3/media/image13.png)

-   For fall delay -- consider the falling edge of the output -- apply
    same method as applied for rise delay

## Static behavior evaluation -- CMOS inverter robustness -- Switching
Threshold

### 30. Switching Threshold, Vm

-   Let us analyse the CMOS Inverter with different W/L ratio of both
    PMOS and NMOS

-   Generally, PMOS has bigger size than NMOS

![](/media_day3/media/image14.png)

-   Shape is almost shape in both -- suggest that CMOS is robust design
    -- when input is zeo, output is high and vice versa across all sizes
    of CMOS -- used widely in any logic gates -- Switching threshold,
    Noise Margin -- Parameters that define the robustness of the CMOS
    -- (1) -- Switching threshold -- the point at which the devices
    switches

-   Threshold voltage is the voltage where input and output is same -- a
    line of 45 degree is drawn and intersection point is found to have
    threshold voltage -- at this point both MOS are in saturation --
    there is high chance of leakage current -- current flowing from
    power to ground

![](/media_day3/media/image15.png)

-   Here, condition for threshold voltage is Vgs = Vds where current
    flowing from PMOS and NMOS are exactly same -- direction different
    -- For PMOS current is from VDD to capacitor -- For NMOS current is
    from capacitor to NMOS

-   Derive the Vm value from the give ratio of W/L of both MOS
    transistor -- OR -- Find the W/L of MOS from the set Vm

### 31. Analytical expression of Vm as a function of (W/L)p and (W/L)n

-   Switching threshold condition -- Vin = Vout -- Vgs = Vds -- both MOS
    in saturation = Direction os IdsN and IdsP are opposite and equal

-   Focusing on points where dashed line intersecting the output
    characteristic

![](/media_day3/media/image16.png)

-   Complete dependency of Vm on IdsN and IdsP

-   Focusing on deriving the Vm from the technological parameters -- W/L
    is given to have Vm

-   Id in the saturation region is given using the following equation
    but value of λ is very close to 0 that causes to have the value of
    (1 + λVds) near to 1.

![](/media_day3/media/image17.png)

-   By ignoring the (1 + λVds),

![](/media_day3/media/image18.png)

-   Let us the current for equations for NMOS and PMOS

![](/media_day3/media/image19.png)

-   By solving the using the given equations and conditions, we have Vm.

![](/media_day3/media/image20.png)

-   In the above equation, put the value of technological parameters
    like W, L, µ, Cox, etc. to have R and from R we have Vm.

### 32. Analytical expression of (W/L)p and (W/L)n as a function of Vm

-   Here, we set the Vm first and based on set value of Vm -- Find the
    value of W/L for both NMOS and PMOS to meet the Vm requirement

-   Let us assume that our power supply voltage is 2.5 V and we want to
    threshold exactly at half i.e. 1.25 V. -- Based on the set value,
    what should be the W/L for both NMOS and PMOS?

![](/media_day3/media/image21.png)

![](/media_day3/media/image22.png)

### 33. Static and dynamic simulation of CMOS inverter

-   Here, we are going to change the ration of (W/L) of NMOS and (W/L)
    of PMOS and we see how the threshold value can change by changing
    this parameter

-   Simulation done on TSMC model file (Only for demonstration purpose
    -- for hands-on purpose

-   Along with finding the switching threshold, dynamic simulation
    (delay calculatio) will be done to find rise delay and fall delay

> ![](/media_day3/media/image23.png)

-   Find the threshold voltage, rise time and fall time for the W =
    0.375 µm, L = 0.25 µm -- How to calculate the rise time and fall
    time is explained in Lecture 29.

-   Repeat the task for other combination to find threshold voltage,
    rise time and fall time and come up with conclusion

![](/media_day3/media/image24.png)

### 34. Static and dynamic simulation of CMOS inverter with increased PMOS
width

-   Here, we are going to change the ration of (W/L) of NMOS and (W/L)
    of PMOS and we see how the threshold value can change by changing
    this parameter

-   Here, only Width is changed -- Length is kept constant

-   As value of x is increased in integer form (As per (Wp/Lp) =
    x(Wn/Ln)), threshold curve is shifted towards the right direction -
    PMOS is getting more stronger than NMOS causes -- PMOS has more
    width than NMOS -- More area in PMOS for capacitor to charge very
    fast

> ![](/media_day3/media/image25.png)

-   Conclusion -- as PMOS is getting more stronger, rise delay getting
    reduced and fall delay increased -- threshold voltage getting
    shifted towards the right

-   Here, Vm is the threshold where Vin = Vout of CMOS inverter

### 35. Applications of CMOS inverter in clock network and STA

-   For different set of (W/L) of both NMOS and PMOS, we have different
    set for rise time, fall time and threshold voltage.

-   If size of PMOS is varied between 2 and 3 of NMOS size, variation in
    threshold voltage is from 1.2 V to 1.25 V -- This is hardly
    difference of 50 mv -- This is due to not achieved exact Wp = 2Wn or
    Wp = 3Wn -- It might shift due to fabrication imperfection -- Here,
    variation in threshold voltage due to W is very small which makes
    robust behaviour of CMOS

-   Choose the size of the MOS in such a way that rise delay and fall
    delay must be same. Here, it comes when Wp = 2Wn -- This is the
    important requirement for the cell which is involved in clock
    network

> ![](/media_day3/media/image26.png)

-   Here, as shown in the figure, rise delay is more than fall delay
    which is not good design

# CMOS Noise Margin robustness evaluation

## Static behaviour evaluation -- CMOS inverter robustness -- Noise margin

### 36. Introduction to noise margin

-   Noise margin -- one of the important aspect for robustness of the
    CMOS inverter -- related to cross talk and glitches -- often
    adversely impacting the performance specifically in lower
    technological nodes -- can be reduced or identified before hand
    before identifying the noise margin of any logic gate

-   How does CMOS noise margin vary and how different size of MOSFETs in
    CMOS affect the noise margin?

-   Let us take the case of Inverter where Output is the inverted form
    of input -- 1 is given, 0 is getting at the output

-   Consider the idle inverter -- Vdd/2 threshold -- slope at this point
    -- change in output is visible but input is not changing causes the
    slope infinite -- slope = dy/dx = (Change in Output)/(Change in
    Input)

> ![](/media_day4/media/image1.png)

-   In the second VTC, slope is finite -- any input voltage between 0 to
    VIL causes to have high output voltage i.e. Vdd or VOH (Here, Vdd
    and VOH are same but in practical they are not same)

-   Any input voltage between VIH to Vdd causes to have low output
    voltage i.e. VOL.

-   0 to VIL \--\> Low IP -- VIH to Vdd \--\> High IP --

-   0 to VOL \--\> Low OP -- VIH to Vdd \--\> High OP

### 37. Noise margin voltage parameters

-   Revise -- Let us consider Vdd = 1 V -- Assume -- VIL = 0.25 V -- VIH
    = 0.75V

-   0 V to 0.25 V \--\> Low IP -- 0.75 V to 1 V \--\> High IP -- VOL
    \--\> OP is low or close to 0 V or less than VIL (0.25 V) -- VOH
    \--\> OP is high or close to Vdd or higher than VIH (0.75 V)

-   Here, (1) VOL must be less than VIL (2) VOH must be higher than VIH
    -- as when output of inverter is connected to input of next stage,
    it can be recognised with correct logic levels.

-   Let us consider the real practical situation

-   On the VTC, consider the points when slope becomes -1, consider only
    those points will act as VIL and VIH.

> ![](/media_day4/media/image2.png)

### 38. Noise margin equation and summary

> • Let is plot the graph for noise margin

-   Noise margin: Irrespectively of input and output, when the voltage
    is in the range of (VOH - VIH) will be considered as high -- Same
    way - Irrespectively of input and output, when the voltage is in the
    range of (VIL - VOL) will be considered as low

![](/media_day4/media/image3.png)

-   Due to any reason, if noise generated causes to change the voltage
    level within the range of noise margin will not affect

-   In other words, noise margin is the range for tolerable range within
    which voltage level remain intact.

-   Let us see the noise bumps and how is it affected and when it would
    be ignored

-   Any noise voltage bum that goes in undefined area, its level will
    not be predicted as either it will be considered as Low or High

> ![](/media_day4/media/image4.png)

-   Consider the voltage noise bumps are generated due to glitches --
    Consider the blue line voltage is steady and is 0 V. -- Due to
    glitch (1) noise bumps are in the margin will not adverse the logic.
    It is considered as safe glitch (2) Bump height goes in undefined
    region which affect the logic level and this glitch needs to be
    fix. (3) Glitch height is to high that has alter the logic level
    which also required to fix.

### 39. Noise margin/Rail Error variation with respect to PMOS width

-   Noise margin is about cascading gates, i.e., whether the next
    inverter still interprets the level correctly, and that depends on
    VOL, VOH, VIH and VIL (the slope = −1 points): (NMH = VOH - VIH) and
    (NML = VIL - VOL)

-   Noise margin \--\> How much noise the next gate can tolerate

-   Rail error tells us how strong or weak the output logic level is

-   If rail error is small \--\> Output is very close to ideal rails
    \--\> Strong logic levels

-   If rail error is large \--\> Output does not reach proper HIGH or
    LOW \--\> Weak logic levels

-   Rail Error = Output Swing Loss -- How far the output voltage is from
    its ideal supply rail -- how far the "HIGH" output falls below Vdd
    and how far the "LOW" output rises above 0

-   Upper Rail = Vdd -- Lower Rail = 0 V (Ground)

-   High Rail Error = Vdd -- VOH

-   Low Rail Error = VOL -- 0

-   Rail error is for only output levels - Rail error affect actual
    noise margin of the next stage

-   We have already seen the effect of (Wp/Lp) and (Wn/Ln) on VTC and
    transient response. Here, we are going to see the same on the effect
    of noise margin and Rail Error

-   When we vary the size of PMOS as compared to NMOS, how does rail
    error and noise margin vary which ultimately tells on robustness of
    the CMOS

> ![](/media_day4/media/image5.png)

-   PMOS is the responsible for holding the High logic -- NMOS is the
    responsible for holding the Low logic

-   As width of PMOS is increased compared to NMOS, High rail error is
    in creasing while low error is reduced

-   For a particular switching threshold voltage, i.e. 1.2 V, Wp is
    required to have twice of Wn but due to limitation in fabrication,
    exact Width of Wp will not be obtained, Wp would be either 1.8 times
    or 2.2 times of Wn. Even in this scenario, High Rail error and and
    Low Rail Error will not be significantly obtained.

![](/media_day4/media/image6.png)

-   If any voltage level, that falls between Vdd and VOH, considered as
    High

-   If any voltage level, that falls between VOL and 0 V, considered as
    Low

-   If an inverter that can amplify the input signal, both MOS should be
    in saturation for analog design

> ![](/media_day4/media/image7.png)

### 40. Sky130 Noise margin labs

-   SPICE Simulation

-   Open the day 4 file using the vim editor and apply dc sweep at input
    from 0 to 1.8 with step of 0.01V

![](/media_day4/media/image8.png)

-   Run this file using the ngspice command and give appropriate command
    to see visualise VTC

![](/media_day4/media/image9.png)

-   From the graph find the NMH = VOH -- VIH = 1.68 -- 0.98 = 0.70, NML
    = VIL -- VOL = 0.78 -- 0.10 = 0.68, High Rail Error = 1.8 -- 1.68 =
    0.12 V, Low Rail Error = VOL -- 0 = 0.10 V

# CMOS power supply and device variation robustness evaluation

## Static behaviour evaluation -- CMOS inverter robustness -- Power supply variation

### 41. Smart SPICE simulation for power supply variations

-   While considering the CMOS robustness, power supply scaling is very
    important -- When technological node is scaled down from 250 nm to
    10 nm to 35 nm, power supply scaling is very essential -- Lower
    technological node, power supply value should be reduced -- CMOS is
    expected to behave as it was behaving before (Compared with lower
    technological node with bigger technological node)

-   We will perform one experiment using the SPICE simulation and aim is
    to that CMOS behaviour should not change

![](/media_day5/media/image1.png)

-   Here, width of PMOS is kept higher than NMOS and supply voltage is
    reduced and its VTC, rise delay, fall delay can be found -- In this
    experiment, Wn and Wp is kept constant and only supply voltage
    changes

-   Smart Simulation required to be done as to have all the VTC have to
    be on same graph -- Netlist will remain same but scripting will
    change

![](/media_day5/media/image2.png)

-   In the script file, loop will be iterated and for each iteration,
    power supply value is subtracted by 0.5 V -- Starting with 2.5, will
    go in each iteration to 2.0 V, 1.5 V, 1.0 V, and 0.5 V

![](/media_day5/media/image3.png)

-   Here, 5 DC plots will be on the new pop-up window -- Anything
    between .control and .endc allows to do scripting -- In case of
    doing more complex simulation, scripting file required to write as
    per functionality

-   Run the file using the ngspice command and give appropriate command

> ![](/media_day5/media/image4.png)

-   It is clearly seen that, there are five VTC for five different power
    supply starting from 2.5 V to 0.5 V.

### 42. Advantages and disadvantages using low supply voltage

-   After getting the 5 VTC for five different supply voltages, first
    observation is that, even for supply voltage of 0.5 V, behaviour of
    CMOS is not changed

-   Find the first parameter -- how much gain is obtained when supply
    voltage is 2.5 V compared to the supply voltage 0.5 V

-   Gain -- Ratio of change in Output voltage to change in input voltage

-   How to have the gain value? -- On the VTC, consider the points where
    slope is -1 -- find the coordinates of those points and find dy/dx
    (Gain)

> ![](/media_day5/media/image5.png)

-   Here, there is an advantage of using the 0.5 V as supply voltage but
    there is also one major disadvantage.

-   Another advantage -- Energy -- How much energy CMOS inverter will
    consume -- (½)CV^2^ -- here, output load capacitance (capacitor
    through which inverter can charge or discharge) is fix and V is
    getting change based on the supply voltage

![](/media_day5/media/image6.png)

-   Significant benefit in reduction of energy \~90% for supply voltage
    0.5 V -- again this low voltage supply has disadvantage that causes
    not used

-   For supply voltage of 0.5 V, Charging the output load capacitance,
    0.5 V supply is not enough -- Device even can't charge and discharge
    complete load capacitor due to not enough rise time to charge the
    device upto 0.5 V -- Here, device is not as fast as expected --
    Here, input clock frequency required to decreased that causes to
    increase the time period which eventually give time to full charge
    output load capacitor and discharge full load capacitor

-   In case of supply voltage 2.5 V, device has enough time for given
    input frequency to fully charge and discharge

-   In compared to supply voltage 2.5 V, supply voltage 1.0 V takes time
    to get the output capacitor to get loaded -- i.e. rise delay and
    fall delay is higher in case of supply voltage 1.0 V

> ![](/media_day5/media/image7.png)

### 43. Sky130 Supply Variations Labs

-   Open the SPICE file for day 5 and make any changes in scripting
    section if find necessary

![](/media_day5/media/image8.png)

-   Here, 4 iteration will be applied with each iteration is reduced
    with supply voltage of 0.3 V -- Based on the number of iterations,
    in the following image change is required.

![](/media_day5/media/image9.png)

-   Here, VTC for all different supply will automatically pop-up and
    find the gain, For switching threshold voltage -- Need to click on
    the VTC points and coordinates will automatically appear on the
    ngspice simulator on the terminal window.

> ![](/media_day5/media/image10.png)

-   Coordinates of the VTS for supply voltage 1.8 V is below to find
    Gain

![](/media_day5/media/image11.png)

## Static behaviour evaluation -- CMOS inverter robustness -- Device variation

### 44. Sources of variation -- Etching process

-   Here, we are trying to find the source of variation that causes the
    device behaviour to change

-   Need to find the exact parameters that vary the width and length of
    CMOS inverter

-   First source of variation -- Etching process -- it is fabrication
    step -- that define the length and width of the device along with
    entire structure -- that directly affect the delay

![](/media_day5/media/image12.png)

-   Here, the shape of each metal layer is obtained using the etching
    process as shown in the layout design of CMOS -- Blue colour metal
    layer: Metal lines for Supply, Ground, Input and Output -- Red
    colour metal layer -- poly silicon area form gates of CMOS has some
    width and height -- Green colour metal layer: P diffusion region
    with some height and width -- Yellow colour metal layer: N diffusion
    area with some height and width -- all metal layer are obtained
    using the etching process

-   Let us consider the inverter chain -- end points would have
    different circuit

![](/media_day5/media/image13.png)

-   Such variation happen a lot in chain of inverter which fabricated on
    a chip -- This variation is not only on small area but chip is
    fabricated on larger area and each device would have different
    variation in terms of W and L -- such distortion is not repetitive

![](/media_day5/media/image14.png)

-   Here, inverter connected to end points have different structures --
    they are connected to flip flops -- Due to this, structural
    variation at the end point devices/inverters would have different
    than the structural variation in the devices/inverter which are in
    the middle

-   These structural variations (in the fabrication) impact the device
    and inverter properties -- Below is equation which tell us how such
    variation impact drain current

![](/media_day5/media/image15.png)

-   Drain current has dependency on W and L of the device -- Question to
    answer is how drain current causes the delay in inverter when
    variation in W and L is present

### 45. Sources of variation -- oxide thickness

-   Along with variation in W and L of device, oxide thickness also
    impact the behaviour of the device -- Oxide thickness is directly
    connected to the capacitance present in drain current

-   If thickness is not uniform -- changes in thickness -- variation in
    capacitance -- variation in drain current -- variation in device
    behaviour

![](/media_day5/media/image16.png)

-   Let us see the how real oxidation process differ than expected

![](/media_day5/media/image17.png)

-   Consider the effect of this variation when large number of
    device/inverters are to be fabricated -- their cumulative effect may
    change the behaviour of entire circuit -- Again, consider the end
    point inverters are connected to other types of circuits due to
    which their actual oxide thickness profile might be different than
    those are in the middle part

![](/media_day5/media/image18.png)

-   Below is the simplification which shows the in mathematical way the
    dependence of oxide thickness on current and device behaviour -- tox
    is the oxide thickness -

![](/media_day5/media/image19.png)

### 46. Smart SPICE simulation for device variations

-   We will perform SPICE simulation

-   Open the spice simulation file for device variation

-   See the PMOS is strong and NMOS is weak based on the width of both
    MOS and apply DC sweep for changing the input from 0 to 1.8 V with
    step of 0.01 V

> ![](/media_day5/media/image20.png)

-   Run this using ngspice and give command to have the graph

> ![](/media_day5/media/image21.png)

-   

-   Strong PMOS -- least resistance by PMOS -- due to wider width of
    PMOS -- low resistive path for output capacitor to charge -- Charge
    the output capacitor fast

-   Weak NMOS -- Highest resistance by NMOS

-   Wide width -- Strong MOS

-   Narrow width -- Weak MOS

-   Assume: 1.875 µm is maximum width can be fabricated -- 0.375 µm is
    the smallest width can be fabricated

![](/media_day5/media/image22.png)

-   Here, we simulate VTC by changing the width of both MOS of the
    inverter -- we will take dimension to extreme to verify the
    behaviour functionality

-   In the script section of the file, total 5 iterations will be
    applied with each loop will change the width of both MOS by 0.375µm

-   Written between '.control' and '.endc' is considered as script file
    -- Pls ensure to have five dc simulation for five VTC

![](/media_day5/media/image23.png)

-   Here, dc1 is for strong PMOS and weak NMOS whereas dc5 is for weak
    PMOS and strong NMOS

![](/media_day5/media/image24.png)

### 47. Conclusion

-   So far we have seen the robust behaviour of CMOS against switching
    threshold, noise margin, power supply variation and device variation
    (oxide thickness and etching cause the variation in W and L)

-   CMOS is insensitive to above variation

-   Here, we continue the discussion from stronger PMOS with weak NMOS
    to weaker PMOS to stronger NMOS

-   Two main parameters to be quantified -- Noise margin and switching
    threshold

-   Here switching threshold variation is \~0.65 V based on threshold
    difference of dc1 and dc5

![](/media_day5/media/image25.png)

-   If you design the inverter for the dc2 and due to device variation,
    it slightly deviated towards dc3 or dc1, there is no drastic change
    in threshold -- very minimal shift in threshold and behaviour of
    CMOS remain intact

-   Another is Low rail error and High rail which are very important
    Here, we are going to change the (W/L) of NMOS and (W/L) of PMOS and
    we see how much the Rail errors vary

-   These rail errors play significant role in improving the noise
    margin for the next stage input

-   Again, the shift is very minimal again showing the robust
    performance against device variations

-   To sum up, due to device variation or supply variation, behaviour
    and operation of CMOS remain intact -- due to this, it can be used
    to build any kind of logic gate

### 48. Sky130 Device Variation Labs

-   Let us go for SPICE simulation

-   Open day 5 device variation file

-   Check the PMOS is strong and NMOS is weak based on width of both MOS

![](/media_day5/media/image26.png)

-   Run this file using ngspice and give the command to have pop-up
    window for VTC graph

![](/media_day5/media/image27.png)

-   From the graph, it is clearly visible that, high holding time is
    more for PMOS as compared to NMOS which implies PMOS is stronger
    than NMOS -- due to that switching threshold has shifted towards the
    right

-   For finding the switching threshold, draw a line of 45 degree and
    find the intersection point

































