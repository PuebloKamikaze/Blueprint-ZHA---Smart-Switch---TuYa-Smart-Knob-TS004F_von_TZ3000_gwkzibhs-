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

remote_button_double_press

or

press_type: 1


This blueprint catches **all** of these variants and normalizes them into clean action triggers.

---

## 📦 Installation

1. Copy the `blueprint.yaml` into:
/config/blueprints/automation/

If you want to use a photo of the smart switch in the Switch Manager, make sure the photo (in .png format) has the same filename as the YAML file.

Example:

zha-tuya-smart-knob-TS004F_von_TZ3000_gwkzibhs.yaml
zha-tuya-smart-knob-TS004F_von_TZ3000_gwkzibhs.png 



3. Restart Home Assistant or reload Blueprints.
4. Create an automation based on this blueprint.
5. Assign button actions in the Switch Manager.

---

## 🧰 Supported Actions

| Physical Action | Recognized Events |
|-----------------|------------------|
| Single press | `press_type: 0` |
| Double press | `remote_button_double_press` or `press_type: 1` |
| Long press | `remote_button_long_press` or `press_type: 2` |
| Rotate left | `left` |
| Rotate right | `right` |

---

## 🔧 Tested With

- Home Assistant OS (2025.12.2)
- Integration: **ZHA**
- Device ID shown as `TS004F_von_TZ3000_gwkzibhs`

---

## 🧪 Example Automation

alias: Example – TS004F Button Actions
trigger:
  - platform: event
    event_type: zha_event
    event_data:
      device_id: YOUR_DEVICE_ID
action:
  - choose:
      - conditions:
          - condition: template
            value_template: "{{ trigger.event.data.command == 'press_type' and trigger.event.data.args[0] == 0 }}"
        sequence:
          - service: light.toggle
            entity_id: light.living_room

      - conditions:
          - condition: template
            value_template: "{{ trigger.event.data.command == 'left' }}"
        sequence:
          - service: light.turn_on
            data:
              brightness_step: -25
            target:
              entity_id: light.living_room


---

## 💌 Contributions

Pull requests and improvements are very welcome!  
If you find firmware variations, feel free to open an issue.

---

## 📜 License

Released under the MIT License. See LICENSE for details.
