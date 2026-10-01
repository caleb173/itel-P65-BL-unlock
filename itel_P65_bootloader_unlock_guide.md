# Unlocking the Bootloader of itel P65 (P671L)

*Using CVE-2022-38694 on a Unisoc T615 (UMS9230) Device*

A Complete Step-by-Step Guide With Challenges & Solutions

By Caleb | April 2026

> **IMPORTANT:** This guide involves modifying low-level device firmware. Done incorrectly it can brick your device. Proceed only if you understand the risks. The author takes no responsibility for damaged devices.

## Introduction & Background

This guide documents the complete process of unlocking the bootloader of an itel P65 smartphone (model number P671L) running Android 14 with HiOS V14.0.0. The device uses a Unisoc T615 (UMS9230) chipset with UFS storage — a combination that makes standard bootloader unlocking methods impossible.

The itel P65 does not support fastboot OEM unlock commands. Despite having 'OEM Unlock' enabled in Developer Options, every standard method fails. This guide covers how we used CVE-2022-38694, a publicly disclosed vulnerability in Unisoc's Boot ROM, to unlock the bootloader — and how we overcame every obstacle along the way.

This device was not officially listed in the CVE exploit's support list, making this guide particularly valuable for owners of similar unlisted Unisoc devices.

### Target Audience

This guide is written for technically inclined Android enthusiasts who are comfortable with Linux terminals, ADB/fastboot, and understand that mistakes at this level can brick a device. If you are new to Android modding, please research each step thoroughly before proceeding.

## 1. Device & Environment Information

| Property | Value |
| --- | --- |
| Device Name | itel P65 (Marketing) / itel P671L (Model Number) — same device |
| Chipset | Unisoc T615 (UMS9230) |
| Storage Type | UFS (NOT eMMC — critical difference for exploit) |
| Android Version | Android 14 (V14.0.0, HiOS V14.0.0) |
| Storage | 128GB |
| Active Boot Slot | Slot A |
| OEM Unlock Setting | ENABLED in Developer Options (required first step) |
| PC Operating System | Linux (Ubuntu-based) |


### Why Standard Methods Fail on This Device

- `fastboot oem unlock` — returns 'Unlock bootloader fail'
- `fastboot flashing unlock` — returns 'unknown command'
- `fastboot getvar all` — returns empty response
- `fastboot flash boot` — accepts the file transfer but fails with 'Flashing Lock Flag is locked'

The itel P65 runs a stripped-down, non-standard implementation of fastboot. The only way to unlock is through BROM (Boot ROM) mode using the CVE-2022-38694 exploit.

## 2. Resources & Tools Required

### Software Tools

| Tool | Source / Description |
| --- | --- |
| spd_dump | github.com/TomKing062/CVE-2022-38694_unlock_bootloader — main exploit tool (C program, needs compilation) |
| gen_spl-unlock | Included in CVE repo — generates the unlock payload from splloader backup |
| chsize | Included in CVE repo — utility tool (compile alongside gen_spl-unlock) |
| ADB & Fastboot | Android Platform Tools — standard Android debugging tools |
| Stock Firmware | itel P671L firmware
| fdl1-dl.bin | Downloaded from itel S23 GitHub repo — correct FDL1 loader for spd_dump |
| fdl2-dl.bin | Downloaded from itel S23 GitHub repo — correct FDL2 loader for spd_dump |
| fdl2-cboot.bin | Downloaded from itel S23 GitHub repo — modified uboot for unlock operation |
| GCC / Make | Standard Linux build tools — for compiling the exploit |

### Critical File Distinctions (Lessons Learned)

> ⚠ `fdl1-sign.bin` and `lk-fdl2-sign.bin` from your stock firmware are NOT suitable as FDL loaders for spd_dump. They are production bootloaders, not download-mode loaders. Using them will cause errors.

> ⚠ `u-boot-spl-16k-emmc-sign.bin` is for eMMC devices. The P671L uses UFS — NEVER use eMMC files.

> ✅ Use `fdl1-dl.bin` and `fdl2-dl.bin` from the itel S23 repo — these are the correct download-mode loaders for UMS9230 UFS devices.

### Key Exploit Parameters for itel P671L

