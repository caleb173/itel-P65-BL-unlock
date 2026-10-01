# itel P65 (P671L) — Complete Device Intelligence
**Compiled by Caleb | May 2026 | v2.0 — Derived from live device extraction**

---

## Device Identity

| Field | Value |
|-------|-------|
| Marketing Name | itel P65 |
| Model Number | P671L |
| Internal Model | itel P671L |
| Manufacturer | ITEL (Transsion Holdings) |
| Brand | Itel |
| Board ID | itel-P671L |
| Hardware ID | ums9230_P671L |
| Product Name | P671L-OP |
| Build Fingerprint | Itel/P671L-OP/itel-P671L:14/UP1A.231005.007/260112V2552:user/release-keys |
| Build Description | ums9230_P671L-user 14 UP1A.231005.007 1542 release-keys |
| Build Host | srv99-12598 |
| Build User | buildsrv-ci |
| OTA Build ID | P671L-SK677ABCDGHJKAaAbAcAe-U-OP-260112V2552 |
| Target Market | Africa |
| Camera Country Tuning | NG (dark skin optimised) |
| GDPR Version | 20210705V3 |
| Facebook Partner ID | transsion:4edab295-658e-4565-a2a8-bef997858d60 |
| Google Client ID | android-transsion |
| GMS Version | 14_202403 |
| Siblings | Tecno, Infinix (same parent — Transsion Holdings) |

---

## System on Chip (SoC)

| Field | Value |
|-------|-------|
| SoC Name | Unisoc T615 |
| SoC Revision | UMS9230-AC |
| SoC Model String | Spreadtrum UMS9230 1H10 |
| ro.hardware | ums9230_P671L |
| DT Compatible | sprd,ums9230 |
| Process Node | 12nm (TSMC) |
| Architecture | ARMv8-A (64-bit) |

### CPU

| Field | Value |
|-------|-------|
| Configuration | Octa-core |
| Efficiency Cluster | 6x ARM Cortex-A55 |
| Performance Cluster | 2x ARM Cortex-A75 |
| CPU Part (A55) | 0xd05, variant 0x2, revision 0 |
| CPU Part (A75) | 0xd0a, variant 0x3, revision 1 |
| CPU Implementer | 0x41 (ARM Ltd.) |
| BogoMIPS | 52.00 |
| Dalvik ISA Variant (arm) | cortex-a55 |
| Dalvik ISA Variant (arm64) | cortex-a75 |
| CPU Features | fp asimd evtstrm aes pmull sha1 sha2 crc32 atomics fphp asimdhp cpuid asimdrdm lrcpc dcpop asimddp |
| Hardware Crypto | AES, PMULL, SHA1, SHA2 |
| Page Size Max | 65536 (64KB) |
| ABI List | arm64-v8a, armeabi-v7a, armeabi |

### GPU

| Field | Value |
|-------|-------|
| GPU | ARM Mali-G57 MC1 |
| Architecture | Valhall (4th gen) |
| Revision | r0p1 |
| GPU ID | 0x9091 |
| GPU Address | 0x23100000 |
| ro.hardware.egl | mali |
| OpenGL ES | 3.2 (ro.opengles.version = 196610) |
| Vulkan | Enabled (ro.hwui.use_vulkan = true) |
| Vulkan Driver | vulkan.ums9230.so |
| Render Engine | skiaglthreaded |
| Open Driver | panfrost (mainline Linux compatible) |
| AI Frameworks | ARM NN, MNN+OpenCL (libMNN_CL.so), Unisoc AI Engine |
| GPU Profiler | Supported |

### Other SoC Components

| Component | Value |
|-----------|-------|
| DSP | Unisoc VDSP |
| Modem | Integrated Unisoc qogirl6_modem |
| Modem Firmware | 4G_MODEM_22B_W24.26.3_P6 |
| Connectivity Chip | Unisoc WCN (WiFi+BT+GPS) @ 0x87000000 |
| PMIC | Unisoc SC2730 |
| Video Codec | @ 0x32000000 |
| JPEG Codec | @ 0x36000000 |
| RNG | @ 0x201e0000 |
| Watchdog | @ 0x644e0000 |
| Thermal Controllers | @ 0x644b0000, 0x644d0000 |
| PWM | @ 0x643f0000 |
| eFuse | @ 0x643d0000 |

---

## Memory & Storage

| Field | Value |
|-------|-------|
| RAM | 4GB physical |
| RAM Base Address | 0x80000000 |
| Storage Type | UFS 2.2 |
| UFS Controller | 0x20200000 |
| UFS IRQ | GICv3 179 Level (2,624,580 total interrupts) |
| Flash Chip | YMTC C2G072 (confirmed via lsscsi) |
| Total Storage | 128GB |
| Userdata | ~113GB (sda75, dm-57) |
| Userdata FS | F2FS + inlinecrypt |
| System FS | EROFS (dm-10) |
| HPB | Disabled by Unisoc |
| Write Booster | Active |
| Swap File | 4096MB (persist.vendor.swapfile_size_mb) |
| Adoptable Storage | Supported |

### Block Device Map

| Block | Mount | Notes |
|-------|-------|-------|
| sda1 | /mnt/vendor | |
| sda46 | /, /vendor, /system, /odm, /product | super (EROFS) |
| sda47 | /cache | |
| sda48 | /blackbox | Crash logs (F2FS) |
| sda51 | /metadata | F2FS |
| sda70 | /tranfs | Transsion FS |
| sda75 | /data | F2FS + inlinecrypt (dm-57) |

### ZRAM

| Field | Value |
|-------|-------|
| Algorithm | lz4 (active); also: lzo, lzo-rle, zstd |
| Pool Size | 2.74GB |
| orig_data_size | 2.0GB |
| compr_data_size | 495MB |
| Compression Ratio | 4.14:1 |
| Swap Used | 1.9GB of 2.7GB |

### Dalvik Heap

| Field | Value |
|-------|-------|
| heapstartsize | 8MB |
| heapgrowthlimit | 192MB |
| heapsize | 512MB |
| heaptargetutilization | 0.6 |
| dex2oat Xms/Xmx | 64MB / 512MB |
| JIT | enabled |
| uffd GC | enabled |

---

## Kernel

| Field | Value |
|-------|-------|
| Version | Linux 5.15.180-android13-8 |
| Full String | 5.15.180-android13-8-g74cec266fd3c-ab1542 |
| Build Date | Thu Nov 20 06:42:10 UTC 2025 |
| Compiler | Android Clang 14.0.7 |
| Linker | LLD 14.0.7 |
| Architecture | arm64 |
| Preemption | PREEMPT |
| SMP | Yes (8 cores) |
| GKI Base | android13 |

### Kernel Memory Map (Key Regions)

| Address Range | Description |
|---------------|-------------|
| 0x80000000–0xb71fffff | System RAM (primary) |
| 0x80090000–0x82afffff | Kernel code |
| 0x82d80000–0x830cffff | Kernel data |
| 0x87000000–0x877fffff | WCN firmware (WiFi/BT/GPS) |
| 0x88f00000–0x8defffff | Audio DSP firmware |
| 0x9e000000–0x9e9e3fff | Display framebuffer |
| 0xb0000000–0xb71fffff | Secure Monitor + TEE |
| 0xfff80000–0xfffbffff | ramoops (kernel panic logs) |

### Key Kernel Config

```
CONFIG_SWAP=y                  CONFIG_ZRAM=m
CONFIG_ZRAM_WRITEBACK=y        CONFIG_ZRAM_DEDUP=y
CONFIG_UFS_SUPPORT=y           CONFIG_MEMCG=y
CONFIG_BPF_SYSCALL=y           CONFIG_BPF_EVENTS=y
CONFIG_KPROBE_EVENTS=y         CONFIG_UPROBE_EVENTS=y
CONFIG_CGROUPS=y               CONFIG_USB_GADGET=y
CONFIG_WLAN=y                  CONFIG_BT=y
CONFIG_BT_BREDR=y              CONFIG_BT_LE=y
CONFIG_CFG80211=m              CONFIG_NETFILTER=y
CONFIG_IPV6=y                  CONFIG_NET_IPVTI=y
CONFIG_SPRD_SOCID=m            CONFIG_SPRD_UID=m
CONFIG_PREEMPT=y               CONFIG_AUDIT=y
CONFIG_FTRACE=y                CONFIG_TRACING=y
CONFIG_SCHED_DEBUG=y           CONFIG_SCHEDSTATS=y
CONFIG_STACKTRACE=y            CONFIG_BUG_ON_DATA_CORRUPTION=y
CONFIG_CC_IS_CLANG=y           CONFIG_LD_IS_LLD=y
CONFIG_WERROR=y                CONFIG_KCOV=n
```

---

## Software & OS

| Field | Value |
|-------|-------|
| Android Version | 14 (API 34) |
| ROM | HiOS V14.0.0 / itelos14.0.0 |
| Build Type | user (ro.debuggable = 0) |
| Build Date | Mon Jan 12 12:08:07 CST 2026 |
| Build ID | UP1A.231005.007 |
| Incremental | 260112V2552 |
| Security Patch | 2026-02-01 |
| Mainline Version | 2024-09 |
| VINTF Target Level | 7 |
| Treble | Enabled |
| A/B Partitions | Yes — Active: Slot A |
| First API Level | 34 |
| Zygote | zygote64_32 |
| Render Engine | skiaglthreaded |
| Crypto | File-based encryption |
| RIL | android reference-ril 1.0 |
| Netflix BSP | U9230-34887-1 |
| VoLTE | Enabled (both SIMs) |
| VoNR | Enabled (both SIMs) |
| DSDS | Dual SIM Dual Standby |
| Modem Mode | TL_LF_W_G (both SIMs) |
| thub core | 34.1.2.1 |
| USB State | adb |
| USB Controller | musb-hdrc.1.auto |

### Transsion Proprietary HALs (VINTF)

| HAL | Interface |
|-----|-----------|
| vendor.transsion.hardware.trandatacenter@1.0 | ITranDataCenter/default |
| vendor.transsion.hardware.tranlog@1.0 | ITranLog/default |
| vendor.transsion.hardware.tranlogconfig@1.0 | ITranLogConfig/default |
| vendor.transsion.performance.sched@1.0 | ITransSched/default |

---

## Display

| Field | Value |
|-------|-------|
| Type | LCD (punch-hole) |
| LCD Chip | Synaptics TD4160 |
| Panel ID | lcd_td4160_hdp_dsi_vdo_txd_inx_p671l |
| Panel Vendors | TXD + Innolux (primary); HKC (variant) |
| Resolution | 720 × 1600 (HD+) |
| DPI | 320 |
| Aspect Ratio | 20:9 |
| Interface | MIPI DSI 4-lane |
| DRM Node | /dev/dri/card0 |
| LCD Base | 0x9e000000 |
| DTBO Index | 18 |
| HDR | HDR_CONVERSION_SYSTEM |
| PQ | Enabled (CABC + DCI) |

### Refresh Rate Timings

| Field | timing0 | timing1 | timing2 |
|-------|---------|---------|---------|
| Rate | **60.3Hz** | 90.0Hz (internal) | **120.3Hz** |
| h-total | 1200px | 876px | 880px |
| v-total | 2654px | 2434px | 1814px |

---

## Audio

| Field | Value |
|-------|-------|
| Audio Codec | Unisoc SC2730 @ 0x56750000 |
| VBC | @ 0x56480000 |
| MCDT | @ 0x56490000 |
| PDM DMIC | @ 0x56401000 |
| Audio HAL | android.hardware.audio@7.1 |
| Speaker Amp 1 | Awinic AW series |
| Speaker Amp 2 | Fourier Semiconductor FSM-128 |
| BT Audio | audio.bluetooth.ums9230.so |
| FM Radio | Yes |
| DTS Audio | Supported |
| EIS Recording | Enabled |
| VAD | Voice Activity Detection supported |

---

## Camera

| Field | Value |
|-------|-------|
| Rear Sensor | Samsung S5KJN1 — 50MP (s5kjn1_1906) |
| Front Sensor | GalaxyCore GC08A8 — 8MP (gc08a8_1890) |
| Rear Bus | I2C 0-0020 |
| Front Bus | I2C 1-005a |
| Camera HAL | android.hardware.camera.provider@2.4-impl-sprd.so |
| Logical IDs | 18 total |
| ZSL | Disabled |
| EIS | Enabled |
| MFNR Version | 3 |
| HDR Version | 4 |
| Sensitivity Range | 50–9000 (both sensors) |
| Flash LED 1 | Awinic AW36515 (I2C 5-0064) |
| Flash LED 2 | OCP81375 (I2C 5-0065) |
| Google Lens | com.transsion.camera + com.gallery20 |
| Portrait | Enabled (front + back) |
| Night Pro | Enabled |
| Multi-camera | Enabled |

---

## Sensors

### Physical Sensors

| Sensor | Chip | Notes |
|--------|------|-------|
| Accel + Gyro | ST LSM6DSOETR3 | 3.12–200Hz, mainline IIO |
| Magnetometer | MEMSIC MC5603NJL | 3.12–200Hz, mainline IIO |
| Light + Proximity | Sensortek STK3335-X | mainline IIO |
| ToF | ST VL53L0X (I2C 4-0052) | 0–2000mm |

### Touchscreen

| Field | Value |
|-------|-------|
| Driver | OmniVision TCM |
| Interface | SPI spi3.0 @ 0x20150000 |
| IRQ | gpio 641000a0 pin 16, Level |

### Fingerprint

| Field | Value |
|-------|-------|
| Chip | Silead (side-mounted) |
| IRQ | gpio 641000a0 pin 29, Edge |
| HAL | fingerprint.silead.default.so |

### Input Devices

| Node | Device |
|------|--------|
| event0 | gpio-keys (Power, Vol Up/Down, Smart Key) |
| event1 | sc27xx:vibrator |
| event2 | sc2730 Headset Jack |
| event3 | sc2730 Headset KB |
| event4 | omnivision_tcm_touch |
| event5 | fp-keys |

### Custom Unisoc Sensors
```
com.spreadtrum.shake / tap / flip / pocket_mode / hand_up
```

---

## Connectivity

| Field | Value |
|-------|-------|
| Cellular | 4G LTE (VoLTE + VoNR) |
| Data Interface | seth_lte0 |
| WiFi Interface | wlan0 |
| WiFi HAL | libwifi-hal-unisoc.so |
| Bluetooth | BR/EDR + BLE (android.hardware.bluetooth@1.1) |
| BT Class | 90,2,12 |
| BT Profiles | A2DP, AVRCP, ASHA, BAS, GATT, HFP, HID, MAP, OPP, PAN, PBAP |
| GPS | Integrated WCN + gps.default.so |
| NFC | Samsung sec-nfc (I2C 2-0027) |
| USB | USB 2.0, USB-C |
| USB Controller | musb-hdrc.1.auto @ 0x64900000 |
| FM Radio | Yes |

---

## I2C Bus Map

| Bus | Address | Devices |
|-----|---------|---------|
| i2c-0 | 0x200d0000 | 0-0020 rear camera |
| i2c-1 | 0x200e0000 | 1-0020 rear cam2, 1-005a front cam |
| i2c-2 | 0x200f0000 | 2-0027 NFC, 2-0034 fs15xx, 2-0058 speaker amp |
| i2c-3 | 0x20100000 | (empty) |
| i2c-4 | 0x20110000 | 4-0052 ToF (VL53L0X), 4-006b charger |
| i2c-5 | 0x20210000 | 5-0064 flash LED 1, 5-0065 flash LED 2 |
| i2c-6 | 0x20220000 | (empty) |
| i2c-7 | 0x641a0000 | HW I2C (empty) |

---

## Biometrics & Security

| Field | Value |
|-------|-------|
| Fingerprint | Silead (side-mounted) |
| Face Unlock | Yes — face.default.so |
| Face Version | 2 |
| TEE | Trusty TEE @ 0xb0040000 |
| Secure Monitor | SML @ 0xb0000000 |
| Widevine Level | L1 |
| Widevine Version | 17.0.1@035 |
| OEM Crypto API | 17 |
| Max DRM Sessions | 50 |
| SOTER | Yes |
| IFAA | Yes |
| Voice Trigger | Hardware IRQ GPIO (always-on hotword) |
| OEM Unlock | Supported |
| FRP | /dev/block/by-name/persist |

---

## Battery

| Field | Value |
|-------|-------|
| Capacity | 4950mAh |
| Charger IC | Southchip SC8950X (I2C 4-006b) |
| Quick Charge | Yes |
| AI Charging | Yes |
| Bypass Charging | Yes (gaming) |
| TypeC | Yes |
| Wireless | No |

---

## Hardware Chips Summary

| Component | Chip |
|-----------|------|
| SoC | Unisoc UMS9230-AC (T615) |
| PMIC | Unisoc SC2730 |
| LCD Controller | Synaptics TD4160 |
| Panel | TXD + Innolux |
| GPU | ARM Mali-G57 MC1 Valhall r0p1 |
| Flash Storage | YMTC C2G072 UFS 2.2 |
| Audio Codec | Unisoc SC2730 |
| Speaker Amp 1 | Awinic AW series |
| Speaker Amp 2 | Fourier Semiconductor FSM-128 |
| Fingerprint | Silead |
| Accel + Gyro | ST LSM6DSOETR3 |
| Magnetometer | MEMSIC MC5603NJL |
| Light + Proximity | Sensortek STK3335-X |
| ToF | ST VL53L0X |
| Touchscreen | OmniVision TCM |
| Rear Camera | Samsung S5KJN1 (50MP) |
| Front Camera | GalaxyCore GC08A8 (8MP) |
| Connectivity | Unisoc WCN |
| NFC | Samsung sec-nfc |
| Charger IC | Southchip SC8950X |
| Flash LED 1 | Awinic AW36515 |
| Flash LED 2 | OCP81375 |

