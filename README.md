# Cruise Controller
COMPSYS 723 Assignment 2: Implementation of a basic cruise controller in Esterel\
***Authors: Harrison Warahi (hwar042), Cassandra D'Souza (cdso559)***

*This project was created for an assessment at The University of Auckland*

## Project Overview
This Project is built in Esterel, a synchronous language.\
The Cruise Controller is split into three submodules, a state controller, a cruise speed controller, and a throttle controller. These are executed parallel in one parent module.

## Cruise State Controller
### Description
The Cruise State Controller manages what state the controller should be in depending on the inputs below. It will move between four states; disabled (DISABLED), standby (STDBY), On (ON) and Off (OFF). Depending on which state the cruise controller is in, the outputs of the Throttle Controller and Speed Controller will change how they retrieve their values.
The accelerator and brake will be detected when it's value is above PedalsMin.
### Inputs
| Type| Name | Description|
| --- | --- | --- |
| Pure | On | Enable the cruise control |
| Pure | Off | Disable the cruise control |
| Pure | Resume | Resume the cruise control |
| Float | Brake | Senses if the brake is pressed |
| Float | Speed | Speed of the car |
| Float | Accel | Senses if the accelerator is on |
### Outputs 
| Type| Name | Description|
| --- | --- | --- |
| Enum  | State | Cruise Control State |
### Control Logic
| Input| Output |
| --- | --- |
### Thresholds
| Type| Name | Value |
| --- | --- | --- |
| float | PedalsMin | 3.0% |

<br/>

## Cruise Speed Controller
### Description
Cruise Speed Control controls the managed "Cruise Speed" of the car, based on external inputs and state of the cruise control system. The cruise speed is 0 kmph when the system is offline, the current speed when the system is first turned on or the cruise speed is set, and can be modified incrementally. The Cruise Speed is kept between two determined thresholds (kmph).

### Thresholds
| Type| Name | Value |
| --- | --- | --- |
| float | speedMin | 30.0 |
| float | speedMax | 150.0 | 

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
Car driving Control physically operates the speed of the car, either directly with the accelerator and the brake, or with the throttle command given by the implemented cruise regulation functions. The function needs to know whether the Cruise Control system is on, so it can choose how the car is controlled. It also needs to know the state of the accelerator pedal and both, the car's current speed and cruise speed.

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

## How To Run Code:
Must be on a Linus system.
To run through the terminal, the code must be located locally (NOT IN A SHARED FOLDER), and the following commands must be run from the appropriate project directory:
`make CruiseControl.xes`\
`./CruiseControl.xes`
