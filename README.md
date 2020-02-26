# Notification_System_For_Industry

### PROBLEM : 
Sensor based fault notification system for Industry.
### List of Hardwares: 
Arduino Mega, DC motor,accelerometer,DHT11,color,buzzer,Gas,Ultrasonic,Proximity,Water level Sensors.

## Problem Definition:
Fisrt check each and every sensor individually, note down the range,resolution and raw high and low values for it.Write a Single program to merge all sensor’s together.Use polling mechanism to read all sensor’s values.Create a chart where you can devide sensor’s values into 3 groups(LOW,MEDIUM,HIGH).As per classified group generate a particuar tone on buzzer.


|colour|UltraSonic|temperature|Accelerometer|threat Level|
|------|------|----|------|----|
|Low|Low|Low|Low|1|
|High|High|Low|Low|2|
|Low|Low|High|Low|3|
|Low|Low|Low|High|4|
|High|High|High|High|5|
