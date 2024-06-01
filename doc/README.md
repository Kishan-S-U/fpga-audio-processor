Audio Processor
-
<img src="../res/block diagram.jpg" align="center"/>
The overall system comprising the codec chip, s2p adaptor, and FIR filter represents a complete digital signal processing (DSP) chain for audio data.

Design Steps
-
<img src="../res/waveform analysis.jpg" align="center" />
The figure above shows how the timing analysis was performed. 
1. Input data[AUD_ADCDAT] is in serial format. (16 bits long, since we are only performing analysis on left channel)
2. It will complete parallel conversion in 16 clock cycles [ADCDAT].
3. A strobe signal [ADCstb] is triggered, output buffer stores the parallel data.
4. On the next LRC, the output is transferred serially [DACDAT].
5. Since the mark-space ratio is 187:188, we can easily perform FIR filter operation within this time.

Codec Initializer
- 
The main purpose of this block is to initialize the on-board CODEC chip for the required specifications. This process is accomplished using the I2C protocol. This process involves two important parts, 
1. The data to be transferred depends on the required specifications, this data will be copied into the internal registers of the CODEC chip. There are a total of 11 registers with a size of 16 bits, each with a different purpose.
2. the format to send the register data is I2C protocol format (programmed accordingly).

S2P Adaptor
-
The main objective of this block is to bridge the gap between the serial data interface of the codec chip and parallel data processing requirements of the FIR filter. With the use of strobe and LRC signals for synchronization with the bit-clock provided by the codec chip. 

This block contains two operations, first is the conversion of input serial data to output parallel data and the second is vice-versa. Which are named input and output channel respectively. The complete data processing in this block runs synchronously with the bit-clock (AUD_BCLK) provided by the codec chip and this block processes 16-bit data.

FIR Filter
-
An FIR filter is characterized by its impulse response, which is finite because it settles to zero in a finite number of sample intervals. The filter’s output is computed as a weighted sum of the current and a finite number of previous input values. The weights are the filter’s coefficients, which, in our case, are (-1260, 7827, 12471, 16384, 16384, 12471, 7827, -1260).

The images below shows the frequency and phase response of this FIR filter.

<img src="../res/frequency response.png" align="center" title="Frequency Response"/> <img src="../res/phase response.png" align="center" title="Phase Response"/>
