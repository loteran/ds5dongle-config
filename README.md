# DS5 Bridge Config — Web App

Web-based configuration tool for **[DS5Dongle Auto Haptics Edition](https://github.com/loteran/DS5Dongle)**.

**Live app → [https://loteran.github.io/ds5dongle-config/](https://loteran.github.io/ds5dongle-config/)**

## Requirements

- **Chrome or Edge** (WebHID API — Firefox not supported)
- DS5Dongle Pico 2 W plugged in via USB

## Usage

1. Open the app in Chrome/Edge
2. Click **Connect** → select the DS5Dongle from the browser dialog
3. Config is read automatically from the device
4. Adjust settings
5. Click **Save to Device**

## Features

- Read and write all firmware parameters live
- **Auto Haptics** section (new in this fork): mode, intensity, low-pass cutoff
- Config saved to Pico flash — persists after reboot
- No install required — single HTML file, works offline

## Parameters

See the [firmware README](https://github.com/loteran/DS5Dongle#all-configuration-parameters) for the full parameter reference.
