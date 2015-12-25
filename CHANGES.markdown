JTAGulator Change Log
=====================

Visit the JTAGulator [github repository][0] for full commit comments.


1.3
---
Release date: **December 25, 2015**

* JTAG: Added support during `BYPASS_Scan` to accept known pins, if any. This can greatly reduce search time, especially if `IDCODE_Scan` was done first to identify all pins except for TDI.

* JTAG: Better verification of `BYPASS_Scan` results (limit to 32 maximum devices in the chain, call `BYPASS_Test` to ensure that the detected pin configuration actually works).

* JTAG: Modified `IDCODE_Known` to work without needing to know the number of devices in the JTAG chain.

* JTAG: Modified `BYPASS_Known` to automatically detect the number of devices in the JTAG chain (instead of asking the user).

* JTAG: Changed TDI to idle HIGH during `Get_Device_IDs` to conform to the IEEE 1149.1 specification.

* General: User can now specify a range of channels to scan instead of always starting at CH0 (`Get_Channels`). This allows multiple ports/targets to be hooked up to the JTAGulator without being forced to scan them all at the same time.

* General: JTAGulator will now remember the most recently detected pinout during a scan (until reset or a completed scan with no results). This allows the user to more easily enter the pin values in subsequent commands.

* General: Display a message if no target device(s) found during a scan.

* General: Added backspace support to user input (thanks to piggybanks).

* General: Minor code cleanup and text updates.


1.2.2
-----
Release date: **September 20, 2014**

* Modified `Set_Target_IO_Voltage` to print a confirmation of the newly set voltage (thanks to Crypt) and to print a warning that the user should NOT connect VADJ to the target (VADJ is used for level-shifting JTAGulator's I/O to match the target's I/O, NOT to externally power the target).


1.2.1
-----
Release date: **September 8, 2014**

* Added prompt to enable/disable local echo during UART passthrough (thanks to dummys). Local echo is turned off by default, since the target device normally controls whether or not to echo characters.

* Minor code cleanup


1.2
---
Release date: **August 7, 2014**

* Added support for detecting the optional JTAG nTRST pin. This pin is often pulled low on target systems, which will intentionally disable the JTAG interface. If it isn't one of the pins connected to the JTAGulator, the interface might not be discovered.

* Fixed/modified JTAG routines to more closely conform to the IEEE 1149.1 specification (thanks to Bryan Angelo @ Qualcomm).

* Added extended IDCODE decoding based on IEEE 1149.1 specification for easier/quicker identification of manufacturer, part number, and version (thanks to Bob Heinemann)

* Modified `UART_Scan` to display previously entered string, if any, as default and to accept hex values (when `\x` is used as the string prefix, ignore MSBs if they are NULL). 

* Changed command input to require that commands are terminated with a single CR or LF, instead of executing immediately after the character was entered.

* Added local echo into `Parallax Serial Terminal.spin` (thanks to HexView). This will make using JTAGulator easier across different terminal programs, many of which don't provide local echo by default.

* Added progress indicators (display a character on the screen and blink LED) to show that JTAGulation is active/working (`Display_Progress`)

* Added command to display firmware version information (`J`).

* Added JTAGulator logo and welcome message to start-up text.

* Minor code cleanup, optimizations, fixes to UI/input sanitization

* Release for [Black Hat USA 2014 Tools Arsenal][3].


1.1.1
-----
Release date: **August 6, 2013**

* Modifed `UART_Scan` and `UART_Passthrough` to stop the UART cog (`jdcogserial`) at the end of their functions. This prevents the cog from maintaining control of the pins, which would prevent subsequent, non-UART commands from working.


1.1
---
Release date: **August 1, 2013**

* Added support for UART discovery and passthrough mode (8N1).

* Adjusted `Set_JTAG` to only ask for the three required pins (TDO, TCK, TMS) when getting JTAG Device ID.

* Modified `Set_Target_Voltage` to allow you to turn off the target voltage output (VADJ).

* Re-organized code by subsystem (e.g., UART, JTAG, General).

* Release for [Black Hat USA 2013][2].


1.0.1
-----
Release date: **June 11, 2013**

* Added linefeeds to text output (for terminal programs that require CR+LF instead of just CR to display properly).

* Minor code cleanup.


1.0
---
Release date: **April 24, 2013**

* Initial release for [DESIGN West 2013][1].


[3]: https://www.blackhat.com/us-14/arsenal.html
[2]: https://www.blackhat.com/us-13/
[1]: http://www.ubmdesign.com/sanjose/
[0]: https://github.com/grandideastudio/jtagulator/commits/master
