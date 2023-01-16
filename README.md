# esphome-votronic

![GitHub actions](https://github.com/syssi/esphome-votronic/actions/workflows/ci.yaml/badge.svg)
![GitHub stars](https://img.shields.io/github/stars/syssi/esphome-votronic)
![GitHub forks](https://img.shields.io/github/forks/syssi/esphome-votronic)
![GitHub watchers](https://img.shields.io/github/watchers/syssi/esphome-votronic)
[!["Buy Me A Coffee"](https://img.shields.io/badge/buy%20me%20a%20coffee-donate-yellow.svg)](https://www.buymeacoffee.com/syssi)

ESPHome component to monitor votronic devices via BLE

## Supported devices

* Bluetooth Connector S-BC
  * Solar Charger SR/MPP since 2014 (S/N 14Vxx.xxxxx)
  * Battery Computer S + Smart Shunt

## Untested devices

* Battery Charger VBCS-Triple
* VPC Jupiter + Smart Shunt

## Requirements

* [ESPHome 2022.12.0 or higher](https://github.com/esphome/esphome/releases).
* Generic ESP32 board

## Installation

You can install this component with [ESPHome external components feature](https://esphome.io/components/external_components.html) like this:
```yaml
external_components:
  - source: github://syssi/esphome-votronic@main
```

or just use the `esp32-ble-example.yaml` as proof of concept:

```bash
# Install esphome
pip3 install esphome

# Clone this external component
git clone https://github.com/syssi/esphome-votronic.git
cd esphome-votronic

# Create a secrets.yaml containing some setup specific secrets
cat > secrets.yaml <<EOF
wifi_ssid: MY_WIFI_SSID
wifi_password: MY_WIFI_PASSWORD

mqtt_host: MY_MQTT_HOST
mqtt_username: MY_MQTT_USERNAME
mqtt_password: MY_MQTT_PASSWORD
EOF

# Validate the configuration, create a binary, upload it, and start logs
esphome run esp32-ble-example.yaml

```

## Pairing / Bonding

TODO: Explain how to pair the ESP with the Votronic Bluetooth Connector.

## Example response all sensors enabled

```
TBD.
```

## Protocol

```
# Battery status frame
<<< 0xE8 0x04 0xBF 0x04 0x09 0x01 0x60 0x00 0x5F 0x00 0x9A 0xFE 0xFF 0xF0 0x0A 0x5E 0x14 0x54 0x02 0x04

# MPPT status frame
<<< 0xE8 0x04 0x76 0x05 0x00 0x00 0x00 0x00 0x00 0x06 0x56 0x00 0x09 0x18 0x00 0x22 0x00 0x00 0x00
```

## Known issues

None.

## Debugging

If this component doesn't work out of the box for your device please update your configuration to increase the log level to see details about the BLE communication and incoming traffic:

```
logger:
  level: VERY_VERBOSE
  logs:
    component: DEBUG
    scheduler: INFO
    mqtt: INFO
    mqtt.idf: INFO
    mqtt.component: INFO
    mqtt.sensor: INFO
    mqtt.switch: INFO
    esp32_ble_tracker: DEBUG
```

## References

* https://codeberg.org/scy/votonic
* https://cumulumbus.de/smart-camper-auslesen-der-batterie-und-solarinformationen-aus-dem-votronic-bluetooth-connector/
