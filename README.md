
#  **It is finaly working!** (llflaywg)

![device-info](<https://github.com/tomaz1/ha_tuya_ble/blob/main/images/llflaywg-device-info.png?raw=true>)
![device-controls](<https://github.com/tomaz1/ha_tuya_ble/blob/main/images/llflaywg-controls.png?raw=true>)
![device-diagnostic](<https://github.com/tomaz1/ha_tuya_ble/blob/main/images/llflaywg-diagnostic.png?raw=true>)

# Home Assistant support for Tuya BLE devices

## Overview

This integration supports Tuya devices connected via BLE.

_Inspired by code of [@redphx](https://github.com/redphx/poc-tuya-ble-fingerbot)_

This fork is FROM: https://github.com/markusg1234/ha_tuya_ble

__________________________________________
[@tomaz1](https://github.com/tomaz1/ha_tuya_ble):
Added Thermostatic Radiator Valve product_id: 'llflaywg' (Category 'wkf')

[Radiator Valve was bought in Bauhaus-Slovenia]

![Radiator Valve](<https://github.com/tomaz1/ha_tuya_ble/blob/main/images/12-crnoozadje.png?raw=true>)
  
It is not so simple to add **'llflaywg'**. We need to find all DPs which device uses. Good resources, what helped me:
  
* In Tuya developer platform we have to change to "DP mode" to get all DP's! (It took me long time to find this important information !)
       https://github.com/0x5e/homebridge-tuya-platform
       Open your project->Devices->All Devices->click pencil on device (Change Control Instruction Mode) -> "DP Instruction" and "Save Configuration"

  Then: Smart Home Basic Service -> Smart Home Device Control-> Get Device Specification Attribute (last one will show "dp_id"s). [One in the middle with the same name, will not show DPs]
* or we could guess what DPs are via tuya-uncover and changing settings on phone app and observing which DP's value change and to what it is changed: 
        https://github.com/blakadder/tuya-uncover?tab=readme-ov-file
        
 \* better solution is first line, because we also get descriptions for DPs!
__________________________________________

## Installation

Place the `custom_components` folder in your configuration directory (or add its contents to an existing `custom_components` folder). Alternatively install via [HACS](https://hacs.xyz/).

[![Open your Home Assistant instance and open a repository inside the Home Assistant Community Store.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=tomaz1&repository=ha_tuya_ble&category=integration)

## Usage

Version 0.2.2 replaces Tuya Developer Platform login with your Smart Life or Tuya Smart app account. A separate developer account or IoT Core subscription is no longer required.

1. Add the **Tuya BLE** integration and keep **User Code** selected.
2. In Smart Life or Tuya Smart, open **Me → ⚙️ Settings → Account and Security → User Code**, and enter that code in Home Assistant. See [Obtaining User Code for sign-in](https://www.home-assistant.io/integrations/tuya/#obtaining-user-code-for-sign-in).
3. Scan the displayed QR code using **+ → Scan** in the app, confirm the login, and select **Submit** in Home Assistant. If the QR expires, request a new one on the same form.
4. Select your supported BLE device from the app account.
5. Confirm the retrieved local credentials. The integration matches the device UUID against nearby Bluetooth advertisements where possible. If the Bluetooth MAC is missing, choose a nearby device or enter its Bluetooth MAC address. Complete any missing required values before saving.

**Manual setup** remains available in the section below User Code, with the same device fields as before. It requires no account login.

The device must first be paired in Smart Life or Tuya Smart. Tuya may omit local keys or BLE metadata for some devices; a device appearing in the app list does not guarantee BLE support. The integration never substitutes a Wi-Fi or gateway MAC for a Bluetooth address.

Device credentials, including `local_key`, are saved in the Home Assistant config entry and used locally over BLE. Account tokens are used only during setup and are not saved. After a factory reset/re-pairing rotates the key, open **Configure** and sign in again to refresh the same device, or update its credentials manually.

Existing entries retain their saved local credentials during the upgrade. Obsolete developer-account secrets are removed. If an old entry lacks required device credentials, Home Assistant requests setup again through User Code or manual entry.

The QR form uses Home Assistant's native QR selector. The User Code instructions use the standard smaller field-description text; font styling is controlled by the Home Assistant frontend.

## Supported devices list

* Fingerbots (category_id 'szjqr')
  + Fingerbot (product_ids 'ltak7e1p', 'y6kttvd6', 'yrnk7mnn', 'nvr2rocq', 'bnt7wajf', 'rvdceqjh', '5xhbk964'), original device, first in category, powered by CR2 battery.
  + Adaprox Fingerbot (product_id 'y6kttvd6'), built-in battery with USB type C charging.
  + Fingerbot Plus (product_ids 'blliqpsj', 'ndvkgsrm', 'yiihr7zh', 'neq16kgd'), almost same as original, has sensor button for manual control.
  + CubeTouch 1s (product_id '3yqdo5yt'), built-in battery with USB type C charging.
  + CubeTouch II (product_id 'xhf790if'), built-in battery with USB type C charging.

  All features available in Home Assistant, programming (series of actions) is implemented for Fingerbot Plus.
  For programming exposed entities 'Program' (switch), 'Repeat forever', 'Repeats count', 'Idle position' and 'Program' (text). Format of program text is: 'position\[/time\];...' where position is in percents, optional time is in seconds (zero if missing).

* Temperature and humidity sensors (category_id 'wsdcg')
  + Soil moisture sensor (product_id 'ojzlzzsw').

* Temperature and humidity sensors (category_id 'zwjcy')
  + Smartlife Plant Sensor SGS01 (product_id 'gvygg3m8').

* CO2 sensors (category_id 'co2bj')
  + CO2 Detector (product_id '59s19z5m').

* Smart Locks (category_id 'ms')
  + Smart Lock (product_id 'ludzroix', 'isk2p555').

* Climate (category_id 'wk')
  + Thermostatic Radiator Valve (product_ids 'drlajpqc', 'nhj2j7su').

* **Climate (category_id 'wkf')**
  + Thermostatic Radiator Valve (product_id 'llflaywg').

* Smart water bottle (category_id 'znhsb')
  + Smart water bottle (product_id 'cdlandip')

* Irrigation computer (category_id 'ggq')
  + Irrigation computer (product_id '6pahkcau')
  + 2-outlet irrigation computer SGW02 (product_id 'hfgdqhho'), also known as MOES BWV-YC02-EU-GY

## Support project

I am working on this integration in Ukraine. Our country was subjected to brutal aggression by Russia. The war still continues. The capital of Ukraine - Kyiv, where I live, and many other cities and villages are constantly under threat of rocket attacks. Our air defense forces are doing wonders, but they also need support. So if you want to help the development of this integration, donate some money and I will spend it to support our air defense.
<br><br>
<p align="center">
  <a href="https://www.buymeacoffee.com/3PaK6lXr4l"><img src="https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png" alt="Buy me an air defense"></a>
</p>

...
