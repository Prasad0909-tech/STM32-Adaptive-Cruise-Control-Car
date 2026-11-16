# STM32 Adaptive Cruise Control Model Car

A small model car that controls its own speed based on the distance to an obstacle or a vehicle ahead. It demonstrates the basic idea behind Adaptive Cruise Control (ACC) in modern cars, built on an STM32F446RE microcontroller.

![Car photo](images/car_front.jpg)

## Demo
[Watch the demo video](ADD-VIDEO-LINK-HERE)

## How It Works
1. An **HC-SR04 ultrasonic sensor** at the front sends out sound pulses and listens for the echo. The echo time gives the distance.
2. The **STM32F446RE** measures this echo time with a hardware timer and calculates the distance.
3. The distance is compared with limits stored in the program to decide the speed:
   - **Very close:** the car stops.
   - **Near:** the car runs slowly.
   - **Far:** the car speeds up, and the larger the distance, the higher the speed.
4. The STM32 sends **PWM signals** to the **L298N motor driver**. A wider pulse gives the motors more power (faster), and a narrower pulse slows them down.
5. The L298N drives the **four N12 gear motors** (two on each side) from the battery pack.
6. This repeats continuously, so the car always reacts to the newest distance. Speed changes in small steps so the car doesn't jerk.

## Distance Thresholds
| Zone | Distance | Behaviour |
|------|----------|-----------|
| Very close | below [__] cm | Car stops |
| Near | [__] to [__] cm | Slow speed |
| Far | above [__] cm | Speed increases with distance |

## Hardware Used
| Component | Purpose |
|-----------|---------|
| STM32F446RE (Nucleo) | Measures, decides and controls |
| HC-SR04 ultrasonic sensor | Measures distance |
| L298N motor driver | Supplies motor current the STM32 pins can't provide |
| 4 x N12 gear motors | Drive the wheels |
| 3 x 3.7V Li-ion cells | Power supply |
| Jumper wires, chassis | Connections and body |

## Pin Connections
| Signal | STM32 Pin | Connected To |
|--------|-----------|--------------|
| Trigger | [PA_] | HC-SR04 TRIG |
| Echo | [PA_] | HC-SR04 ECHO |
| PWM (left motors) | [PA_] | L298N ENA |
| PWM (right motors) | [PA_] | L298N ENB |
| Direction | [PB_] | L298N IN1 |
| Direction | [PB_] | L298N IN2 |
| Direction | [PB_] | L298N IN3 |
| Direction | [PB_] | L298N IN4 |

## Software and Tools
- Language: Embedded C
- IDE: STM32CubeIDE (with STM32CubeMX configuration, HAL drivers)
- Peripherals used: GPIO, Timers (distance measurement), PWM (motor speed control)

## How to Build and Run
1. Clone this repository.
2. Open STM32CubeIDE and import the project (File > Import > Existing Projects into Workspace).
3. Build the project and flash it to the STM32F446RE using ST-Link.
4. Power the motor driver from the Li-ion pack and place the car on the floor.

## Future Improvements
- Add PID control for smoother speed regulation
- Use a more accurate sensor (such as LiDAR or ToF)
- Add a display for live distance and speed
- Add emergency braking with an additional sensor

## Author
**Prasad Vinchurkar**
E&TC Engineering, R C Patel Institute of Technology, Shirpur
Email: prasadvinchurkar0@gmail.com
