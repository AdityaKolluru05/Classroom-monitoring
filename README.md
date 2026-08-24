# Classroom Environmental Monitoring using SiWG917

An IoT-based classroom monitoring system using the **Silicon Labs SiWG917** wireless SoC to measure environmental parameters such as **temperature, humidity, and noise level**, and publish the collected data to a cloud-based MQTT platform for remote monitoring.

## Overview

The system periodically collects sensor data and publishes it through an **MQTT connection** to **ThingSpeak**, where it can be monitored remotely. An alert mechanism notifies the operator when predefined environmental conditions are detected.

**Parameters monitored:** Temperature · Humidity · Noise Level

## Objectives

- Monitor classroom environmental conditions in real time
- Collect sensor data using the SiWG917 dev kit's onboard sensors
- Establish Wi-Fi connectivity via the SiWG917
- Transmit sensor data using MQTT
- Store and visualize data using ThingSpeak
- Generate alerts when conditions exceed predefined thresholds

## System Architecture

```
Classroom Sensors (Temp / Humidity / Noise)
            |
            v
        SiWG917
  (acquisition, processing, Wi-Fi, MQTT client)
            |
            v
   ThingSpeak MQTT Broker
            |
            v
   ThingSpeak Channel / Dashboard
            |
            v
   Alert / Notification System
```

## Communication Protocol

```
SiWG917 --Wi-Fi--> MQTT --> ThingSpeak MQTT Broker --> ThingSpeak Channel
```

MQTT is used for its lightweight publish/subscribe model, well suited to IoT and embedded systems.

## Hardware

- Silicon Labs SiWG917 Development Kit
- Onboard temperature sensor
- Onboard humidity sensor
- Onboard microphone / noise sensing hardware
- USB connection for programming and serial monitoring

## Software and Tools

| Tool                    | Purpose                                                     |
| ----------------------- | ----------------------------------------------------------- |
| **Simplicity Studio 6** | Build, debug, and flash the SiWG917 application             |
| **WiseConnect SDK**     | Provides SiWG917 networking, sensor, and MQTT APIs          |
| **Visual Studio Code**  | Source-code editing and project management                  |
| **C**                   | Application and embedded firmware development               |
| **MQTT**                | Transfers sensor data to the cloud                          |
| **ThingSpeak**          | Cloud storage, visualization, and monitoring of sensor data |
| **Git / GitHub**        | Version control and project repository management           |


## System Workflow

1. Initialize the SiWG917 application
2. Initialize onboard sensors
3. Connect to Wi-Fi
4. Obtain network connectivity
5. Establish MQTT connection with the cloud broker
6. Read temperature, humidity, and noise measurements
7. Process sensor values
8. Publish sensor data via MQTT
9. Visualize data on ThingSpeak
10. Check values against alert conditions
11. Trigger notification if an alert condition is met
12. Repeat

## Alert System

Example condition used during development:

```
Temperature < 15 °C  AND  Humidity > 85 %
```

```
ThingSpeak --trigger--> ThingHTTP --HTTP request--> Google Apps Script --> Email Notification
```

## Data Fields

| Field   | Parameter   | Unit                 |
|---------|-------------|-----------------------|
| Field 1 | Temperature | °C                    |
| Field 2 | Humidity    | %                     |
| Field 3 | Noise Level | dB / relative level   |

Exact topic/field mapping depends on your ThingSpeak channel configuration.

## Repository Structure

```
project-root/
├── app/
│   └── app.c
├── sensors/
│   ├── temperature_sensor.c / .h
│   ├── humidity_sensor.c / .h
│   └── noise_sensor.c / .h
├── mqtt/
│   ├── mqtt_client.c / .h
├── wifi/
│   ├── wifi_app.c / .h
├── docs/
│   └── architecture.md
├── config.h.example
├── CMakeLists.txt
├── .gitignore
├── README.md
└── LICENSE
```

## Getting Started

### 1. Clone

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd <PROJECT_DIRECTORY>
```

### 2. Install tools

- Simplicity Studio 6
- WiseConnect SDK
- Visual Studio Code
- SiWG917 SDK/toolchain components

### 3. Connect the board

Connect the SiWG917 dev kit via USB and verify the serial/debug interface is detected.

### 4. Configure Wi-Fi and MQTT


Step 4 — Configure and establish MQTT communication

Initialize the network.
Connect the SiWG917 to the Wi-Fi network.
Obtain the device IP address.
Initialize the MQTT client.
Configure the MQTT connection parameters.
Connect to the MQTT broker.
Wait for the broker to confirm the connection.
Subscribe to the required topics.
Publish the initial MQTT message.
Exchange MQTT messages with the broker.

```c
#define WIFI_SSID       "YOUR_WIFI_NAME"
#define WIFI_PASSWORD   "YOUR_WIFI_PASSWORD"
#define MQTT_BROKER     "YOUR_MQTT_BROKER"
#define MQTT_PORT       1883
```

`config.h` is gitignored — never commit real credentials.

### 5. Build and flash

Build using the SiWG917 toolchain, then flash the firmware to the board.

### 6. Monitor output

Expected serial output:

```
Wi-Fi Connected
IP Address: xxx.xxx.xxx.xxx

MQTT Connected

Temperature: 27.4 °C
Humidity: 64.2 %
Noise Level: XX

Publishing sensor data...
Publish successful
```

## Security

Never commit: Wi-Fi passwords, MQTT credentials, API keys, ThingSpeak credentials, or private certificates/keys. Keep them in `config.h` (gitignored) or environment variables.

## Future Enhancements

- Edge AI-based anomaly detection
- Automatic HVAC control
- Occupancy detection
- Adaptive sampling
- Multi-classroom / centralized dashboard
- TLS-secured MQTT
- Historical data analysis and prediction

## Applications

Smart classrooms · smart buildings · indoor air monitoring · labs · offices · libraries · industrial environments · IoT building management

## Project Highlights

| | |
|---|---|
| Platform | Silicon Labs SiWG917 |
| Connectivity | Wi-Fi |
| Protocol | MQTT |
| Cloud Platform | ThingSpeak |
| Language | C |
| Dev Environment | Simplicity Studio 6 / WiseConnect SDK |
| Parameters | Temperature, Humidity, Noise Level |

## Contributors

- Aditya Kolluru
- _Add other team members here_

## License

Educational/research use. Add your preferred open-source license before making the repo public.
