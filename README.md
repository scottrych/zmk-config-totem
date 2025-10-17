# ZMK Config for Totem Keyboard

This repository contains the ZMK firmware configuration for a Totem split keyboard with USB dongle support.

## Hardware Configuration

- **Keyboard**: Totem 38-key split keyboard
- **Microcontrollers**: Seeeduino XIAO BLE (left and right halves)
- **Dongle**: Nordic nRF52840 USB Dongle (acts as receiver)
- **Connection**: Wireless via Bluetooth Low Energy

## Firmware Files

This configuration builds **3 firmware files**:

1. **`totem_left-seeeduino_xiao_ble.uf2`** - Left keyboard half (includes ZMK Studio support)
2. **`totem_right-seeeduino_xiao_ble.uf2`** - Right keyboard half  
3. **`totem_dongle-nrf52840dongle_nrf52840.uf2`** - USB dongle/receiver

## How It Works

```
[Left Half] ----BLE----> [Dongle] ----USB----> [Computer]
[Right Half] ---BLE----> [Dongle]
```

- Both keyboard halves connect wirelessly to the USB dongle
- The dongle connects to your computer via USB and appears as a regular keyboard
- ZMK Studio is enabled for real-time keymap editing via USB connection

## Flashing Instructions

### Download Firmware

1. Go to the [Releases](https://github.com/scottrych/zmk-config-totem/releases) page
2. Download the latest firmware files from the **"v1.0-totem-ready"** release
3. Or check [GitHub Actions](https://github.com/scottrych/zmk-config-totem/actions) for the latest builds

### Flash the Keyboard Halves

For **Seeeduino XIAO BLE** boards:

1. **Enter Bootloader Mode**:
   - Connect the board to your computer via USB-C
   - Double-tap the RESET button quickly
   - The board should appear as a USB storage device

2. **Flash Left Half**:
   - Drag `totem_left-seeeduino_xiao_ble.uf2` to the USB storage device
   - The board will reboot automatically

3. **Flash Right Half**:
   - Drag `totem_right-seeeduino_xiao_ble.uf2` to the USB storage device
   - The board will reboot automatically

### Flash the USB Dongle  

For **Nordic nRF52840 USB Dongle**:

1. **Enter Bootloader Mode**:
   - Plug the dongle into a USB port
   - Press the RESET button on the dongle (small button on the side)
   - The dongle should appear as "NRF52BOOT" USB storage device

2. **Flash Dongle**:
   - Drag `totem_dongle-nrf52840dongle_nrf52840.uf2` to the "NRF52BOOT" device
   - The dongle will reboot and appear as "TOTEM" keyboard

## Pairing Process

1. **Flash all three devices** with their respective firmware
2. **Power on the keyboard halves** (they should start advertising for BLE connections)
3. **Plug in the USB dongle** - it will automatically discover and pair with both halves
4. **Test typing** - keys from both halves should work through the dongle

### Troubleshooting Pairing

- If pairing fails, press the **reset button** on each keyboard half
- Check battery levels (low battery can cause connection issues)
- Try moving the keyboard halves closer to the dongle during initial pairing
- Use the **Bluetooth clear binding** keys in layer 4 to reset connections if needed

## Keymap Features

### Layouts

- **Layer 0**: Base layer with home row mods (QWERTY-style layout)
- **Layer 1**: Navigation and numbers (F-keys, brackets, numbers)  
- **Layer 2**: Symbols and media (brightness, volume, arrow keys)
- **Layer 3**: Text Expander and Bluetooth controls (macros, BT management)

### Home Row Mods

- **Left**: `Ctrl` `Alt` `Cmd` `Shift` on A-S-R-T
- **Right**: `Shift` `Cmd` `Alt` `Ctrl` on N-E-I-O

### Custom Macros

- `:ls`, `:lt`, `:apup`, `:yup`, `dtim`, `dush` - Text expansion shortcuts
- Screenshot combinations for macOS
- Various development shortcuts

### Bluetooth Management

Layer 4 includes keys for:
- `BT_SEL 1-4` - Select Bluetooth profile
- `BT_CLR` - Clear current Bluetooth profile
- Bluetooth profile switching for multiple devices

## ZMK Studio

This configuration includes **ZMK Studio** support for real-time keymap editing:

1. Download [ZMK Studio](https://zmk.dev/docs/features/studio) 
2. Connect the **USB dongle** to your computer (not the keyboard halves)
3. Open ZMK Studio and it should detect your keyboard
4. Make real-time changes to your keymap without reflashing firmware

## Building Firmware

If you want to build the firmware yourself:

```bash
# Clone this repository
git clone https://github.com/scottrych/zmk-config-totem.git
cd zmk-config-totem

# Firmware will be built automatically by GitHub Actions
# Or build locally with ZMK toolchain - see ZMK documentation
```

## Configuration Files

- `config/totem.keymap` - Main keymap for keyboard halves
- `config/totem.conf` - Configuration for keyboard halves  
- `config/nrf52840dongle_nrf52840.keymap` - Keymap for USB dongle (mirrors main keymap)
- `config/nrf52840dongle_nrf52840.conf` - Configuration for USB dongle
- `build.yaml` - Build matrix for GitHub Actions

## Credits

- Based on the [Totem keyboard](https://github.com/GEIGEIGEIST/TOTEM) by GEIGEIGEIST
- ZMK firmware by the [ZMK Project](https://zmk.dev)
- Original config template from [Keycoon's zmk-config-totem](https://github.com/Keycoon/zmk-config-totem)