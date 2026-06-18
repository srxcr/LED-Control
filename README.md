# PIC-Microcontroller-LED-Control-Project
This project demonstrates using a PIC18F4580 microcontroller to control eight red LEDs connected to PORTD. The LEDs toggle in a sequence (0xCC, 0x33, 0x00) when an external interrupt is triggered on INT0 (pin RB0).

# PIC18F4580 LED Control Using External Interrupt (INT0)

## 💡 Project Description

This project demonstrates the use of an external interrupt (INT0) on a PIC18F4580 microcontroller to control eight LEDs connected to PORTD. When an interrupt is triggered on the RB0 pin, the microcontroller executes an Interrupt Service Routine (ISR) that cycles the LEDs through a predefined pattern.

---

## 🛠️ Hardware Components

* PIC18F4580 Microcontroller
* 8 × Red LEDs
* 1kΩ Pull-up Resistor
* Push Button (Optional)
* 5V Power Supply
* Connecting Wires

### Circuit Connections

* LEDs D1–D8 → PORTD (RD0–RD7)
* INT0 Interrupt Input → RB0
* 1kΩ Pull-up Resistor → RB0 to +5V
* Push Button → RB0 to GND
* Common Ground Connection

---

## 💻 Software Requirements

* MPLAB X IDE
* XC8 Compiler
* PIC18F4580 Header File (`<xc.h>`)
* Embedded C Programming Language

---

## 🚀 How It Works

The project uses the external interrupt pin INT0 (RB0) to detect an interrupt event. When RB0 receives a falling-edge trigger, the microcontroller jumps to the Interrupt Service Routine (ISR) and displays the following LED sequence:

```text
0xCC → 0x33 → 0x00
```

After completing the sequence, the interrupt flag is cleared, and the microcontroller waits for the next interrupt.

---

## ✨ Features

* External Interrupt (INT0) Implementation
* LED Pattern Generation
* Interrupt Service Routine (ISR) Demonstration
* Simple Embedded C Program
* Beginner-Friendly PIC Project

## 💡 Understanding the Interrupt

### What is an Interrupt?

An interrupt is a signal that temporarily pauses the normal execution of a program and transfers control to a special routine called the Interrupt Service Routine (ISR).

### INT0 Configuration

* INT0 is located on pin RB0.
* It is configured as an external interrupt input.
* A falling-edge signal triggers the interrupt.
* When triggered, the interrupt flag (`INT0IF`) becomes set.

### Interrupt Service Routine (ISR)

When an interrupt occurs:

1. The microcontroller jumps to the ISR.
2. LEDs display the pattern:

   * `0xCC`
   * `0x33`
   * `0x00`
3. The interrupt flag is cleared.
4. Program execution returns to normal operation.

---

## ▶️ Steps to Use

1. Create a new MPLAB X project.
2. Copy the source code into the project.
3. Compile the code using the XC8 compiler.
4. Generate the HEX file.
5. Program the PIC18F4580 with the generated HEX file.
6. Connect the circuit according to the schematic.
7. Power the circuit.
8. Trigger RB0 by connecting it momentarily to GND.
9. Observe the LED sequence running on PORTD.

---

## 📸 Circuit Diagram

![image alt](https://github.com/manubraj/PIC-Microcontroller-LED-Control-Project/blob/e421efbaac4a259a1817dfb2983baed403ed96a6/interrupt.png)

---

## ⚠️ Notes

* Delay timing depends on the oscillator frequency used.
* No debounce mechanism is implemented for the interrupt input.
* False triggering may occur due to switch bounce.
* LED patterns can be modified by changing the values written to `LATD`.

---

## 📚 Applications

* Interrupt Demonstration Projects
* LED Pattern Generators
* Embedded Systems Education
* PIC Microcontroller Learning
* Event-Driven Control Systems

---

## 📄 License

This project is intended for educational and learning purposes. Users are free to modify and enhance the project for academic and personal use.

---

## 🙏 Acknowledgements

Developed and tested using:

* PIC18F4580 Microcontroller
* MPLAB X IDE
* XC8 Compiler
* Proteus Design Suite
* Standard Red LEDs
