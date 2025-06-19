# Breathing Sensor Design and Implementation
## Introduction
Traditional breathing monitoring methods are often manual, which are inefficient, prone to error, and not continuously tracked, yet irregular breathing or temporary cessation of breathing can be life-threatening if not noticed. This design includes a wearable breathing sensor that alerts the caregiver, thereby enabling prompt intervention.
## Working Principle
The breathing sensor is a knitted conductive stretch sensor around the chest. It is made from interwoven conductive thread whose electrical resistance changes with its geometric shape (R=ρ L/A) (Lumen Learning, 2025). As the sensor stretches during user’s inhalation, length (L) increases and its cross-sectional area (A). This increases R. After conversion of the resistance to output voltage, the Arduino’s analogue input captures the output voltage change as a waveform in order to model chest motion (i.e. breathing motion).
By applying the formula V_out = (analogRead value / 1023) * 5V; sensor’s voltage output can be derived in reference to a fixed resistor, R_ref= 108ohms. The choice of R_ref  affects the overall sensitivity of the stretch sensor. An increase in the sensor’s resistance translates to a higher V_out reading, which makes the analysis of breathing frequency and depth more straightforward.
## Circuit Selection and Design
Arduino cannot measure resistance directly; it can only measure voltage. So, there are two ways to covert resistance into output voltage:
1. **Ohm’s Law (V=I∙R)**: This approach is accurate but it requires additional power regulation components to make (I=constant), so it is not ideal for simple, low-cost microcontroller designs.
2. **Voltage Divider**: It is a simple circuit on which the breathing sensor is connected in series with a fixed resistor, the output volage (i.e. the voltage measured by the Arduino) is such that: V_out=V_in×(R_sensor/(R_ref+R_sensor)) (Hamel, 2025).
   
This design adopts the voltage divider due to its simplicity, low cost, and compatibility with Arduino’s analogue input. The circuit diagram is shown in Figure x.1, a fixed resistor (R_ref = 108 ohms) is connected in series with the attached breathing sensor. 
![image](https://github.com/user-attachments/assets/69e38696-04dd-4307-a6be-7166fa097042)

## Technical Implementation
The breathing sensor was sewn into an elastic waistband in a zig-zag pattern to increase its sensitivity to stretch (see Figure 1). The circuit was powered by the Arduino’s 5V output, with V_out connected to analogue pin A0 (see Figure 2). For prototyping, the sensor was connected to the voltage divider on a breadboard by alligator clips.
![image](https://github.com/user-attachments/assets/21b2baca-3b63-4215-8d79-b6dcbfad7153)

## Testing and Results Analysis (Isolated Module Testing)
### Testing Environment:
* Power Supply: USB 5V regulated
* Microcontroller: Arduino UNO
* Connection Method: Breadboard with alligator clips and jump wires attached.
* Serial Monitoring: Arduino IDE Serial Monitor (9600 baud rate)
### Observations:
Below are examples of the voltage waveform and analogue values captured during testing:
![image](https://github.com/user-attachments/assets/8bf0925b-8798-416f-9532-6d9d8db9338b)

