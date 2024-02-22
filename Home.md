# Lab 6 Report: Sensing and Mobility
* Hannah Markwell
* Alexis Puckett

February 22, 2024

## Project Summary:

## Design/Methods:

For this lab we needed:
* A computer running Arduino IDE: MacBook Air
* RedBoard, breadboard, ultrasonic sensor, two motors, and a motor driver: SparkFun Inventor's Kit

**Part One: Ultrasonic Sensor**

Start by connecting the RedBoard to the computer running Arduino IDE. Then, connect the ultrasonic sensor to the RedBoard like in the schematic below. 
<p align="center">
  <img src="https://github.com/hrma240/Lab-6/blob/main/Screenshot%202024-02-22%20at%2012.32.10%20PM.png">
</p>
(Arduino, 2017, https://projecthub.arduino.cc/Isaac100/getting-started-with-the-hc-sr04-ultrasonic-sensor-7cabe1)


We then created the following code that reads the distance an object is from the sensor and displays this distance using the serial monitor. The following code establishes the pins of the trig and the echo in the RedBoard. It then sends out sound waves for 12ms from the trig in a loop. These sound waves bounce off of the object that is in front of the ultrasonic sensor and come back to the echo pin. The echo pin gets this data and the code converts it into the distance of the object away from the sensor and reads it on the monitor. 

We tested the resolution and precision of the sensor system and observed what happened as we moved an object close to the sensor and far away from it. 

**Part Two: Motors**

Keep the ultrasonic sensor connected to the breadboard and the RedBoard, but move the RedBoard connections to pins 7 and 6. Connect the two motors and motor driver to the breadboard and RedBoard in the following manner.

<p align="center">
  <img src="https://github.com/hrma240/Lab-6/blob/main/Screenshot%202024-02-22%20at%2012.48.02%20PM.png">
</p>
(SparkFun, Creative Commons Attribution ShareALike 3.0, https://learn.sparkfun.com/tutorials/sparkfun-inventors-kit-experiment-guide---v40/circuit-5b-remote-controlled-robot#)




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

