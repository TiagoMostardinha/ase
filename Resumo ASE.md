---
parent: "[[ASE]]"
date: 2024-06-19
time: 16:24
tags: 
- in-progress
topics:
- esp32
- "embedded systems"
---
# Resumo ASE
- 
---
# Map Of Content
1. [[#1. Type of Data Transfer|Type of Data Transfer]]
	1. Polling
	2. Interruptions
	3. DMA (Direct Memory  Access)
2. Timers
	1. General Purpose Timer
	2. High Resolution Timer
	3. RTC timer
	4. Watchdogs
3.  Peripheral
	1. General Purpose Input/Output (GPIO)
		- PWM
	2. ADC (Analog-to-Digital Converter)
	3. DAC (Digital-to-Analog Converter)
	4. Wireless Communication
		- Wi-Fi
		- Bluetooth
4. Interfaces
	1. I2C
	2. SPI
	3. UART
5. C
	1. Type Of Variabes
	2. Compilation
6. FreeRTOS
	1. FreeRTOS
	2. Power Management
	3. File System on Flash
	4. OTA (Updates Over The Air)
	5. Wireless Connectivity
7. Components used in class
	1. TC74 Sensor
	2. Display 7 segments
	3. SD card Reader
	4. Inversion of Logic Gate with MOSFETs
---
# 1. Type of Data Transfer
- Data Transfer is where you move data from internal components of the microcontroller itself, such as, moving data from registers of the CPU into or from the memory or peripherals.
- Besides you can transfer data between components without CPU interaction as long as the data bus is free.
- There are 3 type of data transfer essentially.

---
## References
1. https://docs.espressif.com/projects/esp-idf/en/stable/esp32c3/get-started/index.html



ATENCAO
- **Hardware timers** are the physical timer circuits on the ESP32C3 chip.
- **Software (ESP-IDF libraries)** allows you to interact with these hardware timers and define their behavior.

- **Counter:** This is indeed a core component. Both GPTs and the ESP Timer have a counter register. This register is what actually increments or decrements based on the timer configuration.
    - In the ESP32C3, GPTs are 54-bit counters, while the ESP Timer is a 64-bit counter.
- **Pre-scaler (GPTs only):** GPTs have an additional register called the pre-scaler. This allows you to divide the clock signal feeding the timer, effectively slowing down the counter's increment/decrement rate. The ESP Timer doesn't have a pre-scaler.
- **Compare Register:** This register is present in both GPTs and the ESP Timer. You can set a value in this register. When the counter reaches the value in the compare register, an event occurs (like an interrupt). This allows you to generate periodic events based on the timer.
- **Auto-reload:** Both GPTs and the ESP Timer offer auto-reload functionality. When enabled, upon reaching the compare register value, the counter automatically resets to zero and starts counting again. This is essential for creating periodic signals or tasks.