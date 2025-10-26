# BAREMETAL_STM32_startup_linkerscript  
A minimal bare-metal startup / linker-script project for STM32 microcontrollers, providing startup code, linker script and a simple LED blink demo.

---

## 🧩 Project Overview  
This project demonstrates a bare-metal environment for the STM32 microcontroller (Cortex-M series) with no RTOS, no HAL/LL libraries, just direct register-level startup and minimal C runtime support.  

**Key components:**  
- Custom linker script (`stm32_ls.ld`) for memory and section layout  
- Startup code (`stm32_startup.c`) with vector table, reset handler, and data/BSS initialization  
- Demo firmware (`main.c`, `led.c/.h`) for LED blinking  
- Minimal system calls (`syscalls.c`) for basic C runtime stubs  
- Makefile to build using the GNU Arm toolchain  

---

## ✅ Why Use This
Use this project if you want to:  
- Develop truly bare-metal STM32 firmware without HAL or CMSIS  
- Understand startup sequence, vector tables, and memory initialization  
- Learn how linker scripts control Flash/RAM layout  
- Build minimal, efficient embedded codebases  

---

## 🛠️ Repository Structure
📁 BAREMETAL_STM32_startup_linkerscript
│
├── Makefile # Build automation using GCC toolchain
├── stm32_ls.ld # Custom linker script (memory & sections)
├── stm32_startup.c # Vector table, reset handler, init code
├── syscalls.c # Minimal system call stubs for libc
├── main.c, main.h # Main application logic
├── led.c, led.h # GPIO LED blink implementation
├── final_sh.elf # Compiled firmware binary
└── final.map # Memory map output for analysis


**Key modules:**

| File | Role |
|------|------|
| **stm32_ls.ld** | Defines Flash/RAM regions, stack, heap, and section layout |
| **stm32_startup.c** | Initializes `.data` and `.bss`, sets up stack, and calls `main()` |
| **syscalls.c** | Provides lightweight stubs for newlib functions (`_sbrk`, `_write`, etc.) |
| **main.c / led.c** | Demonstrates a working LED toggle loop |
| **Makefile** | Handles compilation, linking, and artifact generation |

---

## ⚙️ How It Works  

1. **MCU Reset:** The core loads the **initial stack pointer** and jumps to `Reset_Handler`.  
2. **Reset_Handler:**  
   - Copies `.data` from Flash → RAM  
   - Clears `.bss`  
   - Calls `SystemInit()` (optional)  
   - Invokes `main()`  
3. **Linker Script:** Defines memory sections (Flash, RAM) and symbol boundaries.  
4. **Syscalls:** Provide stubs so the code links even without a full OS or libc.  
5. **Main Loop:** Toggles GPIO pin to blink an LED — proving the system boots correctly.  

---

## 🧠 Memory Layout Example  

Example memory regions defined in `stm32_ls.ld`:  

```ld
MEMORY
{
  FLASH (rx)  : ORIGIN = 0x08000000, LENGTH = 128K
  RAM   (rwx) : ORIGIN = 0x20000000, LENGTH = 20K
}

| Section   | Description              | Region                  |
| --------- | ------------------------ | ----------------------- |
| `.text`   | Code and constants       | FLASH                   |
| `.rodata` | Read-only data           | FLASH                   |
| `.data`   | Initialized globals      | RAM (copied from Flash) |
| `.bss`    | Zero-initialized globals | RAM                     |
| `.stack`  | Stack memory             | Top of RAM              |
| `.heap`   | Dynamic allocation       | RAM                     |


Building and Flashing
🔧 Prerequisites

GNU Arm Embedded Toolchain (arm-none-eabi-gcc, arm-none-eabi-objcopy, arm-none-eabi-size)

Make (MSYS2/WSL or Linux)

ST-Link or J-Link programmer

🛠️ Build the Project

git clone https://github.com/Abunique/BAREMETAL_STM32_startup_linkerscript.git
cd BAREMETAL_STM32_startup_linkerscript
make

final_sh.elf   → Executable firmware
final.map      → Memory map report

🔩 Flash to Target

st-flash write final_sh.bin 0x08000000
BAREMETAL_STM32_startup_linkerscript/
├── main.c                 # Application entry point
├── startup.s              # Assembly startup code (Reset handler, vector table)
├── linker.ld              # Custom linker script for STM32 memory mapping
├── Makefile               # Simple GCC build script
└── README.md              # This file

