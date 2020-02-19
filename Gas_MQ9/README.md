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
## AirQua
|Low|Medium|High|
|---------|--------|----------|
|47.00 PPM-67.00 PPM|67.00 PPM-85.00 PPM|85.00 PPM-114.00 PPM|
