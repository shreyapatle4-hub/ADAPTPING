# ADAPTPING
<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/4f800405-cbcc-4948-9ec8-faa998aeef01" /># ADAPTPING
<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/4f800405-cbcc-4948-9ec8-faa998aeef01" /># ADAPTPIhttps://github.com/parthburangi2005-eng/ADAPTPING/blob/main/README.mdNG
___________________________________________________________________________________________________________________________________________________________________
A low-power, software-defined sonar payload for AUVs that dynamically adapts pulse-compression waveforms to real-time environmental water conditions using ESP32 DMA architecture

@@ -8,19 +8,21 @@ ________________________________________________________________________________
📌 Project Overview:---------------
AdaptPing is an advanced Minimum Viable Product (MVP) sonar transmitter payload designed for Autonomous Underwater Vehicles (AUVs). This repository contains the complete embedded firmware required to transform a standard ESP32 microcontroller into a highly adaptive, software-defined acoustic engine. Instead of transmitting basic static tones, the system dynamically calculates complex pulse-compression waveforms—including Linear Frequency Modulated (LFM) chirps, Geometric Doppler-tolerant sweeps, and Barker-13 phase-coded sequences.By reading real-time analog environmental sensors (such as turbidity and depth) and streaming the synthesized mathematical waveforms directly to the internal DAC via the I2S Direct Memory Access (DMA) controller, this payload achieves continuous environmental adaptation with near-zero active CPU load, ensuring maximum battery life for the host AUV.
___________________________________________________________________________________________________________________________________________________________________

Architecture Explanation:------------
Physical Inputs (The Sensory Layer):----- The system mimics an AUV's physical sensors. Analog dials pass through hardware RC filters to strip high-frequency electrical noise before the signal touches the microcontroller. A push-button allows the operator to instantly switch waveform modes.
___________________________________________________________________________________________________________________________________________________________________
ESP32 CPU Core (The Software-Defined Engine):------ The CPU acts as the "brain" for only a fraction of a second. It reads the filtered analog voltage, calculates the exact acoustic parameters needed to survive current water conditions, and runs the complex mathematics to generate the shape of the wave.
___________________________________________________________________________________________________________________________________________________________________
Autonomous DMA Engine (The Power-Saving ):---------- Once the CPU calculates the math, it stores the data in the SRAM buffer and goes to sleep. The independent Direct Memory Access (DMA) hardware controller wakes up and streams that memory directly to the DAC. Because the internal ESP32 DAC only supports 8-bit resolution but the internal I2S driver strictly requires 16-bit words, the software mathematically shifts the 8-bit data into the Most Significant Byte (MSB) position using the << 8 bitwise operator. This achieves the zero-CPU transmission required to save AUV battery life.
___________________________________________________________________________________________________________________________________________________________________
Output & Validation (The Real-World Proof):--------- The digital data is transformed into a physical analog wave. A custom voltage divider steps the 3.3V signal down safely so it can be fed into a PC audio jack. Real-time Fast Fourier Transform (FFT) spectrogram software visually proves that the bandwidth, frequency, and time duration are actively shifting on command.
___________________________________________________________________________________________________________________________________________________________________

Component,Purpose / Wiring:-----------

ESP32 DevKit V1,The main controller..
10k Potentiometer,Wire wiper to GPIO 32. Simulates the Turbidity sensor.
Push Button,Wire to GPIO 4 and GND. Switches the acoustic modes.
10k & 4.7k Resistors,Voltage divider on GPIO 25 to protect the PC audio card.
3.5mm AUX Cable,Spliced to feed the voltage divider output to a PC microphone jack.
ESP32 DevKit V1,The main controller.........................
10k Potentiometer,Wire wiper to GPIO 32. Simulates the Turbidity sensor............................
Push Button,Wire to GPIO 4 and GND. Switches the acoustic modes.........................
10k & 4.7k Resistors,Voltage divider on GPIO 25 to protect the PC audio card..................
3.5mm AUX Cable,Spliced to feed the voltage divider output to a PC microphone jack.....................
