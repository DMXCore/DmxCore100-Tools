# CM5 bootloader EEPROM image

`pieeprom.upd` is the Raspberry Pi bootloader release **2026-08-12** for the BCM2712
family (`firmware-2712/latest/pieeprom-2026-08-12.bin` from raspberrypi/rpi-eeprom) with the
DMX Core 100 CM5 configuration applied (identical to the CM5 factory / usbboot `recovery5`
defaults):

```
[all]
BOOT_UART=1
POWER_OFF_ON_HALT=1
BOOT_ORDER=0xf2461
```

`pieeprom.sig` is the SHA-256 of `pieeprom.upd` plus a timestamp, in the format the
bootloader self-update expects.

Why: CM5 modules without Wi-Fi shipped with the 2024-09-23 bootloader, which leaves the
3.7 V Wi-Fi rail and SDIO2 enabled; Raspberry Pi fixed that in the 2025-02-11 release and
recommends 2025-03-10 or newer for CM5. A DMX Core 100 CM5 unit on the old bootloader lost
power spontaneously up to 20 times a day; none since the update.

How it is applied: `init-scripts/update-hostos.sh -e` copies both files to `/mnt/boot`. On
the next boot the bootloader verifies the hash, flashes itself and deletes the files. Check
afterwards with `vcgencmd bootloader_version` (inside the app container) or read
`/proc/device-tree/chosen/bootloader/build-timestamp` on the host.

To rebuild for a newer release: `rpi-eeprom-config --config boot.conf --out pieeprom.upd
pieeprom-<date>.bin`, then `rpi-eeprom-digest -i pieeprom.upd -o pieeprom.sig`.
