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

Graph of output voltage due to current leakage (and when no input is applied): 
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

And the zoomed-in version at the end of the waveform where the charge pump output is stable:

<img src="https://user-images.githubusercontent.com/94942531/154839329-ea5e297d-bf87-4047-9ab3-ee96386992c1.png" width="600" height="400" />

In the above image, it can be seen that we are getting the periodic output of up and down signals even when the charge pump output is stable. So, it looks like the PLL is not correctly locked. The reason behind this is unknown. Here, few approaches to allow PLL to be locked are explored.

Two possible approaches were assumed:
- VCO output frequency is not stable
- Input to VCO (Charge pump/loop filter output is fluctuating)
 
The first option is explored to good extent and is described below. 

 - Firtly, tried to use ac analysis to plot the frequency domain plot of the output clk signal of VCO but, it was not possible to get the frequency domain plot using ac analysis without an ac source in the design. Then, another approach was to use FFT (Fast Fourier Transform) to get the frequency domain plot and, was getting this output (this graph is the simulation output of VCO only and it's around 28MHz):

<img src="https://user-images.githubusercontent.com/94942531/159157417-79dc3fe3-cdce-4a51-89f7-66d1539693a9.png" />

The above graph is achieved with following statements in control block:

<img src="https://user-images.githubusercontent.com/94942531/159158423-8d077192-e289-49e2-a854-bfdb38323d0b.png" />

There are still unanswered questions like why do we have a bump at the start of the graph at 0MHz where there should be no DC at the output.

So, finally got the clock output with the transcient analysis with the complete prelayput simulation of the PLL circuit at different clock samples.

At 800th VCO output clk signal sample:
<img src="https://user-images.githubusercontent.com/94942531/159157785-0f4a8b84-1305-4f9f-8e33-0bd890ee5e51.png" />

At 3000th VCO output clk sample:
<img src="https://user-images.githubusercontent.com/94942531/159157937-739d4c96-0a1d-46af-b04b-7b8cef4cb9db.png" />

At 6000th VCO output clk sample:
<img src="https://user-images.githubusercontent.com/94942531/159157962-6a15f445-af85-4110-aa54-81b48bc51cc2.png" />

At 10000th VCO output clk sample:
<img src="https://user-images.githubusercontent.com/94942531/159157969-2ec490ae-2309-4e4c-bdb1-e625d444e3a6.png" />

At 12000th VCO output clk sample:
<img src="https://user-images.githubusercontent.com/94942531/159157981-934f0eb0-f76f-4769-a1e4-aaf67d5715c4.png" />

At 13500th VCO output clk sample (Fref is the frequency of the reference clock signal):
<img src="https://user-images.githubusercontent.com/94942531/159157849-2b8dfdcb-7774-45a7-8f05-f9fb55547a75.png" />

The above measurements are taken with the help of .meas statment in ngspice used in following manner (there is a need of transcient analysis with control block for this to work):
<img src="https://user-images.githubusercontent.com/94942531/159158585-1f180e31-702a-4291-a63d-592423362e20.png" />

So, the analysis of VCO with different control voltages for above mentioned frequency output:

| Sr | Vcontrol input voltage (in volts) | Output clock frequency (in MHz) |
| ---| --------------------------------  | ------------------------------- |
| 1 | 0.65 | 63.72 |
| 2 | 0.67 | 87.48 |
| 3 | 0.68 | 101.91 |
| 4 | 0.6782 | 99.18 |
| 5 | 0.679 | 100.39 (The frequency that we want) |
| 6 | 0.6925 | 122.67 |
| 7 | 0.6935 | 124.5 |
| 8 | 0.6938 | 124.99 (The frequency that we are getting) |
| 9 | 0.694 | 125.5 |

The voltage difference between required input control voltage and actual control voltage 
Vdiff = 0.6938 – 0.679 = 14.8 mV 

Basically, we are getting 14.8 mV of extra voltage at the output of charge pump which is causing VCO to give output which is 125MHz. 
This could be related to the process node differences (The PLL specifications were originally planned for 180nm technology node but, the used technology node is 130nm)

Noise analysis:



