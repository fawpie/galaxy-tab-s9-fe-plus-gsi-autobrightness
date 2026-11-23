# Galaxy Tab S9 FE+ GSI Auto-Brightness Fix

A Magisk module that enables Adaptive brightness on the Samsung Galaxy Tab S9 FE+ Wi-Fi (SM-X610) running a compatible GSI. It applies an Android framework resource overlay with a brightness curve tuned for this tablet.

## Tested setup

| Component | Tested configuration |
| --- | --- |
| Tablet | Galaxy Tab S9 FE+ Wi-Fi (SM-X610, `gts9fepwifi`) |
| Android | Android 15 |
| GSI | [MisterZtr's LineageOS 22.2 build from January 5, 2026](https://github.com/MisterZtr/LineageOS_gsi/releases/tag/v2026.01.05-lineage22.2) |
| GSI image | `LineageOS-22.2-20260105-GAPPS-EROFS-GSI.img` |
| Root | Magisk 31.1 |

The ambient light sensor reported live lux readings on this setup. The overlay enables the Adaptive brightness setting and provides the framework with the corresponding backlight values. It targets the `gts9fepwifi` vendor device identifier. Verified compatibility covers the build above.

## Installation

1. Download the Magisk ZIP from [Releases](https://github.com/fawpie/galaxy-tab-s9-fe-plus-gsi-autobrightness/releases/latest).
2. In Magisk, open **Modules → Install from storage** and select the ZIP.
3. Reboot and turn on **Adaptive brightness** under **Settings → Display**.

To remove the fix, remove the module in Magisk and reboot.

## Brightness calibration

The curve is an original calibration developed through on-device testing, independently of the stock ROM. We checked live ambient-light readings while changing the light around the tablet and adjusted the backlight response, especially in a dark room. The configured value at **0 lux** is **1**, the lowest backlight step in this curve.

| Ambient light (lux) | Framework backlight value (0–255) |
| ---: | ---: |
| 0 | 1 |
| 3 | 24 |
| 12 | 31 |
| 40 | 45 |
| 100 | 66 |
| 250 | 93 |
| 600 | 120 |
| 1,500 | 149 |
| 3,500 | 183 |
| 8,000 | 216 |
| 20,000 | 250 |

The [overlay source](overlay/) contains the device match, lux points, and backlight values. The release packages the signed overlay at `system/product/overlay/FawpieAdaptiveBrightness.apk`. Its resource table is stored uncompressed and verified with Android SDK `zipalign`.
