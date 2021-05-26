# Cruise Controller
COMPSYS 723 Assignment 2: Implementation of a basic cruise controller in Esterel\
***Authors: Harrison Warahi (hwar042), Cassandra D'Souza (cdso559)***

*This project was created for an assessment at The University of Auckland*

# Car Driving Controller
## Description
Car diving control physically operates the speed of the car, either directly with the accelerator and the brake, otherwise with the throttle command given by the implemented cruise regulation functions.

The function needs to know whether the Cruise control system is on, so it can choose how the car is controlled. It also needs to know the state of the accelerator and brake.

## Car Driving Control Inputs:
| Type| Name | Description|
| --- | --- | --- |
| Float | Accel | Accelerator Pedal Sensor |
| Float | Brake | Brake Pedal Sensor |
| Float | cruiseSpeed | Cruise Speed Value |
| Float | Speed | Car Speed Sensor |
| Enum  | Cruise | Cruise Control State |
<br/>
## Car Driving Control Outputs:
| Type| Name | Description|
| --- | --- | --- |
| Float | ThrottleCmd | Throttle Command |
<br/>
## Car Driving Control Logic:
### When Not Managing:
`Throttle Command = Accel or Brake`
### When Managing:
Input accel into regulation functions\
`Throttle Command = regulation output`
