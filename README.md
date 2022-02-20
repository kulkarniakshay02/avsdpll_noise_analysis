# PLL-workshop

PLL- Need: To generate clk signal with spectral purity which is otherwise difficult to achieve with only VCO(Voltage Controlled Oscillator) or only Quartz crystal.

<img src="https://user-images.githubusercontent.com/94942531/154814007-fdf1c555-38b8-4db6-aa16-fcf1ecf8f0e0.jpg" width="800" height="400" />

Parts of PLL block diagram:
- Phase frequency detector: Does the comparison of reference with output signal
  - It has 2 output signals, up signal to increase the frequency and down signal to decrease the frequency of the output signal of PLL

- Charge pump: Converts output of PFD signal to analog signal
  - It gives analog equivalent of up and down signal by either increasing or decreasing the voltage magnitude 
  - <img src="https://user-images.githubusercontent.com/94942531/154814058-aa8071a9-cf8d-4714-97cd-b613777beaa5.jpg" width="600" height="400" />

- Low pass filter: Multiple aspects, primarily to smoothen the output signal and also to stabilize the circuit.
  - <img src="https://user-images.githubusercontent.com/94942531/154818198-ee265ae5-fc26-4a90-a59b-ade60e951c69.jpg" width="600" height="400" />

- Voltage controlled oscillator: Generation of clk signal as per the analog signal from charge pump.
  - <img src="https://user-images.githubusercontent.com/94942531/154814094-89523427-7746-4571-8acf-90304cc382e8.jpg" width="600" height="400" />
- Frequency divider: Coefficient value of this divider decides the clock multiplier value of PLL. If divider is dividing the output clock by 8 then, PLL can multiply the input signal by 8.
  - <img src="https://user-images.githubusercontent.com/94942531/154817567-229b4bc0-6047-4af5-a11f-1c3337e8aa94.jpg" width="600" height="400" />



Specifications:
- Supply voltage: 1.8V
- Temperature: room temperature
- Process corner: TT
- Reference clock signal: Fmin = 5MHz and Fmax = 12.5 MHz
- Duty cycle: 50%
- Multiplier: 8x  

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

Voltage Controlled Circuit:

<img src="https://user-images.githubusercontent.com/94942531/154801702-6b859d78-ff80-4c65-9700-2ec001850dc3.png" width="500" height="400" />

Phase Frequency Detector circuit:

<img src="https://user-images.githubusercontent.com/94942531/154801868-74986f19-c842-4866-ba7b-933af5e733ae.png" width="500" height="400" />

Final simulation of PLL circuit:

<img width="718" alt="image" src="https://user-images.githubusercontent.com/94942531/154839542-6742a44b-089e-4da3-ab21-c9b1762cc3d3.png">

And the zoomed-in version:

<img src="https://user-images.githubusercontent.com/94942531/154839329-ea5e297d-bf87-4047-9ab3-ee96386992c1.png" width="600" height="400" />
