# ESPHome JBD BMS Monitor (via Webhooks) 🔋📡

[English](#english) | [Українська](#ukrainian)

---

<a name="english"></a>
## 🇬🇧 English

### Description
This project allows you to monitor a **JBD BMS (Smart BMS)** using an **ESP32** via Bluetooth (BLE) and send data to **Home Assistant** using **Webhooks**.

**Why Webhooks?**
Standard ESPHome integration uses a native API that requires a direct connection to Home Assistant. This project is designed for **remote locations** (e.g., a garage, a country house, or behind a provider's NAT/CGNAT) where the ESP32 cannot connect directly to the HA server, but has internet access. The ESP32 pushes data via HTTP POST to your Home Assistant instance.

### Features
* 📊 **Real-time Monitoring:** Voltage, Current, SOC, Power (Charging/Discharging), Cell Voltages.
* 🌡️ **Temperature:** Monitors BMS probes.
* 🌐 **Connection Status:** Reports if the BMS is connected via Bluetooth.
* 🌍 **Network Info:** Reports Local IP and Public IP (useful for tracking ISP changes).
* 🚀 **Stability:** Solves common ESP32 BLE + WiFi coexistence issues (reboots) by disabling WiFi power saving.

![Home Assistant Dashboard](jbd-bms-webhook.jpg)


### Hardware Required
* ESP32 Development Board (e.g., Wemos D1 Mini ESP32).
* JBD BMS (with Bluetooth module).

### Installation

#### 1. ESPHome Configuration (`jbd-bms-webhook.yaml`)
*Requires `syssi/esphome-jbd-bms` component.*

**Key highlights in config:**
* `wifi: power_save_mode: none` - Critical for stable BLE operation.
* `http_request` - Used to send data to HA.
* `interval` - Script that collects all sensor data into a JSON-like payload.

yaml
See the 'jbd-bms-webhook.yaml' file in this repository for the full code.
# Don't forget to replace:
# - WIFI_SSID / PASSWORD
# - BMS_MAC_ADDRESS
# - WEBHOOK_URL / KEY
Home Assistant Configuration (configuration.yaml / templates.yaml)

You need to define a webhook trigger and parse the incoming data into sensors.
YAML

# See the 'jbd-bms-webhook-add-to-template.yaml' file in this repository.
# Don't forget to replace:
# - WEBHOOK_URL / KEY
Troubleshooting
Reboots/Watchdog Trigger: If your ESP32 reboots during scanning/uploading, ensure power_save_mode: none is set in the wifi: section.
Missing MOS Temp: Many standard JBD BMS units do not have a second temperature sensor. It will show as 0 or NaN.

<a name="ukrainian"></a>
🇺🇦 Українська
Опис

Цей проект дозволяє моніторити JBD BMS (Smart BMS) за допомогою ESP32 через Bluetooth (BLE) та відправляти дані в Home Assistant використовуючи Webhooks.

Чому саме Webhooks? Стандартна інтеграція ESPHome використовує нативний API, який вимагає прямого з'єднання з Home Assistant. Цей проект створений для віддалених об'єктів (наприклад, гараж, дача або інтернет за NAT провайдера), де ESP32 не має прямого доступу до сервера HA, але має вихід в інтернет. ESP32 "штовхає" дані через HTTP POST запити на вашу адресу Home Assistant.
Можливості

    📊 Моніторинг у реальному часі: Напруга, Струм, Рівень заряду (SOC), Потужність (Заряд/Розряд), Напруга на комірках.

    🌡️ Температура: Дані з датчиків BMS.

    🌐 Статус з'єднання: Показує, чи підключена BMS по Bluetooth (Online/Offline).

    🌍 Мережа: Відслідковує локальну та публічну IP-адресу (корисно для моніторингу провайдера).

    🚀 Стабільність: Вирішено проблему конфлікту BLE + WiFi (перезавантаження) шляхом вимкнення енергозбереження WiFi.

![Home Assistant Dashboard](jbd-bms-webhook.jpg)

Необхідне залізо

    Плата розробника ESP32 (наприклад, Wemos D1 Mini ESP32).

    JBD BMS (з модулем Bluetooth).

Встановлення
1. Конфігурація ESPHome (jbd-bms-webhook.yaml)

Використовує компонент syssi/esphome-jbd-bms.

Важливі моменти:

    wifi: power_save_mode: none — Критично важливо для стабільної роботи Bluetooth.

    http_request — Використовується для відправки даних.

    interval — Скрипт збирає всі дані та відправляє їх одним пакетом.

YAML

# Дивіться файл 'jbd-bms-webhook.yaml' у цьому репозиторії для повного коду.
# Не забудьте замінити:
# - WIFI_SSID / PASSWORD
# - BMS_MAC_ADDRESS
# - WEBHOOK_URL / KEY

2. Конфігурація Home Assistant (configuration.yaml / templates.yaml)

Необхідно створити тригер webhook та розпарсити вхідні дані у сенсори.
YAML

# Дивіться файл 'jbd-bms-webhook-add-to-template.yaml' у цьому репозиторії.
# Не забудьте замінити:
# - WEBHOOK_URL / KEY

Вирішення проблем

 Перезавантаження (Watchdog): Якщо ESP32 перезавантажується під час сканування або відправки даних, переконайтеся, що у секції wifi: прописано power_save_mode: none.

 Немає температури MOS: Багато стандартних плат JBD BMS фізично не мають другого датчика температури. У цьому випадку буде показуватися 0.

Credits: Based on esphome-jbd-bms component.
