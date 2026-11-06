# High-Voltage DC (HVDC) Generation — MATLAB/Simulink

**Three-Phase AC → Step-Up Transformer → Six-Pulse Diode Bridge → Filter Capacitor → DC Load**

This educational simulation models high-voltage DC generation using MATLAB/Simulink. A balanced 400 V, 60 Hz three-phase source is stepped up to approximately 40 kV AC, rectified with a six-diode bridge, and filtered to supply a 10 kΩ DC load.

> **Simulation only:** This is a student course project, not a validated real-world HVDC power supply or a complete HVDC transmission link. High-voltage hardware must not be built from this model without an appropriate engineered design and safety review.

## Circuit diagram

![Complete Simulink HVDC circuit and displayed results](images/hvdc-simulink-circuit.png)

## Simulation results

The table below transcribes the **latest supplied Simulink screenshot**. These are shown values from the model, **not a new simulation run performed for this README**.

| Parameter | Value |
|:--|--:|
| Input three-phase line-to-line RMS voltage (A, B, C) | 400.00 / 400.00 / 400.00 V |
| Input source RMS current (A, B, C) | 1,394.73 / 1,409.32 / 1,390.94 A |
| Transformer secondary line-to-line RMS voltage (A, B, C) | 40,000.14 / 39,999.75 / 40,000.11 V |
| DC output voltage | **56,161.41 V (56.16 kV)** |
| DC output current | **5.62 A** |
| Load resistance | 10 kΩ |

**Recorded in a separate course-report capture:** DC output **approximately 56,571 V** and **5.66 A**. These values differ from the latest screenshot; the discrepancy has not been diagnosed and the two captures are deliberately kept separate.

### Input three-phase AC waveforms

![Three-phase input AC voltage waveforms from course-report simulation](images/input-ac-waveforms.png)

*Three-phase input voltage waveform (from the course report).*

### Transformer secondary AC waveforms

![Step-up transformer secondary AC voltage waveforms from course-report simulation](images/secondary-ac-waveforms.png)

*Stepped-up three-phase secondary voltages (from the course report).*

### Rectified DC output waveform

![Six-pulse rectified DC waveform from course-report simulation](images/rectified-dc-waveform.png)

*Rectified DC waveform showing periodic ripple (from the course report).*

> The waveform screenshots above come from the course report's simulation capture; they are illustrative of the model and are not claimed to be from the latest numeric screenshot.

## Model parameters

| Block / setting | Configuration |
|:--|:--|
| Three-phase AC source | 400 V line-to-line RMS, 60 Hz |
| Step-up transformer | Y–Y connection, 400 V / 40 kV nominal ratio (1:100) |
| Rectifier | Uncontrolled six-diode, three-phase full-wave bridge |
| Output filter | 20 µF capacitor in parallel with load |
| DC load | 10,000 Ω resistor |
| Simulation solver | Discrete `powergui`; sample time 50 µs (`5e-5 s`) |
| Simulation stop time | 0.08 s |
| Transformer nominal power parameter | 50 kVA in the saved model |

## Operating principle

1. **Three-phase source:** Supplies balanced AC voltage at 60 Hz.
2. **Transformer:** Raises 400 V line-to-line RMS to roughly 40 kV line-to-line RMS.
3. **Diode bridge:** Converts the three-phase AC into a six-pulse rectified waveform.
4. **Capacitor filter:** Reduces voltage ripple across the output terminals.
5. **Load and measurements:** A 10 kΩ resistor receives DC power; scopes and measurements display the voltage and current response.

## Quick analytical checks

- Voltage step-up ratio: `40,000 / 400 = 100`.
- Ideal secondary line-to-line peak: `sqrt(2) × 40,000 ≈ 56,569 V`.
- Current expected from the latest displayed DC voltage and 10 kΩ load: `56,161.41 / 10,000 ≈ 5.616 A`, consistent with **5.62 A**.
- An ideal six-pulse bridge on a 60 Hz supply has a ripple repetition frequency of `6 × 60 = 360 Hz` before smoothing.

These calculations are approximations and do not independently validate the model's detailed component behavior.

## How to open the project

**Required:** MATLAB and Simulink with the relevant Simscape Electrical / Specialized Power Systems blocks.

1. Download `HVDC_Simu.slx` from this repository.
2. Open MATLAB/Simulink and load the model.
3. Run the simulation and inspect its scopes, RMS measurements, and DC output displays.

```matlab
open_system('HVDC_Simu.slx');
sim('HVDC_Simu');
```

The saved model metadata indicates **R2023b**. Block support and model compatibility may differ between MATLAB releases.

## Important limitations

- The diode bridge is uncontrolled: DC output voltage is not adjustable by firing angle.
- A single 100:1 high-voltage transformer ratio would be challenging in physical hardware.
- **The saved transformer nominal power is 50 kVA, while the latest DC output readings imply about 315 kW across the load.** The rating/model inconsistency needs investigation; do not treat the shown values as a verified physical design.
- Ripple, losses, insulation and system protection need more realistic modeling for engineering application.

Potential extensions include an SCR-controlled rectifier, load/ripple sensitivity analysis, and improved transformer/protection models.

## Project files

```text
HVDC_Simu.slx
README.md
images/
    hvdc-simulink-circuit.png
    input-ac-waveforms.png
    secondary-ac-waveforms.png
    rectified-dc-waveform.png
```

## Academic project

Developed for a **High Voltage Engineering** course at **Taif University — Electrical Engineering Department (2026)** as a group simulation project. No personal/student identification numbers are included in this repository. Contributor attribution and licensing should be agreed upon by the project team before applying an open-source license.
