# PlatformIO Setup Instructions for Marlin Firmware Development

## Introduction
PlatformIO is an open-source ecosystem for embedded development that we'll use to compile and manage our Marlin firmware for the Ender 3 printer. It integrates seamlessly with Visual Studio Code and provides all necessary tools and dependencies for building Marlin firmware.

## Prerequisites
- Visual Studio Code installed 

## Setup Instructions

### 1. Install PlatformIO Extension
1. Open VS Code
2. Click the Extensions icon in the sidebar (or press `Ctrl+Shift+X`)
3. Search for "PlatformIO"
4. Install "PlatformIO IDE" extension
5. Restart VS Code when prompted

### 2. Open Project
Open the `Marlin-2.1.x` directory in VS Code using:
- File -> Open Folder
- Select the `Marlin-2.1.x` directory

### 3. Configure PlatformIO
The project includes a `platformio.ini` configuration:

### Update platformio.ini
Add the following to  `platformio.ini`:
```ini
[platformio]
default_envs = STM32F103RET6_creality

[env:STM32F103RET6_creality]
platform = ststm32
board = genericSTM32F103RE
framework = arduino
build_flags =
    -DCONFIG_FILE=ender3/ender3-crtouch.ini
    -DUSE_CONFIG_OVERRIDE
board_build.offset = 0x8000
```

### 4. Using PlatformIO

The PlatformIO interface appears in the VS Code sidebar with several useful buttons:

- **Home** (House icon): Opens PlatformIO home screen
- **Build** (Checkmark icon): Compiles the firmware
- **Upload** (Right arrow icon): Not used for Ender 3 (we use SD card flashing)
- **Clean** (Trash icon): Cleans build files

### 5. Building Firmware

1. Click the PlatformIO Build button (checkmark icon)
2. Wait for compilation to complete
3. Find the compiled firmware at:
   `.pio/build/STM32F103RET6_creality/firmware.bin`

### 6. Next Steps

After successful compilation, follow the flashing instructions in [flashing-instructions.md](flashing-instructions.md) to upload the firmware to your printer.

## Common Operations

### Rebuilding After Configuration Changes
1. Make changes to your configuration files in the `configs/ender3` directory
2. Clean the project using the PlatformIO Clean button
3. Rebuild using the Build button
4. Flash the new firmware following the flashing instructions

### Troubleshooting
- If build fails, check the Terminal panel in VS Code for error messages
- Ensure all configuration values in your INI files are valid
- Verify the correct environment is selected in `platformio.ini`
- Make sure all symbolic links are correctly set up as shown in the project structure

For more detailed configuration management, refer to the [managing-configurations.md](managing-configurations.md) file in the project documentation.

## Related Documentation
- For flashing instructions, see [flashing-instructions.md](flashing-instructions.md)
- For configuration management, see [managing-configurations.md](managing-configurations.md)