---

## Partition Table

| Name | Size | Block | Notes |
|------|------|-------|-------|
| splloader | 256KB | — | **NEVER DELETE** |
| prodnv | 64MB | sda1 | |
| trustos_a/b | 6MB each | — | Trusty OS |
| sml_a/b | 1MB each | — | Secure Monitor |
| uboot_a/b | 3MB each | — | **NEVER DELETE** |
| uboot_log | 16MB | — | |
| logo | 8MB | — | Boot logo |
| l_modem_a/b | 25MB each | — | Modem firmware |
| l_gdsp_a/b | 10MB each | — | GPS DSP |
| l_ldsp_a/b | 20MB each | — | LTE DSP |
| l_agdsp_a/b | 6MB each | — | Audio/GPS DSP |
| boot_a/b | 64MB each | — | Boot image |
| vendor_boot_a/b | 100MB each | — | |
| init_boot_a/b | 8MB each | — | **Magisk @ init_boot_a** |
| dtb_a/b | 8MB each | — | |
| dtbo_a/b | 8MB each | — | Index 18 active |
| super | 7200MB | sda46 | system/vendor/product |
| cache | 64MB | sda47 | |
| blackbox | 500MB | sda48 | Crash logs |
| metadata | 64MB | sda51 | |
| tranfs | 300MB | sda70 | Transsion FS |
| tdfs | 56MB | — | Transsion data FS |
| transec | 56MB | — | Transsion security |
| userdata | 113057MB | sda75 | ~113GB |

---

## Security & Root State

| Field | Value |
|-------|-------|
| Bootloader | UNLOCKED via CVE-2022-38694 |
| Unlock Date | April 25, 2026 |
| Verified Boot | orange |
| Root | Magisk 30.7 on init_boot_a |
| Zygisk | Enabled |
| LSPosed | 2.0 (3021) |
| BROM USB ID | 1782:4d00 |
| exec_addr | 0x65015f08 (P671L specific) |
| FDL1 addr | 0x65000800 |
| FDL2 addr | 0x9efffe00 |
| unlock_offset | 0xfd28 |

---


## Vendor HAL SHA256 Hashes

