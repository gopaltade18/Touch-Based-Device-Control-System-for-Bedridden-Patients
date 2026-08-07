# Touch-Based Device Control System for Bedridden Patients

## Overview

The **Touch-Based Device Control System for Bedridden Patients** is an assistive embedded system developed using the **LPC2148 ARM7 Microcontroller**. The system enables bedridden or physically challenged patients to control household appliances such as a **fan, light, and emergency buzzer** using a **resistive touch screen**.

To prevent unauthorized access, the system requires password authentication through a **4×4 matrix keypad**. The password is securely stored in an **AT25LC512 SPI EEPROM**, ensuring that it remains  even after power is turned OFF.

---

# Objectives

* Help bedridden patients operate household appliances independently.
* Provide a simple and user-friendly touch-based interface.
* Ensure secure access through password authentication.
* Store passwords permanently using non-volatile memory.
* Allow password updates without reprogramming the controller.

---

# Features

* Password-based authentication
* Touch screen appliance control
* Fan and Light ON/OFF control
* Emergency buzzer activation
* Password stored in SPI EEPROM
* LCD status display
* Password change using External Interrupt (EINT1)

---

# Hardware Components

* LPC2148 ARM7 Microcontroller
* 20×4 LCD Display
* 4×4 Matrix Keypad
* Resistive Touch Screen (1255)
* AT25LC512 SPI EEPROM
* Buzzer
* 2 LEDs (Fan & Light)
* Push Button (Password Change)
* 3.3V Power Supply

---

# Software Tools

* **IDE:** Keil uVision4
* **Programming Language:** Embedded C
* **Flashing Tool:** Flash Magic

---

# Communication Protocols

| Protocol                   | Purpose                                         |
| -------------------------- | ----------------------------------------------- |
| UART                       | Receives touch screen coordinate data (X, Y, Z) |
| SPI                        | Communicates with EEPROM for password storage   |
| GPIO                       | Controls LCD, LEDs, Keypad and Buzzer           |
| External Interrupt (EINT1) | Password change request                         |

---

# System Working

### Step 1: Power ON

The LPC2148 powers up and starts program execution.

### Step 2: Peripheral Initialization

The controller initializes:

* LCD
* Keypad
* UART
* SPI
* External Interrupt (EINT1)

### Step 3: Read Password

The stored password is read from the **AT25LC512 EEPROM** through SPI communication.

### Step 4: User Authentication

The LCD prompts the user to enter the password using the keypad.

* If the password is incorrect, the system asks the user to enter it again.
* If the password is correct, the system is unlocked.

### Step 5: Device Status

Initially:

* Fan = OFF
* Light = OFF
* Buzzer = OFF

The LCD displays the current device status.

### Step 6: Touch Screen Operation

The resistive touch screen sends **X, Y, and Z coordinates** to the LPC2148 through UART.

The controller converts these coordinates into integer values and identifies the touched region.

### Step 7: Appliance Control

Depending on the touched area:

* Fan toggles ON/OFF
* Light toggles ON/OFF
* Emergency Buzzer toggles ON/OFF

### Step 8: LCD Update

After every operation, the LCD updates the status of all appliances.

### Step 9: Password Change

When the user presses the push button connected to **EINT1**:

1. Enter the current password.
2. Verify the password.
3. Enter a new password.
4. Store the new password into EEPROM using SPI.
5. Return to normal operation.

---

# Execution Flow

```text
Power ON
    │
    ▼
Initialize LCD, UART, SPI, Keypad & EINT1
    │
    ▼
Read Password from EEPROM
    │
    ▼
Enter Password
    │
 ┌──┴────────────┐
 │               │
Wrong         Correct
 │               │
 ▼               ▼
Retry        Unlock System
                 │
                 ▼
Display Device Status
                 │
                 ▼
Wait for Touch Input
                 │
                 ▼
Receive X,Y,Z Coordinates
                 │
                 ▼
Identify Touch Region
                 │
      ┌──────────┼──────────┐
      ▼          ▼          ▼
    Fan       Light      Buzzer
      │          │          │
      ▼          ▼          ▼
Toggle ON/OFF  Toggle ON/OFF  Toggle ON/OFF
                 │
                 ▼
Update LCD
                 │
                 ▼
Wait for Next Touch
```

---

# Pin Connections

| LPC2148 Pin   | Connected Device                  |
| ------------- | --------------------------------- |
| P0.1          | UART RX (Touch Screen)            |
| P0.3          | External Interrupt Switch (EINT1) |
| P0.4          | SPI Clock (SCLK)                  |
| P0.5          | SPI MISO                          |
| P0.6          | SPI MOSI                          |
| P0.7          | EEPROM Chip Select                |
| P0.8 – P0.15  | LCD Data Lines                    |
| P0.17         | LCD RS                            |
| P0.18         | LCD EN                            |
| P0.22         | LED (Light)                       |
| P0.23         | LED (Fan)                         |
| P0.25         | Buzzer                            |
| P1.16 – P1.23 | 4×4 Matrix Keypad                 |

---

# Advantages

* Easy to operate
* Secure password protection
* Low-cost embedded solution
* Low power consumption
* Non-volatile password storage
* Suitable for elderly and bedridden patients

---

# Applications

* Hospitals
* Home patient care
* Elderly assistance
* Rehabilitation centers
* Smart healthcare systems

---

# Future Enhancements

* Wi-Fi or Bluetooth connectivity
* Mobile application control
* IoT-based remote monitoring
* SMS or mobile notifications during emergencies
* Voice control integration
* Real-Time Clock (RTC) for scheduled appliance control
* Medication reminders
* Nurse call system

---

# Conclusion

The **Touch-Based Device Control System for Bedridden Patients** provides a secure, reliable, and user-friendly solution for controlling household appliances through a touch interface. By combining password authentication, EEPROM-based secure storage, UART touch communication, and SPI memory access, the system enhances independence and safety for patients with limited mobility while demonstrating practical embedded systems concepts.
  
## Block Diagram   
<img width="858" height="616" alt="Screenshot (3)" src="https://github.com/user-attachments/assets/be0b9a5b-e843-4119-8640-ccadd23fdaec" />   
## Reference  
Output Video: https://github.com/user-attachments/assets/441dc235-6f77-425f-bc0e-de0daa45938b   
Output pics:   
<img width="1200" height="1600" alt="WhatsApp Image 2026-06-07 at 20 26 50" src="https://github.com/user-attachments/assets/de11b9dd-a0ab-4a2d-9bab-802ecf0293f8" />
<img width="1200" height="1600" alt="WhatsApp Image 2026-06-07 at 20 26 50 (1)" src="https://github.com/user-attachments/assets/fdf4dbc3-3356-4a7a-b92c-4473fd8d5878" />
<img width="1200" height="1600" alt="WhatsApp Image 2026-06-07 at 20 26 51" src="https://github.com/user-attachments/assets/a6be8774-3a2e-401d-a64f-0bfab0c9a995" />
<img width="1200" height="1600" alt="WhatsApp Image 2026-06-07 at 20 26 51 (1)" src="https://github.com/user-attachments/assets/0e5ff707-2b44-48f7-977c-7e7fa3034d8f" />

  
