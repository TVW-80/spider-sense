# Spider Sense

> A Flipper Zero surveillance-device field sensor — part of the **Anansi** project.

**[→ Open the Operation Debrief](https://tvw-80.github.io/spider-sense/)**

Spider Sense turns a Flipper Zero and a cheap ESP32 Wi-Fi board into a pocket
detector for surveillance hardware — Flock ALPR cameras, Axon gear, generic IP
cameras, Ring, Wi-Fi deauthers, evil-twin access points and pentest kit — and
feeds what it finds into **Anansi**, the regional intelligence globe, as a
mappable layer.

This repository is the **project debrief / showcase** (a static site served via
GitHub Pages). It covers the three parts of the build:

1. **?xOS** — a custom, ghost-themed Flipper Zero firmware to host it (built on
   RogueMaster first, then rebuilt on the official firmware).
2. **Spider Sense** — the ESP32 sensor and the companion Flipper app. The meat
   of the project.
3. **Anansi integration** — the live map layer that turns field detections into
   pins on the globe, tying the two projects back together.

## How the pieces connect

```
ESP32-S2 Wi-Fi board ──UART 115200──▶ Flipper Zero ──USB──▶ PC / Anansi globe
  Spider Sense sensor                  Spider Sense app       flipperDetections layer
  (SQW,* text lines)                   (?xOS firmware)         (GeoJSON + phone GPS/GPX)
```

The sensor emits plain `SQW,*` text lines; the Flipper app shows them; the
Anansi data layer maps them. That serial protocol is the seam between the two
projects.

## Credits

Spider Sense stands on other people's work:

- **Detection engine — [SquachWatch-CYD](https://github.com/skizzophrenic/SquachWatch-CYD) by skizzophrenic.**
  The signatures, the OUI/SSID/behavior rules, and the whole concept of a
  surveillance-device detector are theirs. Spider Sense re-states its Wi-Fi
  detection core as a headless serial sensor and adds the Flipper app.
- **[RogueMaster](https://github.com/RogueMaster/flipperzero-firmware-wPlugins) and the Flipper custom-firmware community.**
  The firmware ?xOS was first grown on, and the bundled-app ecosystem that came
  with it.
- **[Flipper Devices](https://github.com/flipperdevices/flipperzero-firmware).**
  The Flipper Zero, the official firmware the final ?xOS build is based on, and
  the app SDK.
- **[God's Eye View](https://github.com/bilawalsidhu/gods-eye-view) by Bilawal Sidhu.**
  The CesiumJS globe platform Anansi is built on — see the
  [Operation Anansi debrief](https://tvw-80.github.io/Ananasi-intel/).

## Methodology

Claude (Anthropic) was used throughout as a coding, debugging and design
assistant. The hardware decisions, the real-device testing, and every commit
were driven directly — Claude functioned as a pair-programming and research
tool, not an autonomous builder.
