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