| Parameter | Value | Notes |
| --- | --- | --- |
| exec_addr | `0x65015f08` | Found via loadexec command — P671L specific (S23 guide uses 0x65015f48) |
| FDL1 load address | `0x65000800` | Confirmed working (0x65000000 causes timeout) |
| FDL2 load address | `0x9efffe00` | Standard for UMS9230 |
| gen_spl-unlock offset | `0xfd28` | Argument to gen_spl-unlock for this firmware version |
| BROM USB ID | `1782:4d00` | Spreadtrum BROM — what spd_dump needs |

## 3. Preparation Steps

### Step 1 — Enable OEM Unlock on the Phone

1. Go to Settings > About Phone > tap Build Number 7 times to enable Developer Options
2. Go to Settings > Developer Options > enable OEM Unlocking
3. Enable USB Debugging in the same menu

> ⚠ OEM Unlock must be enabled BEFORE starting the exploit. This is a prerequisite.

### Step 2 — Clone and Compile the Exploit

Clone the repository:

```bash
git clone --recursive https://github.com/TomKing062/CVE-2022-38694_unlock_bootloader.git
```

Navigate to the UMS9230 directory:

```bash
cd CVE-2022-38694_unlock_bootloader/soc/ums9230/
```

Compile spd_dump:

```bash
make
```

Compile the additional tools:

```bash
gcc -o chsize ../chsize.c
gcc -o gen_spl-unlock ../gen_spl-unlock.c
```

✅ Result: `spd_dump` (84KB), `chsize`, and `gen_spl-unlock` executables in the `ums9230/` directory

### Step 3 — Download the Correct FDL Files

These must be downloaded from the itel S23 repository — NOT taken from your stock firmware:

```bash
wget https://github.com/[itel-S23-repo]/fdl1-dl.bin
wget https://github.com/[itel-S23-repo]/fdl2-dl.bin
wget https://github.com/[itel-S23-repo]/fdl2-cboot.bin
```

Place all three files in `~/CVE-2022-38694_unlock_bootloader/soc/ums9230/`

### Step 4 — Configure udev Rules

Allow Linux to communicate with Spreadtrum USB devices without permission errors:

```bash
echo 'SUBSYSTEM=="usb", ATTRS{idVendor}=="1782", MODE="0666"' | sudo tee /etc/udev/rules.d/99-sprd.rules
sudo udevadm control --reload-rules && sudo udevadm trigger
```

### Step 5 — Verify ADB Connection

```bash
adb devices
```

Confirm your device appears. Note the device ID for reference.

## 4. Entering BROM Mode — The Critical Skill

BROM (Boot ROM) mode is the lowest-level mode of the Unisoc chipset. It cannot be disabled or erased — the device is always recoverable as long as BROM is accessible. Entering it correctly is the most important physical skill in this guide.

### USB ID Reference

| USB ID | Mode | Works with spd_dump? |
| --- | --- | --- |
| `1782:4d00` | BROM mode — Vol Down + USB while phone is OFF | YES ✅ |
| `1782:4ee0` | Fastbootd userspace (Recovery > Enter Fastboot) | NO ❌ |
| `18d1:4ee0` | Bootloader fastboot (Recovery > Reboot to Bootloader) | NO ❌ |
| `1782:xxxx` | Normal Android / ADB mode | NO ❌ |

### Confirmed BROM Entry Method for itel P671L

1. Start the `spd_dump` command on PC FIRST and wait for 'Waiting for dl_diag connection'
2. Power the phone off completely (or ensure it is already off)
3. Wait 5-10 seconds after the screen goes completely black
4. Hold the Vol Down button firmly
5. While holding Vol Down, plug the USB cable into the PC
6. Hold for 3-5 seconds, then release
7. spd_dump will automatically detect and connect — screen stays BLACK (this is normal)

> ⚠ NEVER run `watch -n 1 lsusb` or any other command that holds the USB device while spd_dump is running — this causes `LIBUSB_ERROR_BUSY` and the connection will fail.

> ⚠ Always start spd_dump BEFORE entering BROM mode. If you plug in first, another process may grab the USB device.

> 💡 If it fails, unplug USB, wait 10 seconds, and try again. BROM is always accessible.

## 5. Challenges Faced & How We Overcame Them

### Challenge 1 — `fastboot oem unlock` Simply Doesn't Work

**The Problem**

