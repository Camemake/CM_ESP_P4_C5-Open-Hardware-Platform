# CM_ESP_P4_C5 Open Hardware Platform

Open hardware development kit for edge vision, HMI, control, and connectivity.

This platform combines:
- A high-performance ESP32-P4 SOM (CM_P4-A1-N16R32)
- A dual-band Wi-Fi 6 ESP32-C5 module (CM_ESP32-C5-WROOM-1-N8R8)
- A stable camera/display carrier board with Ethernet, USB, audio, SD, and expansion
- A standardized Camemake camera module pinout that repeats across development kits

Everything in this repo is published so you can build your own product.  
You can also buy production-grade modules directly.

---

## 1. Key points

- Open hardware dev kit: CM_ESP_P4_C5
- Main compute: ESP32-P4 SOM with dual-core 32-bit RISC-V up to 360 MHz, 16 MB Flash, 32 MB PSRAM
- Connectivity module: ESP32-C5 with dual-band Wi-Fi 6 (2.4/5 GHz), Bluetooth 5 LE, Thread / Zigbee (802.15.4), 8 MB Flash, 8 MB PSRAM
- Camera pipeline: MIPI CSI and DVP/SPI camera support, shared Camemake camera connector pinout
- Display pipeline: MIPI DSI and parallel display connector
- Networking: RMII Ethernet PHY, USB 2.0 HS/FS OTG, SD card
- Audio path: I²S codec and amplifier hooks
- Industrial temperature range hardware
- Full CAD, firmware, and manufacturing data provided

This platform is both:
1. A reference design you can copy.
2. A production-ready module ecosystem you can buy.

---

## 2. Block diagram (functional roles)

**CM_P4-A1-N16R32 (ESP32-P4 SOM)**  
- Dual-core RISC-V application processor up to 360 MHz  
- Low-power controller for always-on wake and housekeeping  
- 16 MB Flash + 32 MB PSRAM on-module  
- High-speed multimedia engines (ISP, JPEG codec, H.264 encoder, pixel pipeline)  
- Interfaces broken out on the SOM:
  - MIPI CSI-2 camera
  - MIPI DSI display
  - Parallel camera / parallel RGB display
  - USB 2.0 OTG HS/FS
  - RMII Ethernet MAC
  - CAN / TWAI
  - I²S audio
  - I²C / I3C / SPI / UART / SDIO / GPIO / ADC / touch

**CM_ESP32-C5-WROOM-1-N8R8 (ESP32-C5 module)**  
- Single-core 32-bit RISC-V up to 240 MHz  
- Dual-band Wi-Fi 6 (2.4 GHz and 5 GHz)  
- Bluetooth 5 LE  
- Thread / Zigbee via 802.15.4  
- 8 MB Flash + 8 MB PSRAM  
- Used as a wireless / network / application coprocessor

**Carrier board (CM_ESP_P4_C5 baseboard)**  
- High-speed camera connector  
- High-speed display connector  
- Gigabit-capable PHY footprint for Ethernet RMII (10/100 mode)  
- USB connectors (data + power + debug)  
- SD card slot  
- I²S audio codec + amplifier drive path  
- User buttons, status LED, accessible UART0, USB Serial/JTAG  
- Power regulation: 5 V in → 3.3 V rails, local LDO rails for camera/display bias and logic

**ESP32-P4NRW32 (bare MCU option)**  
- ESP32-P4 silicon with integrated 32 MB PSRAM in-package  
- Dual-core high-performance domain + always-on low-power domain  
- Same multimedia and interface set as exposed on the SOM  
- Sold standalone for teams who want to design their own SOM instead of buying CM_P4-A1-N16R32

---

## 3. Camemake camera module ecosystem

The CM_ESP_P4_C5 dev kit is camera-first.

- The camera connector is defined and frozen.  
- The same pinout is reused across Camemake development kits.  
- This lets you:
  - Swap camera modules without rewiring
  - Reuse camera firmware, drivers, and I2C control code
  - Scale from prototype to product with minimal PCB change

Supported camera interface modes:
- MIPI CSI-2 (for higher bandwidth sensors)
- DVP / parallel 8-bit and SPI camera modules (for lower cost sensors with onboard compression/encoder)

This repo will include:
- Camera connector pinout
- Power rails for 1.2 V / 1.8 V / 2.8 V image sensor domains
- Example init sequences (I2C/TWI)
- Capture path demo (sensor → ISP/H.264 → stream/store)

---

## 4. Display and HMI path

The baseboard exposes:
- MIPI DSI high-speed lane pair for modern LCD panels
- Parallel/RGB interface for lower-cost LCDs
- Touch panel interrupt and reset lines
- Backlight enable and brightness control
- Orientation (UPDN / SHLR) control

Firmware examples will include:
- Camera preview to display
- Simple UI / menu render
- Touch reading and event handling

This makes CM_ESP_P4_C5 usable as a human-machine interface panel or smart control head.

---

## 5. Networking and I/O

### Ethernet
- RMII interface to external PHY
- RJ45 with magnetics
- PHY reset, MDC/MDIO, activity LEDs
- 10/100 operation for industrial control and wired gateways

### USB
- High-speed USB 2.0 OTG from ESP32-P4 SOM
- Secondary USB port wired to CP2102N bridge for debug UART, auto-program, boot control
- USB power distribution and overcurrent switching

### Wireless
- Handled by ESP32-C5 module
- Dual-band Wi-Fi 6
- BLE 5 LE
- Thread / Zigbee for Matter-class devices

### Storage
- SD card slot (SDIO)
- 16 MB Flash + 32 MB PSRAM on SOM for app/runtime data
- 8 MB Flash + 8 MB PSRAM on ESP32-C5 module

### Audio
- I²S codec path with mic in and speaker out
- Power amp enable line
- Ready for voice input, alerts, UI sounds

---

## 6. Hardware deliverables in this repo

You get full manufacturing data.

- Schematics (PDF and source)
- PCB layout files
- IPC-class PCB stackup and impedance spec
- BOM with part numbers
- Mechanical files (STEP, DXF)
- Pinout drawings for:
  - CM_P4-A1-N16R32 SOM
  - CM_ESP32-C5-WROOM-1-N8R8 module
  - Camera connector
  - Display connector
  - Expansion headers
- Power tree and rail notes
- Reflow guidance

This is meant to let you spin your own carrier, not just blink LEDs.

---

## 7. Live hardware view (3D board)

Below is an embedded Altium 365 viewer for the CM_ESP_P4_C5 board.

> Note: GitHub strips iframes in README rendering.  
> Teams cloning this repo for internal docs or static hosting can keep the embed.  
> On github.com you will just see the HTML below as text.

```html
<iframe src="https://personal-viewer.365.altium.com/client/index.html?feature=embed&source=41859615-3556-46FD-834A-538307991D47&activeView=3D"
        width="1280"
        height="720"
        style="overflow:hidden;border:none;width:100%;height:720px;"
        scrolling="no"
        allowfullscreen="true"
        onload="window.top.scrollTo(0,0);">
</iframe>
