# DS5 Bridge Config — Web App

Web-based configuration tool for **[DS5Dongle Auto Haptics Edition](https://github.com/loteran/DS5Dongle)**.

**Live app → [https://loteran.github.io/ds5dongle-config/](https://loteran.github.io/ds5dongle-config/)**

## Requirements

- **Chrome or Edge** (WebHID API — Firefox not supported)
- DS5Dongle Pico 2 W plugged in via USB
- DualSense controller connected to the Pico via Bluetooth

## Usage

1. Open the app in Chrome/Edge
2. Click **Connect** → select the DS5Dongle from the browser dialog
3. Current config is read automatically from the device
4. Adjust settings with the sliders and toggles
5. Click **Save to Device** — written to Pico flash, persists across reboots and power cycles

After saving, the Pico briefly reconnects USB to apply the new config. The web app reconnects automatically within a few seconds.

## Parameters

| Parameter | Range | Default | Description |
|-----------|-------|---------|-------------|
| Haptics Gain | 1.0 – 2.0 | 1.0 | Global haptics amplitude multiplier |
| Speaker Volume | -100 – 0 dB | -100 | DualSense internal speaker volume |
| Audio Buffer Length | 16 – 128 | 64 | Haptics PCM packet size (lower = less latency) |
| Inactive Time | 5 – 60 min | 30 | Auto-disconnect delay when idle |
| Stay Connected | on / off | off | Disable the auto-disconnect |
| Pico LED | on / off | on | Pico onboard LED |
| Polling Rate | 250 / 500 / 1000 Hz | 250 Hz | HID report rate |
| Controller Mode | DS5 / DSE / Auto | Auto | Force DualSense or DualSense Edge mode |

### Auto Haptics

| Parameter | Range | Default | Description |
|-----------|-------|---------|-------------|
| Mode | Off / Mix / Replace | Replace | Off = native only · Mix = native + audio · Replace = audio only |
| Intensity | 0 – 200% | 100% | Strength relative to Haptics Gain |
| Low-pass Cutoff | 80 / 160 / 250 / 400 Hz | 80 Hz | Bass frequency range sent to actuators |

**Tuning tips:**
- **Replace + 80 Hz** — deep rumble from explosions, bass, engines (default)
- **Replace + 160 Hz** — balanced, good for most games
- **Replace + 250–400 Hz** — more tactile detail (footsteps, reloads)
- **Mix** — if the game already sends native haptics and you want both

## Alternative: Python CLI

No Chrome? Use the Python script from the firmware repo:

```bash
pip install hidapi
python3 scripts/set_ds5.py          # read current config
python3 scripts/set_ds5.py --help   # all options
```

## How it works

The app uses the **WebHID API** to communicate directly with the Pico over USB HID feature reports:
- `0xF7` — read config (64-byte feature report)
- `0xF6 0x01` — write config to RAM
- `0xF6 0x02` — persist to flash
- `0xF6 0x03` — reconnect USB to apply
