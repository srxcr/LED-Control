# PIC18F4580 LED Control Using External Interrupt (INT0)

> **Quick Start:** This project implements external interrupt handling on a PIC18F4580 microcontroller. Pressing a button on pin RB0 triggers INT0, causing 8 LEDs on PORTD to display a pattern sequence: `0xCC` → `0x33` → `0x00`.

## 💡 Project Description

This educational project demonstrates the use of an external interrupt (INT0) on a PIC18F4580 microcontroller to control eight LEDs connected to PORTD. When an interrupt is triggered on the RB0 pin, the microcontroller executes an Interrupt Service Routine (ISR) that displays an LED pattern sequence. This is an excellent learning tool for understanding interrupt-driven embedded systems and event-based programming.

---

## 📁 Repository Structure

```
INTERUPT/
├── main.c                    # Main program and ISR implementation
├── README.md                 # This file
└── [Additional source files]
```

---

## 🛠️ Hardware Components

* **PIC18F4580 Microcontroller**
* **8 × Red LEDs** (with appropriate current-limiting resistors)
* **1kΩ Pull-up Resistor** (for RB0)
* **Push Button** (momentary contact switch)
* **5V Power Supply**
* **Connecting Wires**
* **Breadboard or PCB** (for circuit assembly)

### Circuit Connections

| Component | Connection |
|-----------|-----------|
| LEDs D1–D8 | PORTD (RD0–RD7) |
| INT0 Interrupt Input | RB0 (Pin 33 on 40-pin DIP package) |
| Pull-up Resistor | RB0 to +5V |
| Push Button | RB0 to GND (for interrupt trigger) |
| LED Series Resistors | ~220Ω resistors in series with each LED |
| Common Ground | All components share common ground |

### Detailed Wiring Diagram

```
        +5V
         |
        1kΩ (Pull-up)
         |
    +----o----+
    |         |
   RB0       Push Button
    |         |
    +----o----+
         |
        GND

PORTD to LEDs:
RD0 ----[220Ω]----LED1----GND
RD1 ----[220Ω]----LED2----GND
RD2 ----[220Ω]----LED3----GND
RD3 ----[220Ω]----LED4----GND
RD4 ----[220Ω]----LED5----GND
RD5 ----[220Ω]----LED6----GND
RD6 ----[220Ω]----LED7----GND
RD7 ----[220Ω]----LED8----GND
```

---

## 💻 Software Requirements

* **MPLAB X IDE** (v5.0 or later)
* **XC8 Compiler** (v2.0 or later)
* **PIC18F4580 Header File** (`<xc.h>`)
* **Embedded C Programming Language**
* **Proteus Design Suite** (optional, for simulation)

---

## 🚀 How It Works

The project uses the external interrupt pin INT0 (RB0) to detect an interrupt event. When RB0 receives a falling-edge trigger (button press), the microcontroller:

1. **Halts** normal program execution
2. **Jumps** to the Interrupt Service Routine (ISR)
3. **Displays** the LED pattern sequence on PORTD
4. **Clears** the interrupt flag (INT0IF)
5. **Returns** to normal operation

### LED Pattern Sequence

```
Button Press → 0xCC (binary: 11001100) → 0x33 (binary: 00110011) → 0x00 (binary: 00000000)
```

After completing the sequence, the interrupt flag is cleared, and the microcontroller waits for the next interrupt.

---

## 📝 Code Overview

### Configuration Settings

The microcontroller is configured with:
- **INT0 Edge Select:** Falling edge detection (INTEDG0 = 0)
- **INT0 Priority:** High priority interrupt
- **Interrupt Enable:** INT0 interrupt enabled (INT0IE = 1)
- **Global Interrupt Enable:** Enabled (GIE = 1)
- **PORTD:** Configured as output (TRISD = 0x00)

### ISR Implementation

The Interrupt Service Routine executes the following sequence:

