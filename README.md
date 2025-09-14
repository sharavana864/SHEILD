# 🛡️ SHIELD – Smart Healthcare Waste Sterilization & Collection System

**SHIELD (Safe Handling & Innovation for Eco-friendly Local Disposal)** is a **prototype solution** for biomedical waste management.  
It ensures **on-site sterilization for small waste** and **safe collection for larger waste** through agency support.  

---

## 🌍 Why SHIELD?
Biomedical waste is hazardous if not treated properly. SHIELD helps:  
- Convert **hazardous → non-hazardous** safely.  
- Reduce infection risks for healthcare workers.  
- Provide **smart collection and sterilization**.  

---

## ⚡ Working Logic

### 🔹 Case 1: Waste ≤ 1kg
- Waste is placed inside **SHIELD Box**.  
- The system **sterilizes 99% of microbes**.  
- LEDs + Buzzer show sterilization status.  
- After 40 sec cycle → waste becomes **safe & non-hazardous**.  

### 🔹 Case 2: Waste > 1kg
- User opens **SHIELD mobile app** (prototype in Figma).  
- Books a **delivery slot** for collection.  
- Waste is picked up by an **authorized agency**.  
- Final disposal is done via **BMWM (Biomedical Waste Management) system**.  

---

## 🛠️ Hardware Setup (Prototype Box)
- Arduino Uno R3  
- Breadboard + jumper wires  
- 1x Red LED (Sterilization ON)  
- 1x Blue LED (Sterilization Complete)  
- 220Ω resistors for LEDs  
- Active Buzzer (Piezo)  
- Servo Motor (SG90 lid)  
- Power via USB / Battery  

---

## 🔌 Circuit Setup
- **Red LED** → Pin 2 (through resistor to GND)  
- **Blue LED** → Pin 3 (through resistor to GND)  
- **Buzzer** → Pin 4 (+), GND (–)  
- **Servo Motor** → Pin 5 (signal), 5V, GND  

---
# Prototype (Figma App)

The Figma prototype demonstrates how SHIELD integrates with collection agencies:

- Waste booking flow
- Delivery slot management
- Real-time collection updates

[https://www.figma.com/design/oOm3kR59HYmV09y5yYS8dm/Untitled?node-id=0-1&p=f]

---

## Process Flow (Summary)

1. Waste 1kg @ Sterilize in SHIELD box (99% sterilization).  
   Safe for disposal in normal bins.

2. Waste > 1kg Use SHIELD app.  
   Agency pickup ’ disposed via BMWM system.

---

## Future Scope

- IoT integration for remote monitoring.
- Mobile app notifications for sterilization status.
- Real-time agency tracking.
- Waste logging & reporting for compliance.

---

## Contributors

- Santhiya
- Rahul
- Thangam
- Sharavanakumar 

## 📜 Arduino Code

```cpp
#include <Servo.h>

int redLed = 2;
int blueLed = 3;
int buzzer = 4;
Servo lidServo;

void setup() {
  pinMode(redLed, OUTPUT);
  pinMode(blueLed, OUTPUT);
  pinMode(buzzer, OUTPUT);
  lidServo.attach(5);
  Serial.begin(9600);
}

void loop() {
  Serial.println("Sterilization Starting...");

  // Step 1: Close Lid
  lidServo.write(0);
  delay(1000);

  // Step 2: Sterilization Process (40 sec)
  digitalWrite(redLed, HIGH);
  digitalWrite(blueLed, LOW);
  Serial.println("Sterilization Ongoing...");
  delay(40000); // 40 sec cycle

  // Step 3: Sterilization Complete
  digitalWrite(redLed, LOW);
  digitalWrite(blueLed, HIGH);
  tone(buzzer, 1000, 2000); // 2 sec beep
  Serial.println("Sterilization Complete!");

  // Step 4: Open Lid
  lidServo.write(90);
  delay(5000);

  // Repeat cycle
}

