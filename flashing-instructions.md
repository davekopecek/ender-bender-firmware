# Flashing Instructions for Ender 3 (4.2.2 Board)

## Prerequisites
1. Complete the [PlatformIO setup](platformio-setup.md)
2. Download Marlin firmware source code (latest bugfix-2.1.x branch recommended)
3. Copy provided Configuration.h and Configuration_adv.h files to Marlin/Marlin directory

## Compilation Steps
1. Open the Marlin folder in VS Code
2. Select the correct environment:
   ```ini
   default_envs = STM32F103RET6_creality
   ```
3. Click the PlatformIO build button (checkmark icon) or use command:
   ```bash
   pio run
   ```
4. Find compiled firmware at:
   `.pio/build/STM32F103RET6_creality/firmware.bin`

## Flashing Process
1. Rename the compiled `firmware.bin` to `firmware.bin` (if different)
2. Format a microSD card (8GB or less recommended) to FAT32
3. Copy `firmware.bin` to the empty microSD card
4. With printer powered off, insert the microSD card
5. Power on the printer
6. Wait for screen to initialize (about 10-20 seconds)
7. If successful, the `firmware.bin` on SD card will be renamed to `FIRMWARE.CUR`

## Post-Flashing Configuration

### 1. Initialize EEPROM