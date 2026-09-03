# Init Scripts

Update Balena HostOS with the following command to automatically detect the base board version:

```bash
curl -s -L https://github.com/DMXCore/DmxCore100/raw/refs/heads/main/init-scripts/update-hostos.sh | bash
```

To force a specific base board version (e.g., `v1` or `v2`), use the `-v` option:

```bash
curl -s -L https://github.com/DMXCore/DmxCore100/raw/refs/heads/main/init-scripts/update-hostos.sh | bash -s -- -v v1
```

or

```bash
curl -s -L https://github.com/DMXCore/DmxCore100/raw/refs/heads/main/init-scripts/update-hostos.sh | bash -s -- -v v2
```


To also stage the CM5 bootloader EEPROM update (see `eeprom/cm5/README.md`), add `-e`; the
bootloader applies it on the next reboot:

```bash
curl -s -L https://github.com/DMXCore/DmxCore100/raw/refs/heads/main/init-scripts/update-hostos.sh | bash -s -- -e
```

The script always prints the CM5 bootloader date and warns when it is older than 2025-03-10.

To display usage information, use the `-h` option:

```bash
curl -s -L https://github.com/DMXCore/DmxCore100/raw/refs/heads/main/init-scripts/update-hostos.sh | bash -s -- -h
```

**Note**: You have to reboot after to have the changes take affect.

## For SNAP store applications (not applicable to DMX Core 100 hardware)
Update the network config settings with this command:
```bash
curl -s -L https://github.com/DMXCore/DmxCore100/raw/refs/heads/main/init-scripts/set-network-config.sh | sudo bash
```
