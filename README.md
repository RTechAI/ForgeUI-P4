ForgeUI P4

Created by Scott Forster
Contact: forgeui.esp32@gmail.com

Production-ready LVGL v9 framework and ESP-IDF hardware baseline for the ESP32-P4.

ForgeUI P4 is a clean, modular embedded UI framework for developers building real ESP32-P4 products with LVGL and ESP-IDF.

Primary supported board:

Waveshare ESP32-P4-WIFI6-Touch-LCD-7B

ForgeUI P4 removes the painful low-level bring-up stage by providing a proven starting point for:

- ESP32-P4 display bring-up
- LVGL v9 UI development
- GT911 touch input
- ESP-Hosted WiFi using the onboard ESP32-C6
- DS3231 RTC support
- ES8311 audio output
- SD card storage
- modular embedded UI architecture
- product-ready screen structure


PROJECT STATUS

Current status:

RC1 public baseline

Current focus:

Clean public release, hardware-proven starter framework, theme examples, and reusable ESP32-P4 LVGL architecture.


SUPPORTED HARDWARE

Primary board:

Waveshare ESP32-P4-WIFI6-Touch-LCD-7B

Proven hardware:

- ESP32-P4 RISC-V MCU
- ESP32-C6 Hosted WiFi coprocessor
- EK79007 MIPI DSI display
- GT911 capacitive touch
- DS3231 RTC
- ES8311 audio codec
- SD card storage


SOFTWARE STACK

Framework:

- ESP-IDF v5.5.4

Graphics:

- LVGL v9.2.2

Core components:

- esp_hosted v2.9.7
- esp_wifi_remote v1.3.0
- esp_lvgl_port v2.7.2
- esp_codec_dev v1.2.0
- Waveshare BSP v1.0.2

Display and touch components:

- esp_lcd_ek79007 v1.0.4
- esp_lcd_touch_gt911 v1.2.0~2


PROVEN RC1 FEATURES

ForgeUI P4 RC1 includes:

- Display working
- Touch working
- LVGL v9 stable
- Header clock working
- DS3231 RTC persistence working
- Hosted WiFi working
- WiFi scan, connect, disconnect, and forget
- SD card mount and read/write test
- SD folder creation and safe rebuild
- Audio speaker test
- Volume control
- Dashboard page
- Pre-Op page foundation
- System page
- Admin page foundation
- Admin gate foundation
- Status drawer system
- Keyboard overlay
- Modular feature configuration
- Multiple visual theme foundations
- Reactor touch-driven UI foundation


WHY FORGEUI P4 EXISTS

ESP32-P4 is powerful, but full board bring-up can be painful.

ForgeUI P4 provides a working baseline so developers can start building products instead of spending weeks solving:

- display initialization
- touch setup
- LVGL integration
- ESP-Hosted WiFi setup
- SD card mounting
- RTC persistence
- audio codec bring-up
- UI/backend ownership
- unsafe LVGL threading
- project structure drift

ForgeUI P4 is designed as a real embedded product foundation, not a throwaway demo.


PROJECT GOALS

ForgeUI P4 aims to provide:

- stable ESP32-P4 hardware bring-up
- reusable LVGL v9 UI foundations
- clean embedded architecture
- modular feature control
- product-ready UI structure
- hosted WiFi reference implementation
- safe backend/UI separation
- clear ownership boundaries
- beginner-readable project structure
- professional starting point for commercial prototypes


FORGEUI P4 IS NOT

ForgeUI P4 intentionally avoids:

- demo-driven runtime logic
- hidden state ownership
- tangled UI/backend coupling
- unsafe LVGL calls from async contexts
- one-off project hacks
- unclear build configuration
- undocumented hardware assumptions


CORE DESIGN RULES

main.c owns:

- board startup
- hardware initialization
- LVGL startup
- backend startup
- runtime loop order

Backends own system truth.

UI only:

- renders current state
- sends user intent

UI does not own hardware state.

No LVGL calls from unsafe async callbacks.

Feature ownership belongs in:

00_ForgeUI_Config.h


PROJECT STRUCTURE

Typical main folder structure:

main.c

00_ForgeUI_Config.h

01_FG_HMI.c
01_FG_HMI.h

05_FG_Icons.c
05_FG_Icons.h

10_UI_Dashboard.c
11_UI_PreOp.c
12_UI_System.c
13_UI_Admin.c
14_UI_Header.c
15_UI_Keyboard.c
16_UI_StatusDrawer.c
17_UI_AdminGate.c
17_UI_ReactorModal.c

20_RTC.c
21_RTC_DS3231.c

30_Audio.c
30_WIFI.c

40_SD.c

50_SDMMC_BUS.c
50_SDMMC_BUS.h


FEATURE CONFIG SYSTEM

ForgeUI P4 uses compile-time feature switches.

Example:

