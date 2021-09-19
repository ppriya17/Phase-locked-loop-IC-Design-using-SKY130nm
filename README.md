Phase Locked Loop IC Design on Open Source Google Skywater 130nm
-----------------------------------------------------------------------------------------
The workshop on Phase Locked Loop IC Design conducted on 18-19 September 2021


Content
DAY 1:
 Introduction to PLL
.
  -----------------------------------------------------------------------------------------
  
                                                             Introduction to PLL
Phase locked loop(PLL) is essentially a low noise clock generator locked to the phase of an input reference clock
                                ![image](https://user-images.githubusercontent.com/90973886/133926464-7ffad224-cc8e-4565-9c7b-05a3b2745580.png)
  
  
                                             Figure1: Basic configuration of PLL
                                                             
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
                                
                                
                                               Figure2: PFD
                                               

UP and DOWN carry the phase or frequency error information in the width of the pulse.

Limitation of PFD is dead zone. Dead zone is the zone where PFD is insensitive to the phase difference. The output does not get enough time to rise when two signals fall close to each other.


Charge Pump:

                             ![image](https://user-images.githubusercontent.com/90973886/133928288-75011aa2-5c9c-491f-a98c-a5d888fb0e2c.png)
                             
                             
                                             Figure3 : CP
                                             
                                             
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

Frequency divider circuit is shown below:

                  ![image](https://user-images.githubusercontent.com/90973886/133929265-3b7a0eda-fe70-402f-a5f1-4b6c7bd6800e.png)


                  
Phase Frequency Detector circuit is shown below:

                  ![image](https://user-images.githubusercontent.com/90973886/133929688-b4d283b6-7041-4388-baa9-282f582aa4a2.png)


Charge Pump circuit is shown below:

                  ![image](https://user-images.githubusercontent.com/90973886/133929715-bdd71c07-1773-4af1-9697-9a63cac0865b.png)


Voltage Control Oscillator circuit is shown below:

                 ![image](https://user-images.githubusercontent.com/90973886/133929794-7ba4355a-74c4-45c3-a03c-2d1b6321e662.png)





   


                                               