| Library | SHA256 |
|---------|--------|
| android.hardware.audio.effect@7.0-impl.so | 2fd6a0ddc5c8981261f6e8cc63c2d7b868c105c28653bf2d366cdb9111e837ac |
| android.hardware.audio@7.1-impl.so | 5a00857e407a2147314a7e0f3a525b67c917165c1138946b06cf47321ff5b2dd |
| android.hardware.boot@1.0-impl-1.2.so | 80c27b07946a37795f3182d41dfa00f890523cf6a2d7d248707da3cee5637c96 |
| android.hardware.broadcastradio@1.0-impl.so | 8bf3ee8d8da24f5cee15b6978f270afd00c1912ba3bc6a7ce355b0980b615805 |
| android.hardware.camera.provider@2.4-impl-sprd.so | 04f794e1c5f5caeb646598a24a0d7921d551d6db9a66873c20fa5799c4a547f5 |
| android.hardware.graphics.allocator@4.0-impl-arm.so | 3b5fa6998743d9e001f649a254d7bdd73316afcc5618136353267960bf710b81 |
| android.hardware.graphics.mapper@4.0-impl-arm.so | 3d1666cf3f0a04ac8a56b914eccbe8ad93eab76dede57b085a1e93e13452923f |
| android.hardware.renderscript@1.0-impl.so | f2066c629b370f7edd0340fbbd5d7ab8ce63990470c2cc561b511c21b0d59282 |
| audio.bluetooth.default.so | 8f2514275c382988b3e043c2fa029b317aca90b7d70a3f7655d6fd2a3f5daaf7 |
| audio.bluetooth.ums9230.so | 3a6263516e067857c3dac6596aea7467300a0b86ed29dca288a4f082481966b5 |
| audio.primary.default.so | ef2798b11b970b310b2ed25a1354a47bae2e2bc75f7107ed5ae6a2c8894c38e2 |
| audio.r_submix.default.so | 317a7694a1b6c2c24d46188afcdb43f658e40629dda46da2ced89ee88f7bb1ea |
| audio.usb.default.so | 164a4eeaa9ed50a6857feb83001cc16cca26faf4a1f377b32bf7bdd732445e64 |
| bootctrl.default.so | 6d972b459edd7c3e2089815ee4bac8513fb198aee7fc1699773e0fb11e77d708 |
| camera.unisoc.so | fc57c97a709103fc55515259ce62cdc62a2740d2236f40891126eb03f313acb8 |
| dpu.unisoc.so | 7f33b9141b293592c66458b0efa7038748ab349e363dcd9a994ad4b8becf4fa2 |
| enhance.unisoc.so | f726abbb69ba669b39167d79412335ad08585defc8ce1e5522f960270fd298ad |
| face.default.so | a99eedae3eba6c4dbbdaa8e78e98c041342d4db1101e9d5bcf0783a7aa41dfcd |
| fingerprint.silead.default.so | 8c7633f5204e2a78199883e2726d707cd769a135039a832d79b3ddd1b3a5360e |
| fpsensor_fingerprint.default.so | 9a92e8bd1db71ebc60ced62569f8ade073daa3058e18df6120fb4e297ca896df |
| gps.default.so | a421a486dd0903656b251be1bed8cff6742970a8dea02f89847cdec4a2441862 |
| gralloc.default.so | 3bf41a3a064df10c54b2f530a52d8c8c91e46bc2914afa130edaa519a3f77aef |
| gsp.unisoc.so | ad944f84bd65635511d40e0d558fc0ae965fb901f1fee31e0ec09b461df9c6d0 |
| hwcomposer.unisoc.so | 89d11c062224c801289814f10f3b1b49c223e621fadf563d35d95dbb927d8f90 |
| libawinic.audio.effect.skt3.so | 525a94a6477370c6b5266bfef6af9bfc1495860e00a4cc37ba3b9da586f24585 |
| libfsm_hal_128.so | b9e9c4577188e9298b209ac9793a423bcacd8cf858f3ef52d6107a8ee1ae858b |
| liblowi_wifihal.so | 8299c2ad4e31b3079878fc11d7c2ec81b5ac4bef3e72d6670971dec0a8f51b77 |
| libwifi-hal-unisoc.so | dd7a14bdacd1995fa1516b8764d54f75353399e8ea8bab4e16fa0f472b810c96 |
| local_time.default.so | 05455dbfa704ca13c8cb3881810462471e6e8f8db8cec9bf39788786c4f03e7f |
| power.default.so | 576d7e07fd74b25d0ed37cf74daa1ebace3a9904b482f9bc2e2fb48986f9611c |
| sensors.unisoc.so | 7380ea0de3db0d945f0c89e4c03d4d83ec048b16d615e993aab7d88d0a894acd |
| thermal.default.so | 8990cc9e23a5d29ebb3ed101d01957fd6bbd88ba3efd798503010159fd9b8856 |
| unisoc.bootctrl.so | eaba3e65b2f0e79efbfb65b8c8eb7ffc123e1eb3fbaad13d7b391296d39b8276 |
| vendor.sprd.hardware.connmgr@1.0-impl.so | e566ec15e93f53af10ffe841ca624fab23b929857cb8cdd24003160bd4cf1311 |
| vendor.sprd.hardware.thermal@2.0-impl.so | 5ea82a27b4e9b64aaa8a97bd6952c526adb26a7766f1b66471f0b9b40b684538 |
| vendor.sprd.hardware.trusty-impl.so | 9dd75ab49fe5f6a9803cf4959ea394ea17f50d5f213640474a1bfbd26f68b43d |
| vibrator.default.so | 6547b5e42ccbab2ecf92f2f17fac28ae838f611d80bedba7a776f30a8c8bd50a |

---

*Compiled by Caleb | itel P65 (P671L) | May 2026 | v2.0*
*Should any consideration porting to other phone os, here is my 2 cents
*Source: live device extraction — getprop, /proc/iomem, /proc/interrupts, VINTF manifests, kernel config, Wireshark captures, Termux root shell*
*Camera confirmed: Samsung S5KJN1 50MP (rear), GalaxyCore GC08A8 8MP (front)*
*Storage confirmed: YMTC C2G072 UFS 2.2*
