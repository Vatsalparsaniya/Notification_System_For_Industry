

## Code

            
              #define SERVO_PIN 8

              int trigPin = 11;    // Trigger
              int echoPin = 12;    // Echo
              long duration, cm, inches;


              void Servo_0()
              {
                pinMode(trigPin, OUTPUT);
                pinMode(echoPin, INPUT);
                digitalWrite(SERVO_PIN,HIGH);
                delayMicroseconds(500);

                digitalWrite(SERVO_PIN,LOW);
                delayMicroseconds(10000);
                delayMicroseconds(9500);
                }
              void setup() {
                Serial.begin(9600);
              pinMode(SERVO_PIN,OUTPUT);  // Servo motor
              Servo_0();
              }

              void loop()
              {
               uint16_t pos;
               for(pos=500;pos<=2500;pos+=5)
               {
              Serial.print("Pulse Width(usec)==> ");Serial.print(pos,DEC);
                digitalWrite(SERVO_PIN,HIGH);
                delayMicroseconds(pos);
                //off
                digitalWrite(SERVO_PIN,LOW);
                delayMicroseconds(10000);
                delayMicroseconds(10000-pos);
                // Get Distance
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
                inches = (duration/2) / 74;   // Divide by 74 or multiply by 0.0135
                Serial.print("      Measured Distance : ");
                Serial.print(inches);
                Serial.print("in, ");
                Serial.print(cm);
                Serial.print("cm");
                Serial.println();

                delay(100);
               }
              }


## Thread Level

|Low|Medium|High|
|-----|-------|------|
|300CM-400CM|100CM-300CM|2CM-100CM|
