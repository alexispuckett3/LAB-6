# Lab 6 Report: Sensing and Mobility
* Hannah Markwell
* Alexis Puckett

February 22, 2024

## Project Summary:


The purpose of this lab is to learn about another type of sensor. In Lab 6 we are introduced to the ultrasonic sensor. An ultrasonic sensor is commonly used when it comes to detecting items and determining distance. It uses echolocation to detect objects by sending out bursts of sound and recording the time it takes to come back in order to determine the distance the object is at.  We will also be using analog and digital signals/sensors. Digital signals have a finite set of values (ex 0V to 12V), it cannot reach infinity. On the other hand, analog sensors have infinite numbers of sensors when it comes to detecting and determining values. This creates a continuous wave compared to a stepping wave that digital sensors create. Due to the fact that analog sensors cannot read digital ones a conversion needs to take place. By using the Arduino IDE system that we were introduced to last week the conversion is made. The software has a converter that can read analog sensors and convert it to digital sensors. Also, in order to control the movement of the motor, we will also be using the Arduino IDE system and an actuator. This system allows us to program the motor as well as see the results of the ultrasonic sensor and the actuator moves and controls the system. The H-Bridge will operate the motors that we will use in this lab in accordance with the Arduino. It allows us to see the interface of the motor as well as control the direction and speed of the rotation (i.e. backward and forwards).  With all of these factors in mind we will be able to simulate the workings of a car when attempting to avoid collisions. 

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


We then created code based on code from Arduino's project hub, that reads the distance an object is from the sensor and displays this distance using the serial monitor. The following code establishes the pins of the trig and the echo in the RedBoard. It then sends out sound waves for 12ms from the trig in a loop. These sound waves bounce off of the object that is in front of the ultrasonic sensor and come back to the echo pin. The echo pin gets this data and the code converts it into the distance of the object away from the sensor and reads it on the monitor. 

insert code

We tested the resolution and precision of the sensor system and observed what happened as we moved an object close to the sensor and far away from it. 

**Part Two: Motors**

Keep the ultrasonic sensor connected to the breadboard and the RedBoard, but move the RedBoard connections to pins 7 and 6. Connect the two motors and motor driver to the breadboard and RedBoard in the following manner.

<p align="center">
  <img src="https://github.com/hrma240/Lab-6/blob/main/Screenshot%202024-02-22%20at%2012.48.02%20PM.png">
