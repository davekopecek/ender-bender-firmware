# Managing Multiple Marlin Configurations

## Directory Structure
```
📁 Marlin-2.1.x
├── 📁 Marlin
│   └── 📁 config
│       └── 📁 ender3
│           ├── 📄 ender3-crtouch.ini      # CR Touch/BL Touch configuration
│           └── 📄 ender3-stock.ini        # Stock configuration
```

## Switching Configurations

### Method 1: Using platformio.ini
```ini
[platformio]
default_envs = STM32F103RET6_creality

[env:STM32F103RET6_creality]
platform = ststm32
board = genericSTM32F103RE
framework = arduino
build_flags =
    -DCONFIG_FILE=ender3/ender3-crtouch.ini  # Change this line to switch configs
    -DUSE_CONFIG_OVERRIDE
board_build.offset = 0x8000
```

### Method 2: Using Build Environments
```ini
[platformio]
default_envs = ender3_crtouch  # Change this to switch default config

[env:ender3_crtouch]
platform = ststm32
board = genericSTM32F103RE
framework = arduino
build_flags =
    -DCONFIG_FILE=ender3/ender3-crtouch.ini
    -DUSE_CONFIG_OVERRIDE

[env:ender3_stock]
platform = ststm32
board = genericSTM32F103RE
framework = arduino
build_flags =
    -DCONFIG_FILE=ender3/ender3-stock.ini
    -DUSE_CONFIG_OVERRIDE
```

## Building Different Configurations

### Using VSCode
1. Click the PlatformIO icon
2. Expand 'Project Tasks'
3. Select the environment
4. Click 'Build'

### Using Command Line
```bash
# Build specific environment
pio run -e ender3_crtouch

# Build default environment
pio run

# Clean before building
pio run -t clean
pio run -e ender3_crtouch
```

## Version Control Tips

### Branch Strategy
```bash
# Create branch for each configuration
git checkout -b ender3/crtouch
git checkout -b ender3/stock
git checkout -b ender3-pro/crtouch

# Save configuration changes
git add Marlin/config/ender3/ender3-crtouch.ini
git commit -m "Update CR Touch configuration"
```

### Configuration Backup
```bash
# Backup all configurations
cp -r Marlin/config ~/marlin-configs-backup/

# Backup specific configuration
cp Marlin/config/ender3/ender3-crtouch.ini ~/marlin-configs-backup/
```

## Learn from my mistakes
1. Keep one configuration per file
2. Comment all custom changes
3. Test configurations in separate branches
4. Maintain a backup of working configurations
5. Document probe offsets and PID values
6. Include printer-specific notes in comments
