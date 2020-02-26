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


## All in one 

        #include "DHT.h"
        #define DHTPIN 2     // what digital pin we're connected to
        #define DHTTYPE DHT11   // DHT 11 is our sensor
        #define SERVO_PIN 3
        #define buzzer 12
        int sensorValue;
        int sensorValueGas;
        #include "Wire.h"
        #include "I2Cdev.h"
        #include "MPU6050.h"
        int sensorValueProximity;
        MPU6050 accelgyro;
        int16_t raw_ax, raw_ay, raw_az;
        int16_t raw_gx, raw_gy, raw_gz;
        DHT dht(DHTPIN, DHTTYPE);

        int trigPin = 11;    // Trigger
        int echoPin = 12;    // Echo
        long duration, cm,inches;

        #define S0 4
        #define S1 5
        #define S2 6
        #define S3 7
        #define sensorOut 8
        int redFrequency = 0;


        void Servo_0()
        {

         digitalWrite(SERVO_PIN,HIGH);
         delayMicroseconds(500);

          digitalWrite(SERVO_PIN,LOW);
          delayMicroseconds(10000);
          delayMicroseconds(9500);
          }
        void setup() {
          Serial.println(F("DHTxx test!"));
          dht.begin();
          Wire.begin();
          Serial.println("Initializing I2C devices...");
          accelgyro.initialize();
          Serial.println("Testing device connections...");
          Serial.println(accelgyro.testConnection() ? "MPU6050 connection successful" : "MPU6050 connection failed");

          pinMode(SERVO_PIN,OUTPUT);  // Servo motor
          Servo_0();
          pinMode(trigPin, OUTPUT);
          pinMode(echoPin, INPUT);
          pinMode(S0, OUTPUT);
          pinMode(S1, OUTPUT);
          pinMode(S2, OUTPUT);
          pinMode(S3, OUTPUT);

          pinMode(sensorOut, INPUT);

          digitalWrite(S0,HIGH);
          digitalWrite(S1,LOW);

          Serial.begin(9600);
        }

        void loop() {


          bool low = false;
          bool medium = false;
          bool high = false;
          float t = dht.readTemperature();
          if (isnan(t)) {
            Serial.println(F("Failed to read from DHT sensor!"));
            return;
          }
          else  {
            if(t > 40) { high = true; }
            else if(t > 25) { medium = true; }
            else {low = true; }
          }
          Serial.print(F("%  Temperature: "));
          Serial.print(t);
          Serial.print(F("°C \t"));

          // end temp sensor 

          accelgyro.getMotion6(&raw_ax, &raw_ay, &raw_az, &raw_gx, &raw_gy, &raw_gz);
          Serial.print(" Az: "); Serial.print(raw_az);

          if(abs(raw_ax) > 18000) { high = true; }
            else if(abs(raw_ax) > 10000) { medium = true; }
            else {low = true; }
          //end gyro (accelerometer)


          digitalWrite(trigPin, LOW);
          delayMicroseconds(5);
          digitalWrite(trigPin, HIGH);
          delayMicroseconds(10);
          digitalWrite(trigPin, LOW);
          pinMode(echoPin, INPUT);
          duration = pulseIn(echoPin, HIGH);
          cm = (duration/2) / 29.1;     // Divide by 29.1 or multiply by 0.0343
          Serial.print(cm);
          Serial.print("cm");
          delay(250);

          if(cm < 4) { high = true; }
           else if(t < 50) { medium = true; }
           else {low = true; }

          digitalWrite(S2,LOW);
          digitalWrite(S3,LOW);
          redFrequency = pulseIn(sensorOut, LOW);
          Serial.print("\t R = ");
          Serial.print(redFrequency);
          delay(100);
          digitalWrite(S2,HIGH);
          digitalWrite(S3,HIGH);

          if(redFrequency > 240) { high = true; }
            else if(redFrequency > 100) { medium = true; }
            else {redFrequency = true; }

          digitalWrite(trigPin, LOW);
          delayMicroseconds(5);
          digitalWrite(trigPin, HIGH);
          delayMicroseconds(10);
          digitalWrite(trigPin, LOW);

          // Read the signal from the sensor: a HIGH pulse whose
          // duration is the time (in microseconds) from the sending
          // of the ping to the reception of its echo off of an object.
          pinMode(echoPin, INPUT);
          duration = pulseIn(echoPin, HIGH);

          // Convert the time into a distance
          cm = (duration/2) / 29.1;     // Divide by 29.1 or multiply by 0.0343
          Serial.print("\t Distance :");
          Serial.print(cm);
          Serial.print("cm");
          Serial.println();


           if(high){
            tone(11,14000);}


        }
