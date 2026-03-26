📖 WB-SG1 Command Examples & Protocol Documentation
===================================================

This document contains verified communication logs and command structures for the **BG7TBL WB-SG1** Signal Generator.

* * *

📡 Frequency Settings (Manual Mode)
-----------------------------------

Set Frequency CH1 (BNC)
-----------------------

*   **Input:** `$F10100000000*` (e.g., 10 MHz)
*   **Output:** `CH1 0010000000Hz FOK<\r><\n>`
*   **Valid Range:** 1 Hz to 200 MHz
*   **Scaling:** 9 digits = frequency in **Hz**.
*   **Note:** Output always includes a leading zero.

Set Frequency CH2 (SMA)
-----------------------

*   **Input:** `$F28000000000*` (e.g., 8 GHz)
*   **Output:** `CH2 08000000000Hz FOK<\r><\n>`
*   **Valid Range:** 35 MHz to 8 GHz
*   **Scaling:** 9 digits = frequency in **Hz x 10**.
*   **Note:** Output always includes a leading zero.

* * *

🔄 Sweep Settings
-----------------

Set Sweep CH1 (BNC)
-------------------

*   **Input:** `$W3[Start][Stop][Steps]*`
    *   _Example:_ `$W3123456789123466789123456789*` (9 digits each)
*   **Output:** `CH1 STAR:0123456789Hz STOP:0123466789Hz POINT:0123456789 WOK<\r><\n>`
*   **Valid Range:** 1 Hz to 200 MHz
*   **Scaling:** Hz

> \[!IMPORTANT\] **Display Fix:** Before sending a new frequency command, send `$N*` **twice** to prevent display corruption.

Set Sweep CH2 (SMA)
-------------------

*   **Input:** `$W4[Start][Stop][Steps]*`
    *   _Example:_ `$W4123456789123466789123456789*`
*   **Output:** `CH2 STAR:0123456789Hz STOP:0123466789Hz POINT:0123456789 WOK<\r><\n>`
*   **Valid Range:** 35 MHz to 8 GHz
*   **Scaling:** Hz x 10

> \[!CAUTION\] **Firmware Bug:** Output frequency is displayed as **Hz x 10**, not Hz! **Display Fix:** Before sending a new frequency command, send `$N*` **once**.

* * *

🔊 System & Output Control (Toggle Commands)
--------------------------------------------

| Function | Command (Input) | Expected Output |
| --- | --- | --- |
| **Beep ON** | `$E3232*` | `BEEP ON EOK<\r><\n>` |
| **Beep OFF** | `$E3333*` | `BEEP OFF EOK<\r><\n>` |
| **CH2 Modulation ON** | `$E3838*` | `CH2 MOD ON EOK<\r><\n>` |
| **CH2 Modulation OFF** | `$E3939*` | `CH2 MOD OFF EOK<\r><\n>` |
| **CH1 Output ON** | `$E3434*` | `CH1 OUT ON EOK<\r><\n>` |
| **CH1 Output OFF** | `$E3535*` | `CH1 OUT OFF EOK<\r><\n>` |
| **CH2 Output ON** | `$E3636*` | `CH2 OUT ON EOK<\r><\n>` |
| **CH2 Output OFF** | `$E3737*` | `CH2 OUT OFF EOK<\r><\n>` |

* * *

⌨️ Key Simulation (Remote Control)
----------------------------------

| Key | Input | Output |
| --- | --- | --- |
| **Up** | `$U*` | `KEY UP UOK<\r><\n>` |
| **Down** | `$D*` | `KEY DOWN DOK<\r><\n>` |
| **Left** | `$L*` | `KEY LEFT LOK<\r><\n>` |
| **Right** | `$R*` | `KEY RIGHT ROK<\r><\n>` |
| **Enter (Set)** | `$S*` | `KEY ENT SOK<\r><\n>` |
| **Mode (Next)** | `$N*` | `KEY MODE NOK<\r><\n>` |

* * *

⚡ Baud Rate Configuration
-------------------------

The Baud Rate command is unique because it provides **no feedback**.

*   **Input:** `$B[BaudRate]*` (e.g., `$B115200*`)
*   **Output:** **None** (Immediate hardware switch)

> \[!WARNING\] Since the device does not confirm the change, the host software must wait and then re-establish the connection using the new Baud Rate.

* * *

ℹ️ Status & System Information
------------------------------

Read Current System State
-------------------------

This command returns a comma-separated string containing all current settings and hardware statuses.

*   **Input:** `$A*`
*   **Output:** `SYS STATE:CH1 0010000000Hz,OUT ON,CH2 08000000000Hz,OUT ON,MOD OFF,PLL LOCK,REF INT,BAUARD 0000009600 BPS,AOK<\r><\n>`

> \[!TIP\] **Developer Note for Parsing:** \> \* The output contains a typo: **`BAUARD`** instead of `BAUD`.
> 
> *   The status includes critical hardware flags like `PLL LOCK` (Signal stability) and `REF INT` (Internal Reference Clock).
> *   The baud rate in the status string is padded with leading zeros (e.g., `0000009600`).
>     

* * *

Power-On / Boot Message
-----------------------

When the device is powered on or reset, it sends a multi-line identification string:

```
<\r><\n>
WB-SG1-8G SSG <\r><\n>
CH1:1Hz-250MHz<\r><\n>
CH2:35MHz-8GHz<\r><\n>
BG7TBL V20250104<\r><\n>
```

*   **Model Identification:** `WB-SG1-8G SSG`
*   **Firmware Version:** `V20250104` (Date-based versioning)

* * *
