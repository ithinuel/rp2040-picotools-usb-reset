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

## Reset interface

The reset interface is modeled after the same on in the official pico-sdk.
See [definition](https://github.com/raspberrypi/pico-sdk/blob/2.0.0/src/rp2_common/pico_stdio_usb/stdio_usb_descriptors.c#L109)
and [usage](https://github.com/raspberrypi/pico-sdk/blob/2.0.0/src/rp2_common/pico_stdio_usb/reset_interface.c).

```
> lsusb -vd 2e8a:000a

Bus 003 Device 022: ID 2e8a:000a Fake company Picotool port
Couldn't open device, some information will be missing
Negotiated speed: Full Speed (12Mbps)
Device Descriptor:
  bLength                18
  bDescriptorType         1
  bcdUSB               2.10
  bDeviceClass            0 [unknown]
  bDeviceSubClass         0 [unknown]
  bDeviceProtocol         0
  bMaxPacketSize0         8
  idVendor           0x2e8a Fake company
  idProduct          0x000a Picotool port
  bcdDevice            0.10
  iManufacturer           1 Fake company
  iProduct                2 Picotool port
  iSerial                 3 TEST
  bNumConfigurations      1
  Configuration Descriptor:
    bLength                 9
    bDescriptorType         2
    wTotalLength       0x0012
    bNumInterfaces          1
    bConfigurationValue     1
    iConfiguration          0
    bmAttributes         0x80
      (Bus Powered)
    MaxPower              100mA
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        0
      bAlternateSetting       0
      bNumEndpoints           0
      bInterfaceClass       255 Vendor Specific Class
      bInterfaceSubClass      0 [unknown]
      bInterfaceProtocol      1
      iInterface              4
```
