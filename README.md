# Notification_System_For_Industry

### PROBLEM : 
Sensor based fault notification system for Industry.
### List of Hardwares: 
Arduino Mega, DC motor,accelerometer,DHT11,color,buzzer,Gas,Ultrasonic,Proximity,Water level Sensors.

## Problem Definition:
Fisrt check each and every sensor individually, note down the range,resolution and raw high and low values for it.Write a Single program to merge all sensor’s together.Use polling mechanism to read all sensor’s values.Create a chart where you can devide sensor’s values into 3 groups(LOW,MEDIUM,HIGH).As per classified group generate a particuar tone on buzzer.

## Code
 
    double sensorValue;
    void setup()
    {  
    Serial.begin(9600);                            // sets the serial port to 9600
     }
    void loop()
    {
    sensorValue = analogRead(0);       // read analog input pin 0
    Serial.print("AirQua=");
    Serial.print(sensorValue);               // prints the value read
    Serial.println(" PPM");
    delay(100);                                   // wait 100ms for next reading
    }

|Low|Medium|High|
|---------|--------|----------|
|AirQua=67.00 PPM|AirQua=85.00 PPM|AirQua=114.00 PPM|
