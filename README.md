# HVDC Generation Simulation

**MATLAB/Simulink | Three-Phase AC to High-Voltage DC**

This project simulates stepping up **400 V AC** to **40 kV AC** using a three-phase transformer, then converting it to about **56 kV DC** with a **six-diode rectifier** and **capacitor filter**.

## Circuit

![HVDC Simulink circuit](images/hvdc-simulink-circuit.png)

**Design:** 400 V, 60 Hz source → Y–Y transformer (1:100) → six-pulse diode bridge → 20 µF capacitor → 10 kΩ load.

## Results

| Measurement | Simulation reading |
|---|---:|
| Input voltage (3 channels, RMS) | 400 / 400 / 400 V |
| Input current (3 channels, RMS) | 1394.73 / 1409.32 / 1390.94 A |
| Transformer output voltage (3 channels, RMS) | 40000.14 / 39999.75 / 40000.11 V |
| **DC output voltage** | **56,161.41 V** |
| **DC output current** | **5.62 A** |

### Waveforms

| Input AC | Transformer output AC | Rectified DC |
|:---:|:---:|:---:|
| ![Input](images/input-ac-waveforms.png) | ![Step-up](images/secondary-ac-waveforms.png) | ![DC](images/rectified-dc-waveform.png) |



## Run

Open **[HVDC_Simu.slx](HVDC_Simu.slx)** in MATLAB/Simulink with the required Simscape Electrical blocks and run the model.

## Team

- Turki Abdulrahman Al-Zahrani
- Sattam Turki Al-Otaibi
- Khalid Muteb Alhulayfi
- Abdulrahman Abdullah Alosaimi


