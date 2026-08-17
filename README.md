# Smart Lathe Conversion with IIoT using Node-RED

Converting a conventional lathe machine into a smart, connected system using industrial sensors, a PLC-based control system, and a real-time Node-RED dashboard — built as a final-year B.Tech project at Birla Vishvakarma Mahavidyalaya (BVM), in collaboration with IIT Delhi's CoE-DM.

**Team:** Ankita Pandey ([@your-github-username](#)) & Jyoti Charak
**Guided by:** Prof. Rakeshkumar S. Barot, Er. Krishana Kachhiya, Dr. Anish A. Vahora
**Institution:** Birla Vishvakarma Mahavidyalaya, Vallabh Vidyanagar (2025–2026)

---

## Problem

Conventional lathe machines run without real-time monitoring, which means faults like excessive vibration, overheating, or abnormal power draw go undetected until they cause downtime. There's no historical data to support predictive maintenance, and no remote visibility into machine health — all of which limits how far a shop floor can move toward Industry 4.0.

## What We Built

We retrofitted a standard lathe with industrial sensors and a PLC, then piped the live data into a Node-RED dashboard for real-time visualization and fault detection — without modifying the machine's core mechanical structure.

**Key capabilities:**
- Real-time monitoring of vibration, temperature, spindle RPM, tool position (X/Y axis), and power consumption
- PLC-based safety interlocks and alarm logic
- Live Node-RED dashboards with gauges, charts, and status indicators
- Chuck-key detection for operator safety
- Modular design — built to support future ML-based predictive maintenance

## System Architecture

![Block Diagram](diagrams/block-diagram.png)

Sensors feed data through two paths:
- **Vibration sensors + energy meter** → RS-485 → Serial-to-Ethernet converter → IIoT/Cloud
- **Linear scale (X/Y position) + proximity sensors** → ESP32-P4-ETH / PLC → HMI + IIoT/Cloud

Both paths converge into the Node-RED dashboard for unified real-time visualization.

![Flowchart](diagrams/flowchart.png)

## Tech Stack

| Category | Tools / Hardware |
|---|---|
| **Control** | Omron NX102-9000 PLC, NX-ID5442 (digital in), NX-OD5256 (digital out) |
| **Sensors** | Vibit-Lite (vibration + temperature), Selec EM4M energy meter, Pulsate inductive proximity sensor, Delos TTL linear scale |
| **Connectivity** | ESP32-P4-ETH, USR-TCP232-306 (Serial-to-Ethernet), RS-485/Modbus |
| **HMI** | Omron NB7W-TW01B (7" touchscreen) |
| **Software** | Node-RED + node-red-dashboard, Sysmac Studio, NB-Designer, ModScan64, Radzio Modbus Master Simulator, Arduino IDE |

## My Role (Ankita Pandey)

- Configured ESP32-P4-ETH firmware to read X/Y axis position from the Delos TTL linear scale via quadrature signal decoding, and served the data over a local web endpoint
- Set up Modbus TCP↔RTU communication using ModScan64 and the Ethernet-to-RS485 gateway to pull data from vibration sensors and the energy meter
- Built Node-RED flows to parse raw sensor registers into clean engineering values (RMS/peak acceleration, velocity, RPM, temperature)
- Designed dashboard layouts in Node-RED (gauges, tabs, groups) for headstock, tool post, energy, and position monitoring

## Results

The system was successfully deployed on a working lathe with live dashboards tracking vibration, temperature, RPM, position, and power in real time.

![Dashboard](screenshots/dashboard.png)
![Hardware Setup](screenshots/hardware-setup.png)

Full sensor-level dashboards (headstock, tool post, energy meter) and wiring details are documented in the [project report](docs/Project_Report.pdf).

## Node-RED Flows

Exported flow JSON files are available in [`node-red-flows/`](node-red-flows/) — import directly into Node-RED via **Menu → Import**.

## Firmware

ESP32-P4-ETH firmware for reading the TTL linear scale (X/Y axis DRO) is in [`firmware/`](firmware/).

## Future Scope

- Mobile app for remote monitoring
- ML-based predictive maintenance using vibration pattern analysis
- Migration to OPC-UA / MQTT for more scalable industrial communication
- Multi-machine networking toward a full smart-factory setup
- Cloud analytics (AWS/Azure) for long-term trend analysis

## Documentation

- 📄 [Full Project Report (PDF)](docs/Project_Report.pdf)
