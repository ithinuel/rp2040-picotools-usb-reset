# usbd-picotool-reset

Implements a UsbClass to enable resetting on command sent by
[`picotool`](https://github.com/raspberrypi/picotool).

Rust 1.75 or later is required.

## Usage with example

```
# Flash onto a RP2040 in bootloader mode
> cargo run --example demo

# By default picotool does not want to reboot, unless you force it
> sudo ./picotool reboot
No accessible RP2040/RP2350 devices in BOOTSEL mode were found.

but:

Device at bus 3, address 19 appears to be a RP2040 device with a USB
    serial connection, so consider -f to force the reboot.

# Rebooting brings it back into the same application
> sudo ./picotool reboot -f
> lsusb -d 2e8a:0003
Bus 003 Device 019: ID 2e8a:000a Fake company Picotool port

# Reboot into bootloader mode
> sudo ./picotool reboot -f -u
> lsusb -d 2e8a:0003
Bus 003 Device 020: ID 2e8a:0003 Raspberry Pi RP2 Boot
```
