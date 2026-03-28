BG7TBL WB-SG1 8G Web Front End
=======================

**Quick Start**
---------------

1.  Host `index.html` on any HTTPS-enabled web server (e.g., GitHub Pages) or simply go to https://katzenjens.github.io/wbsg1
2.  Open the page in a Chrome or Edge browser. **Firefox won't work!**
3.  Click **CONNECT**, select your serial port (Default 9600 Baud), and you're ready to go!
4.  Read the full manual for the web front end here: https://github.com/katzenjens/wbsg1/blob/main/manual.md
* * *
🌐 Web Controller
-----------------
**Features (v1.9)**
-------------------
*   **Dual Channel VFO:** Independent control for CH1 (1 Hz – 250 MHz) and CH2 (35 MHz – 8 GHz).

*   **Variable Step Sizes:**
*   *   **CH1:** 1 Hz, 100 Hz, 1 kHz, 10 kHz, 100 kHz, 1 MHz.
*   *   **CH2:** 10 Hz, 1 kHz, 100 kHz, 1 MHz, 10 MHz, 100 MHz.
*   **Automatic Sync:** Upon connection, the app automatically queries the device and synchronizes the display with the current hardware frequency. If this fails, check if you are using the right port and check the USB cable.
*   **Full Sweep Support:** Dedicated controls for CH1 and CH2 with 9-digit precision.
*   **System Controls:** On-the-fly adjustment of LCD contrast (00-63), beeper toggle, modulation toggle and EEPROM saving.
*   **Debug Log:** Built-in terminal to monitor RX/TX traffic (selectable/copyable for troubleshooting).
*   **Privacy:** This web page is static. It does not share data with the web. No cookies are set. Everything will stay on the local machine. If in doubt, take a look at `index.html`.
*   **How does it work?** It uses `CSS`for the user interface and `Javascript`and `Web Serial` to connect with the signal generator. Inside the signal generator is an USB to serial converter type `FTDI`. All current operating systems should be able to connect without issues.
* * *
If you would like to build your own interface to this device feel free to use `protocol.md` and `fulldoc.md`.
