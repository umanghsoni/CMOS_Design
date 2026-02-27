**NgspiceSky130**

**[Day 3]**

**CMOS Switching threshold and dynamic simulations**

Voltage transfer characteristics -- SPICE simulations

27. SPICE deck creation for CMOS inverter

-   SPICE Deck -- Connectivity information about the netlist -- has
    input provided to the simulation -- has tap point from where the
    output is taken

-   Upper part PMOS -- Below NMOS -- input, output, connections, etc
    information will be defined in netlist --

-   Define the component values -- capacitor value comes with
    calculation but here it is assumed

-   Identify the nodes - What is node? -- those two points in between
    component present -- name the nodes -

![](/mnt/data/media_day3/media/image1.png)

![](/mnt/data/media_day3/media/image2.png)

-   Anything start 3 starts \*\*\* are comments -- MOSFET sequence --
    Drain, Gate, Substrate and Source

28\. SPICE simulation for CMOS inverter

-   Model file has all technological parameters, foundry level
    parameters -- it comprises all both PMOS and NMOS -- Both MOS

-   Netlist file -- code file

![](/mnt/data/media_day3/media/image3.png)

-   Model parameters for pmos, nmos used here in the netlist file are
    mentioned in the model library

-   Here, W/L ration for the PMOS and NMOS are kept constant of 1.5 --
    Ideally W/L ratio of PMOS is expected 2 to 2.5 times higher than the
    W/L ratio of the NMOS

![](/mnt/data/media_day3/media/image4.png)

-   Difference -- Graph with same W/L is not centred -- Graph with
    higher W/L for PMOS is centred

29. Labs Sky130 SPICE simulation for CMOS

-   Open the SPICE netlist file for the VTC characteristic

![](/mnt/data/media_day3/media/image5.png)

-   This command will open the SPICE netlist file in the terminal
    itself.

![](/mnt/data/media_day3/media/image6.png)

-   Here, pls check the W/L of both NMOS and PMOS -- Input voltage is
    sweep from 0 to 1.8V with step of 0.01

![](/mnt/data/media_day3/media/image7.png)

-   Run the file using the ngspice command

![](/mnt/data/media_day3/media/image8.png)

-   It will open the plot for the given command and find the threshold
    voltage where vin and vout are same

![](/mnt/data/media_day3/media/image9.png)

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

![](/mnt/data/media_day3/media/image10.png)

-   Run the file using ngspice

![](/mnt/data/media_day3/media/image11.png)

-   Plot will be opened

![](/mnt/data/media_day3/media/image12.png)

-   Calculate the rise delay and fall delay -- Consider the half of Vdd
    i.e. 0.9V

-   Consider the output curve rising edge -- calculate the time
    difference between the input and output when output crosses 0.9 V
    (Half of Vdd) -- Click on the graph on input graph and output graph

![](/mnt/data/media_day3/media/image13.png)

-   For fall delay -- consider the falling edge of the output -- apply
    same method as applied for rise delay

Static behavior evaluation -- CMOS inverter robustness -- Switching
Threshold

30. Switching Threshold, Vm

-   Let us analyse the CMOS Inverter with different W/L ratio of both
    PMOS and NMOS

-   Generally, PMOS has bigger size than NMOS

![](/mnt/data/media_day3/media/image14.png)

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

![](/mnt/data/media_day3/media/image15.png)

-   Here, condition for threshold voltage is Vgs = Vds where current
    flowing from PMOS and NMOS are exactly same -- direction different
    -- For PMOS current is from VDD to capacitor -- For NMOS current is
    from capacitor to NMOS

-   Derive the Vm value from the give ratio of W/L of both MOS
    transistor -- OR -- Find the W/L of MOS from the set Vm

31. Analytical expression of Vm as a function of (W/L)p and (W/L)n

-   Switching threshold condition -- Vin = Vout -- Vgs = Vds -- both MOS
    in saturation = Direction os IdsN and IdsP are opposite and equal

-   Focusing on points where dashed line intersecting the output
    characteristic

![](/mnt/data/media_day3/media/image16.png)

-   Complete dependency of Vm on IdsN and IdsP

-   Focusing on deriving the Vm from the technological parameters -- W/L
    is given to have Vm

-   Id in the saturation region is given using the following equation
    but value of λ is very close to 0 that causes to have the value of
    (1 + λVds) near to 1.

![](/mnt/data/media_day3/media/image17.png)

-   By ignoring the (1 + λVds),

![](/mnt/data/media_day3/media/image18.png)

-   Let us the current for equations for NMOS and PMOS

![](/mnt/data/media_day3/media/image19.png)

-   By solving the using the given equations and conditions, we have Vm.

![](/mnt/data/media_day3/media/image20.png)

-   In the above equation, put the value of technological parameters
    like W, L, µ, Cox, etc. to have R and from R we have Vm.

32. Analytical expression of (W/L)p and (W/L)n as a function of Vm

-   Here, we set the Vm first and based on set value of Vm -- Find the
    value of W/L for both NMOS and PMOS to meet the Vm requirement

-   Let us assume that our power supply voltage is 2.5 V and we want to
    threshold exactly at half i.e. 1.25 V. -- Based on the set value,
    what should be the W/L for both NMOS and PMOS?

![](/mnt/data/media_day3/media/image21.png)

![](/mnt/data/media_day3/media/image22.png)

33. Static and dynamic simulation of CMOS inverter

-   Here, we are going to change the ration of (W/L) of NMOS and (W/L)
    of PMOS and we see how the threshold value can change by changing
    this parameter

-   Simulation done on TSMC model file (Only for demonstration purpose
    -- for hands-on purpose

-   Along with finding the switching threshold, dynamic simulation
    (delay calculatio) will be done to find rise delay and fall delay

> ![](/mnt/data/media_day3/media/image23.png)

-   Find the threshold voltage, rise time and fall time for the W =
    0.375 µm, L = 0.25 µm -- How to calculate the rise time and fall
    time is explained in Lecture 29.

-   Repeat the task for other combination to find threshold voltage,
    rise time and fall time and come up with conclusion

![](/mnt/data/media_day3/media/image24.png)

34\. Static and dynamic simulation of CMOS inverter with increased PMOS
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

> ![](/mnt/data/media_day3/media/image25.png)

-   Conclusion -- as PMOS is getting more stronger, rise delay getting
    reduced and fall delay increased -- threshold voltage getting
    shifted towards the right

-   Here, Vm is the threshold where Vin = Vout of CMOS inverter

35\. Applications of CMOS inverter in clock network and STA

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

> ![](/mnt/data/media_day3/media/image26.png)

-   Here, as shown in the figure, rise delay is more than fall delay
    which is not good design
