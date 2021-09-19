Phase Locked Loop IC Design on Open Source Google Skywater 130nm
-----------------------------------------------------------------------------------------
The workshop on Phase Locked Loop IC Design conducted on 18-19 September 2021


Content
---


DAY 1:
------

 Introduction to PLL
.
  -----------------------------------------------------------------------------------------
  
                                                             Introduction to PLL
Phase locked loop(PLL) is essentially a low noise clock generator locked to the phase of an input reference clock
                                ![image](https://user-images.githubusercontent.com/90973886/133926464-7ffad224-cc8e-4565-9c7b-05a3b2745580.png)
  
  
                                             Figure: Basic configuration of PLL
                                                             
Components of PLL                                                                                                                                                              
1. Phase Frequency Detector
2. Charge Pump
3. Loop Filter
4. Voltage Controlled Oscillator
5. Frequency Divider

Phase Frequency Detector(PFD): measures the phase difference between input reference and feedback signal.


Charge Pump(CP) : converts the digital measure of phase/frequency difference into analog control signal to control the oscillator. 


Loop filter(LF) : filters the CP output and generates the VCO control voltage, also plays major role in the stablity of feedback loop.


Voltage Controlled Oscillator(VCO): generates the output signal with frequency controlled by control voltage.


Frequency Divider(FD) : serves as frequency multiplier


Phase Frequency Detector:

![image](https://user-images.githubusercontent.com/90973886/133927753-d9b14258-ec38-4d50-a0e2-48aa3d8de3d3.png)
                                
                                
                                            
                                               

UP and DOWN carry the phase or frequency error information in the width of the pulse.

Limitation of PFD is dead zone. Dead zone is the zone where PFD is insensitive to the phase difference. The output does not get enough time to rise when two signals fall close to each other.


Charge Pump:

![image](https://user-images.githubusercontent.com/90973886/133928288-75011aa2-5c9c-491f-a98c-a5d888fb0e2c.png)
                             
                             
 
 
 If the UP signal is active, current flows from VDD to output capacitor and charges the capacitor. As a result the voltage at the output of CP increases.
 
 If the DOWN signal is active, current flows from output capacitor to ground and discharges the capacitor. As a result the voltage at the output of CP decreases.
 
 Voltage Controlled Oscillator:
 
 ![image](https://user-images.githubusercontent.com/90973886/133933691-4f6b2942-733b-4ea1-bb77-4c939f7332d4.png)

The above figure shows a ring oscillator which has odd number of inverter in series.
The frequency depends on delay & delay depends on current supplied.

Important terms used in PLL

Lock-in range

Range of freuencies which PLL can stay in lock in steady state. It mainly depends on the range of frequencies VCO can produce and is limited by the dead zone of PFD.

Capture range

Range of frequencies which PLL can lock when started from unlocked condition. Capture range is smaller than the lock-in range. It depends on the loop filter bandwidth.

Settling time

The time taken by the PLL to lock from an unlocked state is called the settling time. It depends on how quickly charge pump rises to the stable value.

PLL Specification
----
Corner TT

Supply Voltage 1.8V

Room Temperature

Input Fmin = 5MHz ;  Fmax = 12.5MHz

Multiplier  8x

Jitter(rms) <~ 20ns

Duty cycle = 50%
                                             
Tool setup and design flow:
------------------------------------------------------------------------------------------------------------------------------------------------------------
Two tools are used:

Ngspice: it is an open source tool used for design simulations,used for the transistor level circuit simulations.
Magic: it is an open source tool,used for the layout design.

Development flow steps:
Circuit development
Pre layout simulation
Layout development
Parasitics extraction
Post layout simulation


DAY 2
------------------------------------------------------------------------------------------------------------------------------------------------------------
PLL Component design:
--------------------------

Frequency divider circuit is shown below:

![image](https://user-images.githubusercontent.com/90973886/133929265-3b7a0eda-fe70-402f-a5f1-4b6c7bd6800e.png)


                  
Phase Frequency Detector circuit is shown below:

![image](https://user-images.githubusercontent.com/90973886/133929688-b4d283b6-7041-4388-baa9-282f582aa4a2.png)


Charge Pump circuit is shown below:

![image](https://user-images.githubusercontent.com/90973886/133929715-bdd71c07-1773-4af1-9697-9a63cac0865b.png)


Voltage Control Oscillator circuit is shown below:

![image](https://user-images.githubusercontent.com/90973886/133930119-1aa31748-db65-4e82-9ae2-5097fc1334d4.png)


PLL Components circuit simulation :
----------------------------------------
FD.cir file is shown below

![image](https://user-images.githubusercontent.com/90973886/133931319-1b0fd462-4a68-4b03-bb72-b40c63360f94.png)

FD simulation & output is shown below:

![image](https://user-images.githubusercontent.com/90973886/133931347-fad2739e-ac47-41e7-a1d6-e3d6c7ca7074.png)

![image](https://user-images.githubusercontent.com/90973886/133931362-76cde2d2-d546-4238-85ce-53893829ec52.png)


CP.cir file is shown below:

![image](https://user-images.githubusercontent.com/90973886/133931443-9601afec-5476-43a8-bbbf-ffca10d10211.png)

CP simualtion & output is shown below:

![image](https://user-images.githubusercontent.com/90973886/133931470-33fff413-a22d-42ab-9b45-00b48d43a5e9.png)

![image](https://user-images.githubusercontent.com/90973886/133931484-d7e82fc3-fa5b-4f3c-bfeb-165ea5aa784b.png)


PD.cir file is shown below:

![image](https://user-images.githubusercontent.com/90973886/133931561-21c6fcad-22ab-4d31-8d34-76cc42345353.png)

PD simulation & output is shown below:

![image](https://user-images.githubusercontent.com/90973886/133931576-d61d00e6-3d09-4462-93c6-4a00dd505695.png)

![image](https://user-images.githubusercontent.com/90973886/133931590-0d8c2661-68de-4aa6-b082-67ccc11453ef.png)


VCO simulation & output is shown below:

![image](https://user-images.githubusercontent.com/90973886/133931647-60b7cf92-60d8-4cd9-a2c3-ef008ad0f578.png)

![image](https://user-images.githubusercontent.com/90973886/133931658-802a1ccb-f622-4975-940f-a0d1fbe11f94.png)


Steps to combine PLL sub-circuits and PLL full design simulation
---------------------------------
Combining all the circuits to form PLL
PLL simulaton & output is shown below:

![image](https://user-images.githubusercontent.com/90973886/133931802-a543551e-cb3c-4322-bcd6-326c3ec2be86.png)

![image](https://user-images.githubusercontent.com/90973886/133931804-0d2463a0-c467-45db-90b9-ad0d57cf585c.png)

Here red signal is the reference signal,blue is Output Clock Divided by 8

Troubleshooting Steps
------
If output doesn't  mimic the ref signal, we should always try to debug individual circuits beore simulating the whole circuit. If signals are coming flat up or the simulation is crashing then check whether the connectivity is done properly or any issues like wrong net names or parameter value issues.

Magic Layout
-------
layout for FD is shown below:

![image](https://user-images.githubusercontent.com/90973886/133932065-2f035c37-ba41-4254-bd6d-c968987a75df.png)

layout for PFD is shown below:

![image](https://user-images.githubusercontent.com/90973886/133932074-3ffb7e66-9219-4c58-9414-549357c8d691.png)

layout for CP is shown below:

![image](https://user-images.githubusercontent.com/90973886/133932085-edf1cb7f-eebc-4d67-901a-3d140d22f16b.png)

layout for VCO is shown below:

![image](https://user-images.githubusercontent.com/90973886/133932152-49526095-faf8-42de-9103-2b94d921464a.png)

layout for PLL is shown below:

![image](https://user-images.githubusercontent.com/90973886/133932325-41c54639-8977-450a-9745-beec2b906712.png)

Parasitics Extraction
---
To extract the capacitance effect information parasitics extraction, press i button to select the whole design and then give "extract all" command.
For postlayout simulation the extraction file has to be converted to spice file using ext2spice command.

![image](https://user-images.githubusercontent.com/90973886/133932484-02fcfec9-54db-4041-9583-16c50b587533.png)


Post Layout simulation
-----
PFD simulation result:

![image](https://user-images.githubusercontent.com/90973886/133937475-0d678074-1113-4073-9fd3-9da4aa2089f4.png)

![image](https://user-images.githubusercontent.com/90973886/133937482-9ddbab65-a34d-48d7-a683-d9a0ac2a8cc5.png)



Tapeout
---
Tapeout means to sned our final design to the fab. Is the final result of the design process for integrated circuits or printed circuit boards before they are sent for manufacturing.

Acknowledgement
---
Kunal Ghosh (Co-founder) (VSD Corp Pvt Ltd)

Lakshmi Sathi (Instructor)

https://github.com/lakshmi-sathi/avsdpll_1v8


                                               






