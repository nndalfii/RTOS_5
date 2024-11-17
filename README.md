# STM32 FreeRTOS LED Control Project

This project demonstrates multitasking on an STM32 microcontroller using FreeRTOS. It includes control of three LEDs (Green, Red, and Blue) and simulates shared resource management with contention handling.

---

## Features
- **Multitasking with FreeRTOS:** Two tasks (`GreenLedTask` and `RedLedTask`) run concurrently to control LEDs.
- **Shared Resource Management:** A `StartFlag` variable ensures orderly access to a shared resource.
- **LED Indicators:**
  - **Green LED:** Activity of `GreenLedTask`.
  - **Red LED:** Activity of `RedLedTask`.
  - **Blue LED:** Indicates contention during resource access.

---

## Hardware Components
- **STM32 Microcontroller**
- **LEDs:**
  - **Green LED:** Connected to GPIO Pin PA5.
  - **Red LED:** Connected to GPIO Pin PB0.
  - **Blue LED:** Connected to GPIO Pin PC13.

---

## Software Components
- **HAL (Hardware Abstraction Layer):** For GPIO initialization and delay functions.
- **FreeRTOS:** Real-time kernel for task scheduling and management.

---

## Workflow

1. **Initialization:**
   - System clock and GPIO are configured.
   - Three FreeRTOS tasks are created:
     - `GreenLedTask`: Toggles the Green LED and accesses a shared resource.
     - `RedLedTask`: Toggles the Red LED and accesses the same resource.
     - `defaultTask`: Placeholder task for future extensions.

2. **Task Execution:**
   - Tasks execute in parallel based on their priorities.
   - Tasks access the shared resource guarded by the `StartFlag` variable.
   - Contention is handled by toggling the Blue LED.

3. **Shared Resource Access:**
   - A function `Access_Shared_Data()` simulates accessing shared data.
   - If a conflict occurs, the Blue LED is toggled briefly as a visual indication.

---

## Configuration

### GPIO Pin Assignments
| LED  | Port | Pin  |
|------|------|------|
| Blue | PC13 | 13   |
| Green| PA5  | 5    |
| Red  | PB0  | 0    |

### FreeRTOS Task Configuration
| Task Name         | Priority      | Stack Size |
|-------------------|---------------|------------|
| `defaultTask`     | Normal        | 128        |
| `GreenLedTask`    | Idle          | 128        |
| `RedLedTask`      | Idle          | 128        |

---

## Key Functions

### **1. void Access_Shared_Data()**
Simulates access to a shared resource:
- If the resource is free (`StartFlag == 1`), the function grants access and marks the resource as in use (`StartFlag = 0`).
- If the resource is already in use, the Blue LED toggles to indicate contention.
- Includes a delay of 500ms to simulate processing.

### **2. void GreenLedTask(void const * argument)**
Controls the Green LED:
- Toggles the Green LED on and off.
- Calls `Access_Shared_Data()` to simulate resource access.
- Delays for 2500ms before the next cycle.

### **3. void RedLedTask(void const * argument)**
Controls the Red LED:
- Toggles the Red LED on and off.
- Calls `Access_Shared_Data()` to simulate resource access.
- Delays for 500ms before the next cycle.

---

## How to Use

### Prerequisites
- STM32CubeIDE or other compatible IDE.
- STM32 development board.
- FreeRTOS library integrated into the project.

### Steps
1. Clone or download the project into STM32CubeIDE.
2. Build the project to ensure all dependencies are resolved.
3. Flash the compiled binary onto your STM32 board.
4. Observe LED behavior:
   - Green and Red LEDs toggle at different intervals.
   - The Blue LED toggles briefly if contention occurs.

---

## Troubleshooting

- **No LED Activity:**  
  Check GPIO pin connections and verify power supply.
- **Blue LED Always On:**  
  Indicates excessive contention. Adjust task delays to reduce conflicts.
- **Build Errors:**
   Ensure FreeRTOS and HAL libraries are correctly included in the project.


https://github.com/user-attachments/assets/af7cf09c-6a8d-48af-ad8b-a80d5068c606



