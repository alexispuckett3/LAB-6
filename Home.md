# Lab 6 Report: Sensing and Mobility
* Hannah Markwell
* Alexis Puckett

February 22, 2024

## Project Summary:

## Design/Methods:

For this lab we needed:
* A computer running Arduino IDE: MacBook Air
* RedBoard, ultrasonic sensor, two motors, and a motor driver: SparkFun Inventor's Kit

**Part One: Ultrasonic Sensor**


## Results:

**Part One:**

_What is the resolution of this sensing system?_ 

The resolution is 0.01cm. We can see this in the output of the code because the distance values measured by the sensor goes to the 0.01 decimal place.

_Determine how precise this sensing system is._ 

In our code, the minimum distanced measured is bouncing back 12ms. The distance that this auto signal can travel is the speed of sound times the time the signal is traveling for, which is 12ms. 340m/s*12ms = 4.08mm. This is minimum measurement that this system can measure precisely, so 4.08mm is the precision of this system. When we tried to move the object my a millimeter, the system was not able to pick this up, which makes sense because the precision is more than 1mm. 

**Part Two:**

_What is the minimum speed number for the motors to move forward?_

Our minimum speed value was 26. The motor movement was not continuous at this speed, but they were still able to move. When we lowered the speed number to 25 and less, the motors stopped moving all together. 

## Conclusions:

