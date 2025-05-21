# ✋ Gesture-Based IR Controller

This project is a compact, SMD-based **gesture-controlled infrared (IR) transmitter**, powered by the RP2040 microcontroller and the APDS-9960 gesture sensor. It enables hands-free control of IR-enabled devices like TVs, LED strips, or home automation receivers, all without needing Bluetooth, Wi-Fi, or pairing.

---

## 📦 Features

- 🔌 Powered via USB-C (Power-only 6P connector)
- 🧠 Built on the **RP2040** dual-core microcontroller
- 👋 Integrated **APDS-9960** gesture/proximity sensor
- 📤 High-speed IR LED transmission using PWM (38kHz)
- 🔘 Manual **Bootsel** and **Reset** buttons for development
- 🌈 Optional status LED for gesture response indication
- 🔧 Fully SMD design, suitable for hand or reflow soldering

---

## 🔧 Hardware Overview

### 🧠 Core MCU
- **RP2040** with external QSPI Flash (if required)
- Powered via onboard AMS1117-3.3 LDO

### 👋 Gesture Input
- **APDS-9960** optical sensor (I2C)
- INT pin routed to GPIO for real-time gesture notifications
- Pull-up resistors (10kΩ) on SDA and SCL
- Decoupling capacitor (0.1uF) for power stability

### 📤 Infrared Output
- High-efficiency **IR LED**
- Current-limiting resistor (100Ω)
- Driven directly from a GPIO at 38kHz using PWM

### 🧪 Debug / Control
- **SW1**: Bootsel button → GPIO0 (active-low)
- **SW2**: Reset button → RP2040 `RUN` pin (active-low)
- **D1**: Optional status LED (330Ω resistor)

### 🔋 Power Regulation
- **USB-C (Power Only)** input
- **AMS1117-3.3** LDO regulator
- 10uF output capacitor (C2)
- Pull-downs (5.1kΩ) on CC1 and CC2 for proper USB-C sink negotiation

---

## 📐 GPIO Assignments

| Function         | GPIO Pin |
|------------------|----------|
| I2C SDA          | GPIO20   |
| I2C SCL          | GPIO21   |
| Gesture INT      | GPIO22   |
| Status LED       | GPIO23   |
| IR Output (PWM)  | GPIO19   |
| Bootsel (SW1)    | GPIO0    |
| Reset (SW2)      | RUN pin  |

---

## 🛠️ Component Footprints (SMD)

| Component     | Footprint                          |
|---------------|------------------------------------|
| RP2040        | `MCU_RaspberryPi:RP2040`           |
| APDS-9960     | `Sensor_Optical:APDS-9960`         |
| IR LED        | `LED_SMD:LED_0805_2012Metric`      |
| SW1/SW2       | `Button_Switch_SMD:SW_SPST_SKQG`   |
| AMS1117-3.3   | `Regulator_Linear:AMS1117-3.3`     |
| USB-C         | `Connector_USB:USB_C_Receptacle_GCT_USB4125-6P_TopMount_Horizontal` |
| Resistors     | `Resistor_SMD:R_0603_1608Metric`   |
| Capacitors    | `Capacitor_SMD:C_0603_1608Metric`  |

---

## 🧠 Logic Flow

```c
// Pseudocode overview
setup() {
    configure_i2c();
    configure_pwm(38kHz);  // for IR LED
    attach_interrupt(GESTURE_INT);
}

loop() {
    if (gesture == RIGHT_SWIPE) {
        send_ir_code(POWER);
    }
    else if (gesture == UP_SWIPE) {
        send_ir_code(VOLUME_UP);
    }
    // etc.
}
```

---

## 📝 Bill of Materials (Simplified)

| Quantity | Component       | Value    |
|----------|------------------|----------|
| 1x       | RP2040           | –        |
| 1x       | APDS-9960        | –        |
| 1x       | IR LED           | –        |
| 1x       | Status LED       | –        |
| 1x       | AMS1117-3.3      | –        |
| 1x       | USB-C Connector  | 6P       |
| 2x       | Tactile Switch   | –        |
| 2x       | 10kΩ Resistor    | Pull-up  |
| 2x       | 5.1kΩ Resistor   | USB-C CC |
| 1x       | 330Ω Resistor    | LED      |
| 1x       | 100Ω Resistor    | IR LED   |
| 1x       | 0.1uF Capacitor  | –        |
| 1x       | 10uF Capacitor   | –        |

---

## 📁 Folder Structure

```
/Gesture-IR-Controller/
├── schematic.kicad_sch
├── pcb.kicad_pcb
├── symbols/
├── footprints/
├── firmware/  (optional)
└── README.md
```

---

## Preview
![image](https://github.com/user-attachments/assets/cf513fa2-b9a6-4663-a2f8-6fd7c7ef423e)

---

## 📜 License

This project is released under the **MIT License**.  
Use it freely, improve it, deploy it — just give credit where it’s due.

---

**Built with love by Akmal Nazir**
