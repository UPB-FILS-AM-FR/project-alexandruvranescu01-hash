# Smart Traffic Light with Video Detection (Cars and Pedestrians)

| | |
|-|-|
|`Author` | Alexandru Vranescu

## Description

This project implements an intelligent, adaptive traffic management system designed for smart city intersections. Unlike traditional timer-based traffic signaling, this system relies on real-time Edge Computer Vision to monitor traffic density dynamically. 

Using an **OpenMV Cam P4**, the system captures live grayscale footage of an intersection, evaluating pre-defined Regions of Interest (ROIs) for the roadway and sidewalk. On-board blob detection processes frame data locally to count active vehicles and pedestrians. This census is transmitted via UART serial communication to an **Arduino Nano Every** microcontroller, which acts as the core decision unit. The Arduino executes a prioritization algorithm and dynamically controls the GPIO output for Red and Green traffic signaling LEDs.

## Motivation

Traditional traffic lights operate on rigid, static timers that fail to adapt to unpredictable real-world traffic flows. This inefficiencies lead to:
* Drivers idling at empty intersections while waiting for a green light.
* Pedestrians waiting unnecessarily on sidewalks, encouraging jaywalking.
* Increased vehicle carbon emissions due to prolonged, unoptimized idling times.

By integrating Edge AI image processing with local microcontrollers, this project offers a low-cost, low-latency, and scalable infrastructure alternative. By ensuring data is processed on-board rather than streamed to a cloud server, the system also respects civic privacy laws while providing fast, reliable adaptive intersection control.

## Architecture

### Block diagram

![Block Diagram](schematics/block_diagram.png)

### Schematic

![Schematic](schematics/kicad_schematic.png)

### Components

| Device | Usage | Price |
|--------|--------|-------|
| Arduino Nano Every | Unitate centrală de decizie, parsare UART și control semafor | [75 RON](https://www.optimusdigital.ro/ro/placi-compatibile-arduino/3739-placa-de-dezvoltare-compatibila-cu-arduino-nano-every.html) |
| OpenMV Cam P4 | Achiziție imagine, Edge AI și numărare vehicule/pietoni | [390 RON](https://www.optimusdigital.ro/ro/camere/2534-openmv-cam-h7.html) |
| LED Verde | Semnalizare permisiune trecere mașini | [0.5 RON](https://www.optimusdigital.ro/ro/led-uri/17-led-verde-5mm.html) |
| LED Roșu | Semnalizare oprire mașini / Prioritate pietoni | [0.5 RON](https://www.optimusdigital.ro/ro/led-uri/16-led-rosu-5mm.html) |
| Jumper Wires | Conectarea magistralelor UART și a liniilor de masă comună (GND) | [7 RON](https://www.optimusdigital.ro/ro/fire-fire-mufate/884-set-fire-tata-tata-40p-10-cm.html) |
| Breadboard | Placă de prototipare pentru distribuirea semnalelor hardware | [10 RON](https://www.optimusdigital.ro/ro/prototipare-breadboard-uri/8-breadboard-830-points.html) |

### Libraries

| Library | Description | Usage |
|---------|-------------|-------|
| [pyb (MicroPython)](https://docs.openmv.io/library/pyb.html) | OpenMV board-specific peripheral control library | Used for accessing internal camera hardware functions, onboard LEDs, and initializing the hardware UART 3 module. |
| [sensor (MicroPython)](https://docs.openmv.io/library/omv.sensor.html) | OpenMV camera sensor control module | Used to reset the camera, lock auto-exposure/gain parameters, and capture grayscale QVGA frame snapshots. |
| [Arduino AVR Core](https://github.com/arduino/ArduinoCore-megaavr) | Hardware abstraction layer library for megaAVR architectures | Pre-installed core library used for handling standard GPIO (`digitalWrite`) and managing `Serial1` hardware UART lines on the ATMEGA4809. |

## Reference links

[OpenMV Cam UART Documentation](https://docs.openmv.io/library/pyb.UART.html)

[Arduino Nano Every Pinout & Setup Guides](https://docs.arduino.cc/hardware/nano-every)

[MicroPython Frame Blob Processing Tutorial](https://docs.openmv.io/library/omv.image.html#image.image.find_blobs)
