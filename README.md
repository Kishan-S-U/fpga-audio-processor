# FPGA Audio Processor
<img src="res/audio filter system.jpg" align="center"/>
An audio input always contains noise, it is very important to remove certain degree of that noise to make the audio more realistic. There are many methods to accomplish this, this project uses an FIR filter to remove noise and is built on FPGA development board.

Prototype Features:
-
- FIR filter has a cut-off frequency of 4.5 kHz (approximately).
- Internal system runs in sync with the onboard CODEC chip.
- CODEC has a sampling frequency of 44.1 kHz. (input signal beyond 22.05kHz will be attenuated)
- This system is designed to work continuously (without any validation signals), hence no delay in output.

Prototype Description:
-
- FPGA: DE1-SoC FPGA development board.
- FPGA development platform: Quartus prime.
- Programming language: VHDL