#define FORGEUI_ENABLE_WIFI     1
#define FORGEUI_ENABLE_SD       1
#define FORGEUI_ENABLE_AUDIO    1
#define FORGEUI_ENABLE_RTC      1
#define FORGEUI_ENABLE_PREOP    1

Set:

0 = disabled
1 = enabled

Purpose:

- cleaner builds
- modular product variants
- easier feature testing
- smaller firmware builds
- safer project scaling


THEME SYSTEM

ForgeUI P4 includes multiple visual style foundations.

Current theme families include:

- ATLAS LIGHT
- NEBULA BLUE
- ForgeUI Reactor

Theme screenshots are stored in:

docs/images/Themes

The Reactor UI direction is a touch-driven tile interface designed for a more modern embedded product feel.


DISPLAY SYSTEM

Current display baseline:

- stable LVGL rendering
- touch input working
- native BSP panel orientation
- startup rotation flash removed
- theme-ready UI structure

Display hardware:

- EK79007 MIPI DSI panel
- GT911 capacitive touch


RTC SYSTEM

RTC strategy:

- DS3231 provides persistent time
- ESP system time is used during runtime
- DS3231 restores time at boot
- UI can update stored RTC time

Current RTC features:

- live clock
- header clock
- manual time set
- power-off time retention


AUDIO SYSTEM

Current audio baseline:

- ES8311 codec path working
- speaker output working
- beep test working
- runtime volume control working


HOSTED WIFI

Important:

ESP32-P4 does not contain a native WiFi radio.

ForgeUI P4 uses the onboard ESP32-C6 through ESP-Hosted.

WiFi architecture:

- ESP32-P4 host processor
- ESP32-C6 WiFi coprocessor
- ESP-Hosted
- esp_wifi_remote
- SDIO transport

Current proven WiFi features:

- hosted WiFi init
- WiFi scan
- WiFi connect
- WiFi disconnect
- WiFi forget
- IP address display

Important configuration notes:

- Host WiFi enabled
- WiFi Remote enabled
- PSRAM XIP disabled
- TWT disabled
- Hosted WiFi proven stable


SD CARD SYSTEM

Current SD features:

- SD card mount
- ForgeUI folder creation
- read/write test
- folder listing
- live rebuild
- safe reset path

Important:

ForgeUI P4 avoids live full-formatting inside the UI because SD and Hosted WiFi share sensitive hardware paths.

The stable approach is:

- safe app-level reset
- delete/rebuild ForgeUI app folders
- avoid destructive low-level format from the live UI


KNOWN GOOD STARTUP ORDER

Current proven startup order:

1. Display startup
2. LVGL startup
3. UI creation
4. Hosted WiFi init
5. SD init
6. Runtime loop start

Important hardware rule:

Hosted WiFi should initialize before SD card mounting on this board.


BUILD ENVIRONMENT

Recommended development setup:

- Windows
- Visual Studio Code
- ESP-IDF Extension
- ESP-IDF v5.5.4

Build:

idf.py build

Flash:

idf.py flash monitor

Full clean:

idf.py fullclean


MENUCONFIG REFERENCE

Known-good setup references are stored in:

docs/setup

Important configuration areas:

- ESP-Hosted
- WiFi Remote
- SDIO transport
- PSRAM XIP disabled
- TWT disabled
- SD card configuration
- RTC clock configuration
- power management


SCREENSHOTS

Theme and UI screenshots are stored in:

docs/images/Themes

Recommended screenshots for public release:

- Dashboard
- System page
- WiFi tile
- SD tile
- Audio tile
- Status drawer
- Admin gate
- Theme examples


ROADMAP

Planned future work:

- more themes
- polished transitions
- stronger admin authentication
- SPIFFS or SD-backed mini database
- reusable widget library
- overlay system
- starter product editions
- additional ESP32-P4 board support
- possible ESP32-S3 edition


LICENSE

ForgeUI source code:

Copyright (c) 2026 Scott Forster

Licensed under the ForgeUI Source Available License.

See:

LICENSE

Third-party components retain their own licenses.

See:

THIRD_PARTY_LICENSES.md


THIRD PARTY SOFTWARE

ForgeUI P4 uses and acknowledges third-party software and vendor ecosystems including:

- LVGL
- Espressif ESP-IDF
- Espressif managed components
- Waveshare BSP and board support packages

Please review all third-party licenses before redistribution or commercial use.


DISCLAIMER

This project is provided as-is without warranty.

Before commercial deployment, always validate:

- electrical safety
- thermal safety
- hardware stability
- regulatory requirements
- production suitability


KEYWORDS

ESP32-P4
ESP32 P4
LVGL
LVGL v9
ESP-IDF
ESP32-P4-WIFI6-Touch-LCD-7B
Waveshare ESP32-P4
ESP-Hosted
esp_wifi_remote
embedded UI
embedded GUI
touch screen UI
MIPI DSI
GT911
EK79007
DS3231
ES8311
SD card
RISC-V MCU
product-ready ESP32
embedded product framework