```c
void __interrupt() ISR(void) {
    if (INT0IF) {
        // Display first pattern
        LATD = 0xCC;
        __delay_ms(500);
        
        // Display second pattern
        LATD = 0x33;
        __delay_ms(500);
        
        // Display third pattern
        LATD = 0x00;
        __delay_ms(500);
        
        // Clear interrupt flag
        INT0IF = 0;
    }
}
```

### Main Loop

The main function initializes the microcontroller and waits for interrupts:
- Configures PORTD as output
- Initializes interrupt settings
- Enables global interrupts
- Enters idle loop waiting for external interrupt

---

## ✨ Features

* **External Interrupt (INT0) Implementation** – Full INT0 configuration and handling
* **LED Pattern Generation** – Demonstrates sequential output control
* **Interrupt Service Routine (ISR) Demonstration** – Proper ISR structure and flag management
* **Simple Embedded C Program** – Easy-to-understand code structure
* **Beginner-Friendly PIC Project** – Ideal for learning interrupt-driven programming
* **Falling-Edge Detection** – Triggered on button press (logic low transition)

---

## 💡 Understanding the Interrupt

### What is an Interrupt?

An interrupt is a signal that temporarily pauses the normal execution of a program and transfers control to a special routine called the **Interrupt Service Routine (ISR)**. This allows the microcontroller to respond immediately to external events without continuously polling.

**Benefits:**
- Event-driven programming
- Reduced CPU usage
- Immediate response to external signals
- Simplified control logic

### INT0 Configuration

| Property | Value |
|----------|-------|
| **Location** | Pin RB0 (PORTB, bit 0) |
| **Pin Number** | 33 (40-pin DIP package) |
| **Trigger Type** | Falling edge (high-to-low transition) |
| **Interrupt Flag** | INT0IF (INTCON register, bit 1) |
| **Enable Bit** | INT0IE (INTCON register, bit 4) |
| **Priority Control** | INT0IP (INTCON2 register, bit 1) |

### Interrupt Service Routine (ISR)

When an interrupt occurs:

1. **Current State Saved:** Program counter and status register are saved on the stack
2. **ISR Executed:** Microcontroller jumps to the ISR function
3. **Pattern Displayed:** LEDs show the pattern sequence (0xCC → 0x33 → 0x00)
4. **Flag Cleared:** INT0IF is set to 0 to acknowledge the interrupt
5. **Execution Resumes:** Program counter is restored, normal execution continues

---

## ▶️ Steps to Use

### 1. **Setup Development Environment**
   - Download and install MPLAB X IDE
   - Install XC8 Compiler
   - Ensure PIC18F4580 support is enabled

### 2. **Create Project**
   - Open MPLAB X IDE
   - Create a new MPLAB X project for PIC18F4580
   - Select XC8 as the compiler

### 3. **Add Source Code**
   - Copy the source code into the project
   - Ensure all configuration bits are set correctly
   - Set oscillator frequency (typically 4 MHz or 8 MHz)

### 4. **Compile**
   - Compile the code using XC8 compiler
   - Check for any errors or warnings
   - Generate the HEX file

### 5. **Program Microcontroller**
   - Connect PIC programmer (PICkit 3/4 or equivalent)
   - Load the generated HEX file
   - Program the PIC18F4580

### 6. **Assemble Circuit**
   - Build the circuit on breadboard or PCB
   - Follow the wiring connections provided above
   - Double-check all connections before powering

### 7. **Power and Test**
   - Apply 5V power supply
   - Verify LEDs turn on briefly for initial test
   - Press the push button on RB0
   - Observe the LED sequence running on PORTD

---

## ✅ Verification & Troubleshooting

### Expected Behavior

- **At Power-Up:** LEDs remain off (PORTD = 0x00)
- **Button Press:** LED pattern displays (0xCC → 0x33 → 0x00) sequentially
- **After Sequence:** LEDs turn off, waiting for next button press
- **Multiple Presses:** Pattern repeats consistently

### Troubleshooting Guide

