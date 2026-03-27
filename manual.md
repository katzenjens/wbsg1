* * *

User Manual: WB-SG1-8G Web Frontend
===================================

Connectivity & Privacy
----------------------

*   **Browser Compatibility:** This interface uses the Web Serial API and requires a **Chrome-based browser** (Chrome, Edge, Opera).
*   **Privacy:** The application runs entirely locally in your browser. No data is transmitted to the internet, and no cookies are used.
*   **Connection:** Click the **"CONNECT"** button to open the system dialog and select the appropriate serial port for your signal generator.

Frequency Control (VFO)
-----------------------

*   **Initial Sync:** Once connected, the displays for CH1 and CH2 will automatically synchronize with the current frequencies set on the hardware.
*   **Manual Adjustment:** To change the frequency, hover your mouse over the rotary knob and use the **mouse wheel**.
*   **Step Size:** Select the desired increment (from 1 Hz up to 100 MHz) using the buttons located to the right of the knobs.
*   **RF Output:** Use the **RF ON** and **RF OFF** buttons to toggle the signal output for each channel independently.

Sweep Functionality
-------------------

*   **Setup:** Enter the **Start** and **Stop** frequencies in Hz.
*   **Steps:** Define the number of steps for the sweep. Note that a higher number of steps increases the total sweep duration.
*   **Validation:** There is no plausibility check for inputs. Incorrect values may result in no signal output.
*   **Progress:** The sweep progress is visible only on the physical display of the signal generator.
*   **Exiting Sweep:** To return to fixed frequency mode from a sweep:
    *   **CH1:** Press the **"MODE"** button twice.
    *   **CH2:** Press the **"MODE"** button once.

Modulation & System Settings
----------------------------

*   **AM Modulation (CH2):**
    1.  Set the desired modulation frequency on **CH1** (e.g., 1,000 Hz).
    2.  Set the carrier frequency on **CH2**.
    3.  Toggle the **Modulation** slider to the right. _Note: If the slider is already in the ON position, toggle it OFF and ON again to ensure the command is sent._
*   **Beeper:** Toggles the audible confirmation beep for button presses on the hardware.
*   **Contrast:** Adjusts the LCD contrast. Recommended values are between **40 and 55**.
*   **SAVE:** Writes all current settings to the signal generator's internal EEPROM.
*   **Debug Log:** Opens a terminal window to monitor data transmission for troubleshooting.

* * *

Known Limitations
-----------------

Due to the current firmware version of the signal generator, there are some unavoidable constraints:

*   **One-Way Sync:** Only the frequency can be reliably read from the device upon connection. Other states (Sweep data, Beeper, Modulation, or RF status) cannot be queried accurately.
*   **UI State:** Consequently, the sliders and sweep inputs may not reflect the actual hardware state until you interact with them for the first time in your current session.
*   **Navigation:** Returning from Sweep mode to Fixed Frequency mode requires a manual "MODE" button press as described above.

Device Compatibility
--------------------

*   This frontend works on all devices with a USB interface running a Chrome-based browser.
*   **Android Devices:** Requires a mouse; touch input is currently not supported for the rotary knobs.
*   **Support:** If you encounter bugs, please open an **Issue** on the GitHub repository.

* * *

> \[!CAUTION\]
> 
> Important Hardware Note
> -----------------------
> 
> The output signal of this generator is a **square wave**, which generates significant **harmonics**. Do **NOT** connect this device directly to an antenna, as it will cause illegal radio interference!

* * *