Despite having OEM Unlock enabled in Developer Options, every fastboot unlock command failed. `fastboot oem unlock` returned 'Unlock bootloader fail'. `fastboot flashing unlock` returned 'unknown command'. Even `fastboot getvar all` returned empty output.

**The Solution**

Unisoc devices use a completely non-standard fastboot implementation. Standard fastboot unlock is not supported. The CVE-2022-38694 exploit bypasses fastboot entirely and works directly through BROM mode.

### Challenge 2 — git clone Missing Submodule

**The Problem**

An initial clone of the repository left the `spreadtrum_flash` submodule empty, causing `spd_dump.py` not to be found. This was a leftover issue from a previous session.

**The Solution**

```bash
rm -rf CVE-2022-38694_unlock_bootloader
git clone --recursive https://github.com/TomKing062/CVE-2022-38694_unlock_bootloader.git
```

The `--recursive` flag ensures all submodules are cloned. Also note: spd_dump is a C program that needs compilation, not a Python script.

### Challenge 3 — Wrong FDL Files

**The Problem**

The stock firmware contains `fdl1-sign.bin` and `lk-fdl2-sign.bin`. Logically these seem like the right files to use as FDL1 and FDL2 loaders. Using them caused PIPE errors, timeouts, and 'incompatible partition' errors.

**The Solution**

These production bootloader files are NOT download-mode loaders. spd_dump requires special `fdl1-dl.bin` and `fdl2-dl.bin` files. The correct files were found in the itel S23 GitHub repository and downloaded separately. These files are compatible with UMS9230 UFS devices.

### Challenge 4 — Finding the Correct exec_addr

**The Problem**

The exploit requires sending a custom payload to the correct memory address (exec_addr). The itel S23 guide specified `0x65015f48`, but using this address on the P671L caused incorrect behavior.

**The Solution**

The `loadexec` command in spd_dump reads the correct exec_addr directly from the device:

```bash
sudo ./spd_dump --wait 300 loadexec custom_exec_no_verify_65015f08.bin fdl fdl1-dl.bin 0x65000800
```

The device reported: 'current exec_addr is 0x65015f08' — confirming the P671L uses `0x65015f08`, not `0x65015f48`. This is the payload filename as well.

### Challenge 5 — FDL1 Address Timeout

**The Problem**

Initial attempts to load FDL1 used address `0x65000000` (from documentation), which caused consistent timeout errors.

**The Solution**

Through trial and error, `0x65000800` was found to be the correct FDL1 load address for the P671L. This produced: 'BSL_REP_VER: Spreadtrum Boot Block version 1.1' — confirming FDL1 loaded successfully.

### Challenge 6 — LIBUSB_ERROR_BUSY

**The Problem**

When the `1782:4d00` BROM device appeared briefly, spd_dump failed with `LIBUSB_ERROR_BUSY`. The device was detected for a fraction of a second then disappeared.

**The Solution**

A `watch -n 1 lsusb` command was running in another terminal, constantly polling the USB bus and holding the device. Killing the watch command and starting spd_dump BEFORE entering BROM mode solved this completely.

### Challenge 7 — BROM Mode Not Triggering

**The Problem**

Multiple attempts at Vol Down + USB while off did not produce the `1782:4d00` BROM USB ID. Various methods tried included pressing power + volume combinations, using recovery modes, and ADB reboot commands.

**The Solution**

The exact method that works for the P671L: start spd_dump first, power phone completely off, wait 5-10 seconds, then hold Vol Down and plug USB simultaneously. Timing matters — the phone must be fully powered off before attempting BROM entry.

### Challenge 8 — FDL2 'Incompatible Partition' Warning

**The Problem**

Every BROM session showed 'FDL2: incompatible partition' followed by 'EXEC FDL2' and 'usb_recv failed: LIBUSB_ERROR_TIMEOUT' in the logs. This looked alarming.

**The Solution**

This is normal and expected behavior for UFS devices with `fdl2-dl.bin`. The FDL2 still loads and executes correctly despite this warning. The subsequent 'Reading Partition List' completing at 100% confirms FDL2 is working. These messages can be safely ignored.

## 6. Complete Step-by-Step Execution

### STEP 1 — Back Up Critical Partitions (splloader + uboot)

