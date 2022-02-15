# PLL-workshop

PLL- Need: To generate clk signal with spectral purity which is otherwise difficult to achieve with VCO(Voltage Controlled Oscillator) and Quartz crystal.

img of PLL can be added here

Part of PLL block diagram:
- Phase frequency detector: Does the comparison of input with output signal
- Charge pump: Converts output of PFD signal to analog signal
- Low pass filter: Multiple aspects, discussed later 
- Voltage controlled oscillator: Generation of clk signal
- Frequency divider: coefficient value of this divider decides the clock multiplier value of PLL. If divider is dividing the output clock by 8 then, PLL can multiply the input signal by 8.



