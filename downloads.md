# Downloads

## Where to get payloads

Many payloads are hosted from the centralized library on the Hak5 git repository at [github.com/hak5/bashbunny-payloads](https://github.com/hak5/bashbunny-payloads). Payloads from this repository are contributed from the Bash Bunny community. As with any script downloaded from the Internet, you are advised to proceed with caution. Similarly, many community developed tools exist for working with the Bash Bunny, such as [BunnyToolkit.com](https://bunnytoolkit.com/).

**WARNING:** Community payloads come with absolutely no warranty. You are solely responsible for the outcome of their execution.

## Bash Bunny Firmware Upgrades

| Version | Changelog | Forum | SHA256 |
| ------- | --------- | ----- | ------ |
| [Download 1.5](https://storage.googleapis.com/bashbunny_updates/ch_fw_1.5_298.tar.gz) | [Changelog](https://storage.googleapis.com/bashbunny_updates/ch_fw_1.5-changelog.txt) | [Forum Thread](#) | ff2533d331dae2a299d57216be5cf0a8ec7c967e76761ae0e0fcc74c6925d003 |
| [Download 1.4](https://storage.googleapis.com/bashbunny_updates/ch_fw_1.4_284.tar.gz) | [Changelog](https://storage.googleapis.com/bashbunny_updates/ch_fw_1.4-changelog.txt) | [Forum Thread](https://forums.hak5.org/index.php?/topic/42073-release-bash-bunny-firmware-v14/) | 26d820fbaba708d74086f960e1ccd4daab884ce35f647f4e272dbe615db2dcf4 |
| [Download 1.3](https://storage.googleapis.com/bashbunny_updates/ch_fw_1.3_264.tar.gz) | [Changelog](https://storage.googleapis.com/bashbunny_updates/ch_fw_1.3-changelog.txt) | [Forum Thread](https://forums.hak5.org/index.php?/topic/40953-release-bash-bunny-firmware-v13/) | fe260b0a5f68c3b2c721fae111e970beaba3a47184df630b1c5bca1e567e4a81 |
| [Download 1.2](https://storage.googleapis.com/bashbunny_updates/ch_fw_1.2_249.tar.gz) | [Changelog](https://storage.googleapis.com/bashbunny_updates/ch_fw_1.2-changelog.txt) | [Forum Thread](https://forums.hak5.org/index.php?/topic/40902-release-bash-bunny-firmware-v12/) | c77be9d7a6526e9ce6b4b919b9cb7e3f7da48f059261622ab1713d8cc1814e84 |
| [Download 1.1](https://storage.googleapis.com/bashbunny_updates/ch_fw_1.1_228.tar.gz) | [Changelog](https://storage.googleapis.com/bashbunny_updates/ch_fw_1.1-changelog.txt) | [Forum Thread](https://forums.hak5.org/index.php?/topic/40661-release-bash-bunny-11/) | 3d768f70bdbc4b5209a587189ac71cbf8ad7ee394ede371c040695db95d9dd3b |

## Installation Overview

Your Bash Bunny can be easily upgraded to the latest firmware version. Just copying an upgrade file to the root of the Bash Bunny flash drive in arming mode, safely eject it, and plug it back into your computer in arming mode.

The first time the Bash Bunny is upgraded it will indicate the flashing process with a red blinking LED for up to 10 minutes. The flashing process will be followed by a green LED to indicate that the Bash Bunny is rebooting. Finally the standard slow blinking blue LED will indicate that the flashing process has succeeded and arming mode is ready.

**WARNING**: Do **not** unplug the Bash Bunny while firmware upgrade is in progress. Doing so will spell certain doom.
**WARNING**: Do **not** extract the contents of the downloaded `.tar.gz` to the Bash Bunny or change the name of the downloaded `.tar.gz` file. Doing so will put your Bash Bunny into a boot loop on firmwares 1.0 to 1.3.

**NOTE**: Following version 1.0, all future upgrades and firmware recoveries will be indicated by a special LED "police" pattern, alternating quickly between red and blue.

## Step by Step Firmware Upgrade Instructions

1. Download the latest version of the Bash Bunny firmware from [https://bashbunny.com/downloads](https://bashbunny.com/downloads)
2. Verify that the SHA256 checksum of the downloaded firmware files matches the checksum listed at bashbunny.com
3. Slide the Bash Bunny switch into Arming Mode (closest to the USB plug) and plug the Bash Bunny into your computer
4. Copy the firmware upgrade file downloaded in step 1 to the root of the Bash Bunny flash drive.
5. Safely eject the Bash Bunny flash drive (**IMPORTANT**)
6. With the switch still in Arming Mode, plug the Bash Bunny back into your computer and wait 10 minutes.

### LED Status for upgrades *from 1.0 to 1.1*

| LED           | Status |
| --- | --- |
| Red Blinking  | Flashing in progress |
| Green Solid   | Rebooting |
| Blue Blinking | Flash complete |

### LED Status for upgrades *from 1.1 onwards*

| LED | Status |
| --- | --- |
| Red/Blue Alternating | Flashing in progress |
| Green Solid | Rebooting |
| Blue Blinking | Flash complete |