> ⚠ This step erases splloader from the phone, making it temporarily unbootable. This is EXPECTED. Do not panic.

Ensure battery is at least 80% before starting. Start this command, then enter BROM mode:

```bash
sudo ./spd_dump --wait 300 \
  loadexec custom_exec_no_verify_65015f08.bin \
  fdl fdl1-dl.bin 0x65000800 \
  fdl fdl2-dl.bin 0x9efffe00 \
  exec \
  read_part splloader 0 0 splloader.bin \
  read_part uboot 0 0 uboot.bin \
  erase_part splloader \
  reset
```

✅ Expected result: `splloader.bin` (256KB) and `uboot.bin` (3MB) saved. Phone will not boot after this — that is correct.

> ⚠ KEEP `splloader.bin` and `uboot.bin` safe. These are your recovery backups. Never delete them.

### STEP 2 — Generate the Unlock Payload

This step runs entirely on the PC — no phone needed:

```bash
./gen_spl-unlock splloader.bin 0xfd28
```

Verify the output file was created:

```bash
ls -lh spl-unlock.bin
```

✅ Expected: `spl-unlock.bin` (~64KB) created. The tool outputs `0xfd68` — this is normal.

### STEP 3 — Flash Modified uboot (fdl2-cboot.bin)

This replaces the uboot partition with a modified version that disables write verification, enabling the unlock payload to work. Start command then enter BROM:

```bash
sudo ./spd_dump --wait 300 \
  loadexec custom_exec_no_verify_65015f08.bin \
  fdl fdl1-dl.bin 0x65000800 \
  fdl fdl2-dl.bin 0x9efffe00 \
  exec \
  w uboot fdl2-cboot.bin \
  reset
```

✅ Expected: 'Write Part Done: uboot_a' with `0xfd2e8` bytes written.

### STEP 4 — Send the Unlock Payload

This is the actual unlock step. The payload runs and writes unlock data to miscdata. Enter BROM after starting:

```bash
sudo ./spd_dump --wait 300 \
  loadexec custom_exec_no_verify_65015f08.bin \
  fdl spl-unlock.bin 0x65000800
```

The device will disconnect with USB errors after the payload executes — this is the payload running and the device resetting. It is expected behavior.

### STEP 5 — Verify the Unlock

Read 64 bytes from miscdata offset `0x2000` to confirm unlock status:

```bash
sudo ./spd_dump --wait 300 \
  loadexec custom_exec_no_verify_65015f08.bin \
  fdl fdl1-dl.bin 0x65000800 \
  fdl fdl2-dl.bin 0x9efffe00 \
  exec \
  verbose 2 read_part miscdata 8192 64 m.bin \
  reset
```

Then inspect the file:

```bash
xxd m.bin
```

- ✅ **UNLOCKED:** File contains non-zero hash/key data (64 bytes of random-looking data)
- ⚠ **STILL LOCKED:** File contains all 00 bytes — repeat Step 4

### STEP 6 — Restore splloader and uboot

This makes the phone bootable again. Start command then enter BROM:

```bash
sudo ./spd_dump --wait 300 \
  loadexec custom_exec_no_verify_65015f08.bin \
  fdl fdl1-dl.bin 0x65000800 \
  fdl fdl2-dl.bin 0x9efffe00 \
  exec \
  w splloader splloader.bin \
  w uboot uboot.bin \
  reset
```

✅ Expected: Both partitions written successfully. Phone will reboot.

> ⚠ The phone will boot into Android Recovery and prompt a FACTORY RESET. This is normal and expected after bootloader unlock. Accept it. Back up your data beforehand.

### STEP 7 — Verify Unlock via ADB

After the phone boots and you complete setup:

```bash
adb shell getprop ro.boot.vbmeta.device_state
```

Expected: `unlocked`

```bash
adb shell getprop ro.boot.flash.locked
```

Expected: `0`

✅ Both returning the expected values confirms the bootloader is fully unlocked!

## 7. Rooting with Magisk (After Unlock)

With the bootloader unlocked, rooting with Magisk is straightforward. The P671L runs Android 14, which uses `init_boot.img` (NOT `boot.img`) for Magisk patching.

1. Download the latest Magisk APK from `github.com/topjohnwu/Magisk/releases`
2. Install Magisk on the phone: `adb install magisk.apk`
3. Push init_boot.img to the phone:
   ```bash
   adb push ~/path/to/init_boot.img /sdcard/
   ```
