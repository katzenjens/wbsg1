# wbsg1
* * *

BG7TBL WB-SG1-8G Signal Generator Protocol Documentation
========================================================

This repository contains the reverse-engineered serial protocol for the **BG7TBL WB-SG1-8G** (1Hz - 8GHz) wideband signal generator. Since official documentation is scarce, this community-driven guide aims to help developers and radio amateurs automate their devices.

🔌 Connection Settings
----------------------

Default connection parameters for the internal USB-to-Serial (FTDI) interface:

*   **Baudrate:** `9600` (Default) or `115200` (via command)
*   **Data bits:** `8`
*   **Parity:** `None`
*   **Stop bits:** `1`
*   **Flow Control:** `None`
*   **Line Ending:** `CR+LF` (`\r\n`)

* * *

🛠 Command Set
--------------

All commands follow the `$X...*` syntax.

| Command | Parameter | Description | Example |
| --- | --- | --- | --- |
| **`$A*`** | None | Get system status (Freq, Lock, etc.) | `$A*` |
| **`$F[K][Hz]*`** | K=Channel (1/2), Hz=10 digits | Set static frequency 1=BNC, 2=SMA | `$F20100000000*` (100MHz) |
| **`$W[K][S][E][St]*`** | K=ID (3/4), S=Start, E=End, St=Steps | Start Frequency Sweep 3=BNC, 4=SMA | `$W4...*` |
| **`$CX*`** | X = 0 to 7 | **LCD Contrast** (0=Light, 7=Dark) | `$C3*` |
| **`$B[Bd]*`** | Bd = Baudrate | Change Serial Speed (volatile) | `$B115200*` |
| **`$S*`** | None | Save settings to EEPROM | `$S*` |
| **`$Exxxx*`** | Register Pair | Hardware Toggles (see below) | `$E3232*` |

* * *
Buttons
-------
*   **`$U*`**: Button Up
*   **`$D*`**: Button Down
*   **`$L*`**: Button Left
*   **`$R*`**: Button Right
*   **`$S*`**: Button ENT
*   **`$N*`**: Button MODE
* * *

🏗 Hardware Registers (\$E)
---------------------------

The device uses register pairs for switching.

*   **`$E3232*` / `$E3333*`**: System Beeper (On/Off)
*   **`$E3434*` / `$E3535*`**: Channel 1 (BNC) Output (On/Off)
*   **`$E3636*` / `$E3737*`**: Channel 2 (SMA) Output (On/Off)
*   **`$E3838*` / `$E3939*`**: Internal Modulation (On/Off)

* * *

⚠️ Known Issues & Workarounds
-----------------------------

1\. The Contrast "Whiteout"
---------------------------

The `$C` command only accepts values from **0 to 7**. Sending longer values or values outside this range can cause the LCD to overflow and turn completely white.

*   **Recovery:** Send `$C3*` followed by `$S*` blindly via terminal.

2\. Sweep-to-Static Transition
------------------------------

When a sweep is active, the device often ignores static frequency commands (`$F`).

*   **Workaround:** Emulate a "Mode" button press using `$N*` to return to point-frequency mode before sending a new `$F` command.

3\. Baudrate Handshake
----------------------

Baudrate changes via `$B` are immediate but not permanent.

*   **Pro-Tip:** If the connection is lost after `$B`, power-cycle the device to return to the 9600 baud safety net.

* * *

🌐 Web Controller
-----------------

A web-based controller using the **Web Serial API** is currently under development. Stay tuned!

* * *
