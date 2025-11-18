# INTERFACING LED AND PWM, WITH LPC1768 ARM PROCESSOR.

# AIM:    
   To write an embedded c program to interface LED and PWM with ARM processor          LPC1768
          
# COMPONENTS REQUIRED:
##  HARDWARE:
ARM LPC1768
LED
## SOFTWARE:
KEIL MICRO VISION 4.0 IDE

# PROCEDURE:

## Procedure

1. Open the **Keil µVision** software and select **New µVision Project** from the **Project** menu.
2. Browse to your project folder, provide the **project name**, and click **Save**.
3. Once the project is saved, a new pop-up **“Select Device for Target”** appears. Select the controller **(NXP: LPC1768)** from **NXP (founded by Philips)** and click **OK**.
4. As **LPC1768** requires the startup code, click **Yes** to include the **LPC17xx Startup** file.
5. Create a new file by selecting **File → New** to write the program.
6. Type the code.
7. After typing the code, save the file as **main.c** (e.g., `abc.c`).
8. Right-click **Target 1** and add the suitable files to **Source Group 1** and the required **header files** for the project.
9. Add both **main.c** and **system_LPC17xx.c**.
10. Build the project and fix any compiler **errors/warnings** if present.
11. Once the code compiles successfully with no errors, note that the **.bin** file is still not generated.
12. Right-click **Target Options** to enable the option for generating a **.bin** file.
13. Set the **IROM1 start address** as **0x2000**.

    * The bootloader will be stored from **0x0000–0x2000**, so the application should start from **0x2000**.
14. Write the command to generate the **.bin** file from the **.axf** file:

    ```bash
    fromelf --bin projectname.axf --output filename.bin
    ```
15. In **C/C++ → Include Paths**, add the path to your library folder (e.g., `Desktop\00-libfiles`).
16. Rebuild the project.
17. The **.bin** file will be generated successfully.
18. Check the project folder for the generated **.bin** file.

---

### Files to be Added

* **main.c**
* **system_LPC17xx.c**
* **startup_LPC17xx.s**
* **projectname.uvprojx** (Keil project file)
* **projectname.uvoptx** (Keil project options file)
* **filename.bin** (generated binary file after build)


# ADD FILES:
- Target1:
- Source group1:
Startuplpc17xx.s, delay.c , gpio.c , pwm.c , sysytemlpc17xx.c, main.c
- Header:
delay.h, gpio.h, pwm.h, stdulils.h

# PIN DIAGRAM :

<img width="619" height="369" alt="image" src="https://github.com/user-attachments/assets/3a047c5b-aed8-4cbe-82e4-ed82c0891d09" />

# CIRCUIT DIAGRAM:

<img width="1071" height="542" alt="image" src="https://github.com/user-attachments/assets/344add23-41a1-402f-b223-b2547c8ccceb" />

# PROGRAM:
```C
#include <lpc17xx.h>
#include "pwm.h"
#include "delay.h"
#define CYCLE_TIME 100
/* start the main program */
int main()
{
int dutyCycle;
SystemInit(); /* Clock and PLL configuration */
PWM_Init(CYCLE_TIME); /* Initialize the PWM module and the Cycle time(Ton+Toff) is
set to 255(similar to arduino)*/
PWM_Start(PWM_3); /* Enable PWM output on PWM_1-PWM_4 (P2_0 - P2_3) */
while(1)
{
for(dutyCycle=0;dutyCycle<CYCLE_TIME;dutyCycle++) /* Increase the Brightness of the
Leds */
{
PWM_SetDutyCycle(PWM_3,dutyCycle); //P2_2
DELAY_ms(10);
}
17
for(dutyCycle=CYCLE_TIME;dutyCycle>0;dutyCycle--) /* Decrease the Brightness of the
Leds */
{
PWM_SetDutyCycle(PWM_3,dutyCycle); //P2_2
DELAY_ms(10);
}
}
}
```
# Output:

![WhatsApp Image 2025-11-13 at 15 35 43_e6fc9a3a](https://github.com/user-attachments/assets/3fbfbbe1-9885-439d-826b-3d9e4a60ef29)


# Result : 
Thus,an embedded C program is written in order to interface PWM with LPC1768.
