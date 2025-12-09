This repository provides a Home Assistant blueprint for the **Tuya Zigbee Smart Knob** (model: `TS004F`, manufacturer: `TZ3000_gwkzibhs`), which is widely sold under various brands.

The blueprint works with **ZHA** and supports:

- Single press
- Double press
- Long press
- Rotate left
- Rotate right

This version fixes issues where Home Assistant only recognized rotation events, by handling both `press_type` and `remote_button_*` events emitted by the device firmware.

---

## 🧠 Why this blueprint?

The TS004F sends **multiple event formats** depending on firmware.  
For example, a double press may be:
