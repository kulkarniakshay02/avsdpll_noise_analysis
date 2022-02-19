# PLL-workshop

PLL- Need: To generate clk signal with spectral purity which is otherwise difficult to achieve with VCO(Voltage Controlled Oscillator) and Quartz crystal.

img of PLL can be added here

Part of PLL block diagram:
- Phase frequency detector: Does the comparison of reference with output signal
- Charge pump: Converts output of PFD signal to analog signal
- Low pass filter: Multiple aspects, discussed later 
- Voltage controlled oscillator: Generation of clk signal
- Frequency divider: coefficient value of this divider decides the clock multiplier value of PLL. If divider is dividing the output clock by 8 then, PLL can multiply the input signal by 8.

Specifications:

Pre-layout simulations:

Frequency divider circuit:
Blue signal= input clock 
Red signal = Output of clk divider

<img src="https://user-images.githubusercontent.com/94942531/154800201-39ac9d1c-674b-480b-8fe4-ca1422107b50.png" width="500" height="400" /> 

Charge pump circuit:

Graph of output voltage due to current leakage (and when no imput is applied): 
<img src="https://user-images.githubusercontent.com/94942531/154800347-276a79de-492e-434a-85cf-8d11be850bc3.png" width="500" height="400" />

Graph of output voltage for up signal:

<img src="https://user-images.githubusercontent.com/94942531/154800742-3dfea931-3704-4a70-9175-0b3ea388631a.png" width="500" height="400" />

Graph of output voltage for down signal:

<img src="https://user-images.githubusercontent.com/94942531/154800888-ef5f40d7-86a3-4ae1-8514-82204d278f90.png" width="500" height="400" />

