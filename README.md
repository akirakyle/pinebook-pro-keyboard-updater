# Pinebook Pro keyboard/touchpad firmware updater

This application does upgrade firmware of the built-in keyboard and touchpad.

## Compiling

```bash
git clone https://github.com/jackhumbert/pinebook-pro-keyboard-updater
cd pinebook-pro-keyboard-updater
sudo apt-get install build-essential libusb-1.0-0-dev xxd
make
```

## Pick right keyboard model

Pinebook Pro offers two keyboard types: `iso` and `ansi`.

Append your model type after the `step-1` or `step-2` command specifying `iso` or `ansi`.

**In order to update with `ansi` keyboard the external keyboard will be required as for the duration of the process the keyboard will stop working.**

## Update all firmwares

You need to do all of that in correct order,
if at any point process fails, start it from point 1.:

1. Run `step-1 iso` or `step-1 ansi` of update process: `sudo ./updater step-1 iso`,
1. After `step-1 iso` or `step-1 ansi` touchpad **will not work**, keyboard works as normal (this is true only for **ISO**, the **ANSI** keyboard will not work after `step-1`),
1. Reboot with `sudo reboot`,
1. After reboot, run `step-2 iso` or `step-2 ansi` of update process: `sudo ./updater step-2`,
1. Reboot with `sudo reboot`,
1. After reboot, your keyboard and touchpad firmware should be updated.

### Revised firmware

There has been some effort in `firmware/` to reverse engineer and customise the existing firmware, fixing some of the common issues people are facing. **Currently you need to flash this after steps 1 and 2 with a separate command**, `flash-kb-revised` followed by the keyboard type. No reboot is required after flashing, but may be needed if your keyboard/touchpad is unresponsive (currently rare). Changelogs and assembly code for each version can be found in `firmware/fw_<type>_revised.asm`.

```bash
# compile
git clone https://github.com/jackhumbert/pinebook-pro-keyboard-updater
cd pinebook-pro-keyboard-updater
sudo apt-get install build-essential libusb-1.0-0-dev xxd
make

# For ISO keyboard
# step-1
sudo ./updater step-1 iso
sudo reboot

# after reboot, step-2
sudo ./updater step-2 iso
sudo reboot

# For ANSI keyboard
# step-1
sudo ./updater step-1 ansi
sudo reboot

# after reboot, step-2
sudo ./updater step-2 ansi
sudo reboot

# updating to the revised ansi firmware after steps 1 and 2
sudo ./updater flash-kb-revised ansi

# updating to the revised iso firmware after steps 1 and 2
sudo ./updater flash-kb-revised iso

```

### Log from `STEP-1`

```bash
$ sudo ./updater step-1 iso
Running STEP-1...
[*] Flashing keyboard updater firmware...
>>> Fix hex file
[*] Opening in user mode...
>>> Trying to open VID:258a PID:001e...
>>> Device not found
>>> Trying to open VID:258a PID:001f...
[*] Sending command to switch to boot mode...
[*] Command send
>>> release interface
[*] Opening in boot mode
>>> Trying to open VID:0603 PID:1020...
>>> Device not found
>>> Trying to open VID:0603 PID:1020...
>>> Kernel Driver Active
[*] Erasing flash
[*] Writing firmware...
>>> USB: write_block_start (length=14336)
>>> USB: write_block (offset=0, length=2048)
>>> USB: write_block (offset=2048, length=2048)
>>> USB: write_block (offset=4096, length=2048)
>>> USB: write_block (offset=6144, length=2048)
>>> USB: write_block (offset=8192, length=2048)
>>> USB: write_block (offset=10240, length=2048)
>>> USB: write_block (offset=12288, length=2048)
>>> USB: write_block_start (length=14336)
>>> USB: write_block (offset=0, length=2048)
[*] Reading back firmware...
>>> USB: read_block_start (length=14336)
>>> USB: read_block (offset=0, length=2048)
>>> USB: read_block (offset=2048, length=2048)
>>> USB: read_block (offset=4096, length=2048)
>>> USB: read_block (offset=6144, length=2048)
>>> USB: read_block (offset=8192, length=2048)
>>> USB: read_block (offset=10240, length=2048)
>>> USB: read_block (offset=12288, length=2048)
[*] Comparing firmwares...
[*] Reseting device?
[*] Finished succesfully!
>>> release interface
[*] Please reboot now, and run `step-2`.
```

### Log from `STEP-2`

```bash
$ sudo ./updater step-2 iso
Running STEP-2...
[*] Flashing touchpad firmware...
[*] Opening in touchpad mode
>>> Trying to open VID:258a PID:001f...
>>> Kernel Driver Active
>>> Writing offset:0 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:1024 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:2048 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:3072 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:4096 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:5120 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:6144 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:7168 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:8192 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:9216 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:10240 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:11264 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:12288 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:13312 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:14336 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:15360 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:16384 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:17408 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:18432 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:19456 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:20480 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:21504 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:22528 length:1024...
>>> Verifying '1k-data'...
>>> Writing offset:23552 length:1024...
>>> Verifying '1k-data'...
[*] Verifying 'end-program'...
[*] Verifying 'checksum'...
[*] Verifying 'program'...
[*] Finished succesfully!
>>> release interface
[*] Flashing ISO keyboard firmware...
>>> Fix hex file
[*] Opening in user mode...
>>> Trying to open VID:258a PID:001e...
>>> Device not found
>>> Trying to open VID:258a PID:001f...
[*] Sending command to switch to boot mode...
[*] Command send
>>> release interface
[*] Opening in boot mode
>>> Trying to open VID:0603 PID:1020...
>>> Device not found
>>> Trying to open VID:0603 PID:1020...
>>> Kernel Driver Active
[*] Erasing flash
[*] Writing firmware...
>>> USB: write_block_start (length=14336)
>>> USB: write_block (offset=0, length=2048)
>>> USB: write_block (offset=2048, length=2048)
>>> USB: write_block (offset=4096, length=2048)
>>> USB: write_block (offset=6144, length=2048)
>>> USB: write_block (offset=8192, length=2048)
>>> USB: write_block (offset=10240, length=2048)
>>> USB: write_block (offset=12288, length=2048)
>>> USB: write_block_start (length=14336)
>>> USB: write_block (offset=0, length=2048)
[*] Reading back firmware...
>>> USB: read_block_start (length=14336)
>>> USB: read_block (offset=0, length=2048)
>>> USB: read_block (offset=2048, length=2048)
>>> USB: read_block (offset=4096, length=2048)
>>> USB: read_block (offset=6144, length=2048)
>>> USB: read_block (offset=8192, length=2048)
>>> USB: read_block (offset=10240, length=2048)
>>> USB: read_block (offset=12288, length=2048)
[*] Comparing firmwares...
[*] Reseting device?
[*] Finished succesfully!
>>> release interface
[*] All done! Your keyboard and touchpad should be updated.
```

## License

MIT, 2019, SHEN ZHEN HAI LUCK ELECTRONIC TECHNOLOGY CO., LTD
