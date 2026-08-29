# Dark-Activated AC Load Controller

Hardware and PCB simulation project for the Semiconductor Physics course (HCMUT).

## Circuit Overview
- **Power Supply:** 220VAC to 9VAC step-down, bridge rectifier, LM7805 regulator (5V DC output).
- **Sensor:** CdS Photoresistor (LDR) with 10k potentiometer for threshold tuning.
- **Comparator:** LM358 Op-Amp comparing sensor voltage with fixed 2.5V reference.
- **Driver:** C945 NPN transistor driving a 5V relay with 1N4007 flyback diode protection.
- **Load:** 220VAC incandescent lamp.

## Hardware Files
- `simulation/`: Proteus schematic and simulation file (`.pdsprj`).
- `docs/`: PCB layout and physical hardware photos.

## Team Members
- Đỗ Gia Huy
- Huỳnh Võ Minh Nhựt
- Trần Nguyễn Như Huỳnh
- Nguyễn Thành Tài
- Hà Phương Nam
