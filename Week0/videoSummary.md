# Getting Started with Digital VLSI SoC Design and Planning — Summary

---

## 1. Application Development & Cross-Compilation  
- Create the application in **C** and run in **GCC** → **Output O0**  
- Run it through target-specific compilers (e.g., **RISC-V GCC**, **ARM GCC**) → **Output O1**  
- **Verify:** `O0 == O1`

---

## 2. RTL Implementation  
- Implement a **soft copy of hardware** (gates, flip-flops, etc.) using **RTL** (e.g., Verilog) and run the application on it → **Output O2**  
  - **Processor:** Synthesizable (implemented as gates)  
  - **Peripherals / IPs:**  
    - **Macros:** Synthesizable  
    - **Analog IPs** (e.g., ADC, PLL): Not necessarily synthesizable  
- **Verify:** `O2 == O1`

---

## 3. SoC Integration  
- Integrate RTL blocks into the **SoC** with GPIOs and extract → **Output O3**  
- **Verify:** `O3 == O2`

---

## 4. Physical Design  
- Perform **Floorplanning**, **Placement**, and **Routing** (convert RTL to gates and place properly)

---

## 5. Tapeout Preparation  
- Generate **GDSII file**  
- Run **DRC/LVS checks**  
- **Tapeout** and then **Tape-in**

---

## 6. Post-Silicon Verification  
- Connect the fabricated chip with peripherals and verify output → **Output O4**