4. Open Magisk app > Install > Select and Patch a File > choose `init_boot.img`
5. Pull the patched image back to PC:
   ```bash
   adb pull /sdcard/Download/magisk_patched_*.img ~/
   ```
6. Reboot to bootloader and flash:
   ```bash
   adb reboot bootloader
   fastboot flash init_boot ~/magisk_patched_*.img
   fastboot reboot
   ```
7. Verify root:
   ```bash
   adb shell su -c "id"
   ```
   Expected: `uid=0(root)`

### How to Unroot

**Option 1 (easiest):** Open Magisk app > Settings icon > Uninstall Magisk > Restore Images. Phone reboots fully unrooted.

**Option 2 (fastboot):** Flash original init_boot.img directly:

```bash
adb reboot bootloader
fastboot flash init_boot ~/path/to/init_boot.img
fastboot reboot
```

## 8. Recovery Procedures

Because BROM mode is hardwired into the Unisoc chipset and cannot be erased, the device is ALWAYS recoverable as long as you can enter BROM mode. This is a fundamental safety net.

### Phone Won't Boot (splloader erased)

Enter BROM mode and run:

```bash
sudo ./spd_dump --wait 300 \
  loadexec custom_exec_no_verify_65015f08.bin \
  fdl fdl1-dl.bin 0x65000800 \
  fdl fdl2-dl.bin 0x9efffe00 \
  exec \
  w splloader splloader.bin \
  w uboot uboot.bin \
  reset
```

### Full Stock ROM Restore (Worst Case)

If all else fails, reflash the complete stock firmware via BROM:

```bash
sudo ./spd_dump --wait 300 \
  loadexec custom_exec_no_verify_65015f08.bin \
  fdl fdl1-dl.bin 0x65000800 \
  fdl fdl2-dl.bin 0x9efffe00 \
  exec \
  w splloader ~/Music/itel-P671L-16/outdir/u-boot-spl-16k-ufs-sign.bin \
  w uboot ~/Music/itel-P671L-16/outdir/lk-fdl2-sign.bin \
  w boot ~/Music/itel-P671L-16/outdir/boot.img \
  w init_boot ~/Music/itel-P671L-16/outdir/init_boot.img \
  reset
```

## 9. Critical Warnings Summary

- ⚠ Never use eMMC FDL files (`u-boot-spl-16k-emmc-sign.bin`) on this UFS device.
- ⚠ Never use `fdl1-sign.bin` or `lk-fdl2-sign.bin` as spd_dump FDL loaders — use `fdl1-dl.bin` and `fdl2-dl.bin` only.
- ⚠ Never run `watch -n 1 lsusb` while spd_dump is running — causes `LIBUSB_ERROR_BUSY`.
- ⚠ Always start spd_dump command BEFORE entering BROM mode.
- ⚠ Never delete `splloader.bin` and `uboot.bin` backups — they are your recovery lifeline.
- ⚠ Use `init_boot.img` for Magisk on Android 14 — NOT `boot.img`.
- ⚠ Ensure battery is at least 80% before any BROM operations.
- ⚠ A factory reset WILL happen on first boot after unlock — back up your data first.
- ⚠ exec_addr for P671L is `0x65015f08`, NOT `0x65015f48` (which is the S23 value).
- ⚠ FDL1 address is `0x65000800`, NOT `0x65000000` (causes timeout).

## 10. Conclusion

The itel P65 (P671L) bootloader was successfully unlocked using CVE-2022-38694, despite the device not being officially listed in the exploit's support matrix. The key insight is that the UMS9230 universal UFS entry in the exploit's device list covers this chipset.

The process took considerable research and trial-and-error, particularly around identifying the correct FDL files, finding the right exec_addr (`0x65015f08` vs `0x65015f48`), and the correct FDL1 load address (`0x65000800` vs `0x65000000`). These device-specific parameters are now documented here for anyone with the same device.

Once unlocked, the device supports Magisk rooting, custom GSI flashing via fastboot or DSU, and full BROM-based recovery — making it a fully open device for further experimentation.


Guide by Caleb | April 2026 | itel P65 (P671L) CVE-2022-38694 Bootloader Unlock