</p>
(SparkFun, Creative Commons Attribution ShareALike 3.0, https://learn.sparkfun.com/tutorials/sparkfun-inventors-kit-experiment-guide---v40/circuit-5b-remote-controlled-robot#)

Then, use code from SparkFun to move both motors. This code controls the direction of both motors by sending a message for the user to type in the direction and distance they want the motors to travel. The motors then travel in this direction and for how far the user typed in. They stop when they have reached that distance. We then edited this code so that instead of controlling the distance the motors travel, we can control the speed at which the motors travel at. To do this, we got rid of the code that tells the motors to travel a certain distance and created an integer for the speed. The user can type in this integer when prompted and the motors will travel that quickly or slowly. 

```c++
//the right motor will be controlled by the motor A pins on the motor driver
const int AIN1 = 13;           //control pin 1 on the motor driver for the right motor
const int AIN2 = 12;            //control pin 2 on the motor driver for the right motor
const int PWMA = 11;            //speed control pin on the motor driver for the right motor

//the left motor will be controlled by the motor B pins on the motor driver
const int PWMB = 10;           //speed control pin on the motor driver for the left motor
const int BIN2 = 9;           //control pin 2 on the motor driver for the left motor
const int BIN1 = 8;           //control pin 1 on the motor driver for the left motor


int speeds;

const int driveTime = 20;      //this is the number of milliseconds that it takes the robot to drive 1 inch
                               //it is set so that if you tell the robot to drive forward 25 units, the robot drives about 25 inches

const int turnTime = 8;        //this is the number of milliseconds that it takes to turn the robot 1 degree
                               //it is set so that if you tell the robot to turn right 90 units, the robot turns about 90 degrees

                               //Note: these numbers will vary a little bit based on how you mount your motors, the friction of the
                               //surface that your driving on, and fluctuations in the power to the motors.
                               //You can change the driveTime and turnTime to make them more accurate

String botDirection;           //the direction that the robot will drive in (this change which direction the two motors spin in)
String speed;               //the speed



void setup() {

    //set the motor control pins as outputs
  pinMode(AIN1, OUTPUT);
  pinMode(AIN2, OUTPUT);
  pinMode(PWMA, OUTPUT);

  pinMode(BIN1, OUTPUT);
  pinMode(BIN2, OUTPUT);
  pinMode(PWMB, OUTPUT);

  Serial.begin(9600);

  //prompt the user to enter a command
  Serial.println("Enter a direction followed by a speed.");
  Serial.println("f = forward, b = backward, r = turn right, l = turn left, s = stop");
  Serial.println("Example command: f 50");
}

void loop() {

  if (true)
  {                                                     //if the switch is in the ON position
    if (Serial.available() > 0)                         //if the user has sent a command to the RedBoard
    {
      botDirection = Serial.readStringUntil(' ');       //read the characters in the command until you reach the first space
      speed = Serial.readStringUntil(' ');           //read the characters in the command until you reach the second space

      //print the command that was just received in the serial monitor
      Serial.print(botDirection);
      Serial.print(speed);
      Serial.println(speed.toInt());
      speeds = speed.toInt();

      if (botDirection == "f")                         //if the entered direction is forward
      {
        rightMotor(speeds);                                //drive the right wheel forward
        leftMotor(speeds);                                 //drive the left wheel forward
        //delay(10000);            //drive the motors long enough travel the entered distance
        //rightMotor(0);                                  //turn the right motor off
        //leftMotor(0);                                   //turn the left motor off
        }
       
      else if (botDirection == "b")                    //if the entered direction is backward
      {
        rightMotor(-speeds);                               //drive the right wheel forward
        leftMotor(-speeds);                                //drive the left wheel forward
        //delay(driveTime * speed.toInt());            //drive the motors long enough travel the entered distance
        //rightMotor(0);                                  //turn the right motor off
        //leftMotor(0);                                   //turn the left motor off
      }
      else if (botDirection == "r")                     //if the entered direction is right
      {
        rightMotor(-speeds);                               //drive the right wheel forward
        leftMotor(speeds);                                 //drive the left wheel forward
        //delay(turnTime * speed.toInt());             //drive the motors long enough turn the entered distance
        //rightMotor(0);                                  //turn the right motor off
        //leftMotor(0);                                   //turn the left motor off
      }
      else if (botDirection == "l")                   //if the entered direction is left
      {
        rightMotor(speeds);                                //drive the right wheel forward
        leftMotor(-speeds);                                //drive the left wheel forward
        //delay(turnTime * speed.toInt());             //drive the motors long enough turn the entered distance
        //rightMotor(0);                                  //turn the right motor off
        //leftMotor(0);  
        }                                 //turn the left motor off
      else if (botDirection == "s")
      {
        rightMotor(0);
        leftMotor(0);
      }
    }
  }
  else
  {
    rightMotor(0);                                  //turn the right motor off
    leftMotor(0);                                   //turn the left motor off
  }
}

/********************************************************************************/
void rightMotor(int motorSpeed)                       //function for driving the right motor
{
  if (motorSpeed > 0)                                 //if the motor should drive forward (positive speed)
  {
    digitalWrite(AIN1, HIGH);                         //set pin 1 to high
    digitalWrite(AIN2, LOW);                          //set pin 2 to low
  }
  else if (motorSpeed < 0)                            //if the motor should drive backward (negative speed)
  {
    digitalWrite(AIN1, LOW);                          //set pin 1 to low
    digitalWrite(AIN2, HIGH);                         //set pin 2 to high
  }
  else                                                //if the motor should stop
  {
    digitalWrite(AIN1, LOW);                          //set pin 1 to low
    digitalWrite(AIN2, LOW);                          //set pin 2 to low
  }
  analogWrite(PWMA, abs(motorSpeed));                 //now that the motor direction is set, drive it at the entered speed
}

/********************************************************************************/
void leftMotor(int motorSpeed)                        //function for driving the left motor
{
  if (motorSpeed > 0)                                 //if the motor should drive forward (positive speed)
  {
    digitalWrite(BIN1, HIGH);                         //set pin 1 to high
    digitalWrite(BIN2, LOW);                          //set pin 2 to low
  }
  else if (motorSpeed < 0)                            //if the motor should drive backward (negative speed)
  {
    digitalWrite(BIN1, LOW);                          //set pin 1 to low
    digitalWrite(BIN2, HIGH);                         //set pin 2 to high
  }
  else                                                //if the motor should stop
  {
    digitalWrite(BIN1, LOW);                          //set pin 1 to low
    digitalWrite(BIN2, LOW);                          //set pin 2 to low
  }
  analogWrite(PWMB, abs(motorSpeed));                 //now that the motor direction is set, drive it at the entered speed
}
```

Finally, we created a code that incorporates the ultrasonic sensor that makes the motors stop when the distance measured by the sensor is less than 10cm. 

insert code

This code sets up all of the pins that the motors and ultrasonic sensor are connected to on the RedBoard. It then goes into a looped if/else statement that sends out signal from the sensor that hits the object and bounces back for the echo pin to measure the distance. If the distance is greater than 10cm, both motors turn on at a specified speed (100 in our case), otherwise, the motors stay off or turn off if the distance becomes less than 10cm. 

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

By the end of this lab, a better understanding of ultrasonic sensors was obtained and learned. On top of this, the learning about analog and digital signals as well as the functions and workings of the H-bridge was also obtained and learned. By using the Arduino systems we found the resolution to 0.01cm, which showed us how precise the ultrasonic sensor can be. We also found that the minimum measurement of the sensor is 4.08 mm, which supports the findings of how precise the ultrasonic sensor is which is 1 mm. By using the Arduino system and the H-bridge we were able to command the motors to rotate front, back, right, and left. We were also able to determine the minimum speed. If the command was any less than 26 the motos would cease to move. With that being said we were able to command differing speeds as well.   