| Issue | Possible Cause | Solution |
|-------|-------|----------|
| **LEDs don't respond** | INT0 not configured correctly | Verify INT0IE and GIE bits are set |
| **LEDs stay on continuously** | ISR not clearing INT0IF | Check that INT0IF = 0 in ISR |
| **Inconsistent LED patterns** | Switch bounce causing multiple triggers | Implement debouncing (delay ~20ms) |
| **Only some LEDs light** | Broken LED or resistor connection | Test continuity; replace LED if needed |
| **Weak LED brightness** | Incorrect resistor value or low power | Use 220Ω resistors; check power supply |
| **Button has no effect** | Pull-up resistor missing/faulty | Verify 1kΩ resistor connected to +5V |
| **Program doesn't compile** | Header file missing | Ensure `<xc.h>` is included |

### Common Issues & Solutions

**1. Switch Debouncing**
   - Mechanical switches bounce for 5-20ms
   - Add delay in ISR before processing next interrupt
   - Example: `__delay_ms(20)` after INT0IF check

**2. Timing Adjustments**
   - LED display time depends on `__delay_ms()` implementation
   - Adjust delays to 200-500ms for visible pattern
   - Formula: Delay (ms) = instruction count / (Clock frequency / 4)

**3. Proteus Simulation**
   - Set oscillator to 4MHz in circuit properties
   - Use virtual button on RB0
   - Monitor PORTD with virtual LEDs

---

## 📸 Circuit Diagram

For a visual representation of the circuit, refer to the detailed wiring diagram in the "Circuit Connections" section above. For Proteus simulation, use the provided schematic or build one following the connection table.

---

## ⚠️ Notes

* **Delay Timing:** Timing depends on the oscillator frequency used. Default assumes 4 MHz or 8 MHz clock with proper `__delay_ms()` configuration.
* **No Debounce:** No debounce mechanism is implemented for the interrupt input.
* **Switch Bounce:** False triggering may occur due to switch bounce (mechanical switches bounce for 5-20ms).
* **LED Patterns:** LED patterns can be modified by changing the hex values written to `LATD`:
  - `0xCC` = binary 11001100 (alternating pattern)
  - `0x33` = binary 00110011 (inverse pattern)
  - `0x00` = binary 00000000 (all off)
* **Current Limiting:** Always use appropriate series resistors (220Ω recommended) to protect LEDs and microcontroller pins.
* **Power Supply:** Ensure stable 5V power supply with adequate current capacity (≥100mA recommended).

### Performance Considerations

- ISR execution time: ~2-5ms per pattern cycle
- Minimum interrupt spacing: ~50ms (hardware dependent)
- Maximum interrupt frequency: ~20kHz (with proper ISR implementation)

---

## 📚 Applications

* **Interrupt Demonstration Projects** – Learning interrupt handling concepts
* **LED Pattern Generators** – Visual feedback systems
* **Embedded Systems Education** – Foundation for advanced microcontroller projects
* **PIC Microcontroller Learning** – Understanding PIC18F architecture
* **Event-Driven Control Systems** – Real-world sensor interfacing
* **Home Automation** – Button-triggered lighting sequences
* **Industrial Control** – Interrupt-based process management

---

## 📄 License

This project is intended for **educational and learning purposes**. Users are free to modify and enhance the project for academic and personal use. No commercial use without proper attribution.

---

## 🙏 Acknowledgements

Developed and tested using:

* **PIC18F4580 Microcontroller** – Microchip Technology
* **MPLAB X IDE** – Microchip Technology
* **XC8 Compiler** – Microchip Technology
* **Proteus Design Suite** – Labcenter Electronics
* **Standard Red LEDs** – Common 5mm LEDs (20mA rated)

---

## 📞 Support & Contribution

For questions, issues, or improvements:
- Review the troubleshooting section above
- Check Microchip's PIC18F4580 datasheet for detailed specifications
- Consult MPLAB X IDE documentation for compiler-specific issues

**Happy Learning! 🚀**
