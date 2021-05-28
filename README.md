# Cruise Controller
COMPSYS 723 Assignment 2: Implementation of a basic cruise controller in Esterel\
***Authors: Harrison Warahi (hwar042), Cassandra D'Souza (cdso559)***

*This project was created for an assessment at The University of Auckland*

## Project Overview
This Project is built in Esterel, a synchronous language.\
The Cruise Controller is split into three submodules, a state controller, a cruise speed controller, and a throttle controller. These are executed parallel in one parent module.

## Cruise State Controller
### Description
### Inputs
### Outputs 
### Control Logic
<br/>

## Cruise Speed Controller
### Description
Cruise Speed Control controls the managed "Cruise Speed" of the car, based on external inputs and state of the cruise control system. The cruise speed is 0 when the system is offline, the current speed when the system is first turned on or the cruise speed is set, and can be modified incrementally. The Cruise Speed is kept between two determined thresholds.

### Inputs
| Type| Name | Description|
| --- | --- | --- |
| Pure | Set | Button Sets Cruise Speed |
| Pure | QuickAccel | Incrememnts Cruise Speed |
| Pure | QuickDecel | Decrements Cruise Speed |
| Float | Accel | Accelerator Pedal Sensor |
| Float | Speed | Current Car Speed |
| Enum  | State | Cruise Control State |


### Outputs 
| Type| Name | Description|
| --- | --- | --- |
| Float | CruiseSpeed | Speed set by the Cruise Control |


### Control Logic
| Input| Output |
| --- | --- |
| Cruise Control is Off | `CruiseSpeed = 0` |
| Cruise Control is going on | `CruiseSpeed = Speed` |
| Cruise Control is set | `CruiseSpeed = Speed` |
| Quick Accel applied | `CruiseSpeed += increment` |
| Quick Decel applied | `CruiseSpeed -= increment` |
<br/>

## Throttle Controller
### Description
Car diving control physically operates the speed of the car, either directly with the accelerator and the brake, otherwise with the throttle command given by the implemented cruise regulation functions. The function needs to know whether the Cruise control system is on, so it can choose how the car is controlled. It also needs to know the state of the accelerator pedal and both the car's current speed and cruise speed.

### Inputs:
| Type| Name | Description|
| --- | --- | --- |
| Float | Accel | Accelerator Pedal Sensor |
| Float | CruiseSpeed | Cruise Speed Value |
| Float | Speed | Car Speed Sensor |
| Enum  | State | Cruise Control State |


### Outputs:
| Type| Name | Description|
| --- | --- | --- |
| Float | Throttle | Throttle Output |


### Control Logic:
| Input| Output |
| --- | --- |
| Cruise Control is Off | `Throttle = Accelerator Sensor` |
| Cruise Control is on | `Throttle Command = regulated output` |
