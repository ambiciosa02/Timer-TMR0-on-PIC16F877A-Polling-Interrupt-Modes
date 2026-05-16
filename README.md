# ⏱️ Timer TMR0 on PIC16F877A – Polling & Interrupt Modes

**Initiation to TMR0 Timer on PIC16F877A: Polling and Interrupt Mode with mikroC & Proteus Simulation**

## 🎯 1. TP Objective

The objective of this practical work is to introduce students to the **TMR0 timer** of the **PIC16F877A** microcontroller.
The goal is to create **hardware-based timing delays** using:

- 🔹 **mikroC** development environment
- 🔹 **Proteus** simulator
- 🔹 **Polling mode** (scrutation)
- 🔹 **Interrupt mode**


## 🧱 3. Project Structure

The project is divided into two main parts:

### 🔷 Part A – TMR0 in Polling Mode (Scrutation)

**Objective:**
Blink a **green LED** connected to **RC0** (200 ms ON, 200 ms OFF) using TMR0 **without interrupts**.

**Calculations for 200 ms delay:**
- Number of overflows needed = 200 ms / 13.1072 ms = **15.25** → **15 overflows**

**Implementation:**
- Configure `OPTION_REG = 0b00000111` (internal clock + prescaler 1:256)
- Loop indefinitely testing `INTCON.T0IF` flag
- When flag = 1 → increment counter, clear flag
- After 15 overflows → toggle green LED state
<br>

<img width="206" height="179" alt="image" src="https://github.com/user-attachments/assets/bf7a01bd-3adf-490a-8038-8dd5f4a8ee83" />

**Code Logic:**
Configure TMR0 with prescaler 1:256
counter = 0
Loop:
Wait for T0IF = 1
Clear T0IF
counter++
If counter >= 15:
Toggle GREEN LED
counter = 0

### 🔷 Part B – TMR0 with Interrupt Mode

**Objective:**
Generate a **periodic interrupt every 2 seconds** to toggle a **red LED**, while the main program continues blinking the **green LED**.

**Calculations for 2 seconds delay:**
- Number of overflows = 2000 ms / 13.1072 ms = **152.5** → **153 overflows**

**Implementation:**
- Enable global interrupts (`GIE`) and TMR0 interrupt (`T0IE`) in `INTCON`
- Interrupt service routine (ISR) executes automatically
- ISR counts overflows and toggles red LED when target is reached
- Main program handles green LED blinking independently

<br>
<img width="208" height="176" alt="image" src="https://github.com/user-attachments/assets/23b49cb8-c1d6-4577-9d7b-690c67bc9844" />

**Code Logic:**
Main Program:
Configure TMR0, enable interrupts
Loop forever:
Blink green LED with delays

Interrupt Service Routine:
If T0IF = 1:
Clear T0IF
counter++
If counter >= 153:
Toggle RED LED
counter = 0

🚀 8. How to Run the Project
📍 In mikroC:
Open the project file (.mcppi)

Verify configuration: PIC16F877A, 20 MHz

Compile (F9) to generate the .hex file

📍 In Proteus:
Open the circuit schematic (.pdsprj)

Double-click the PIC16F877A component

Browse and load the generated .hex file

Click Play ▶️ to start simulation

⚖️ 14. License
📚 This project is for educational purposes only
