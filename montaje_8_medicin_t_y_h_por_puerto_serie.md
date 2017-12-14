
# Montaje 8 Medición T y H por puerto serie

### Programa con DHT11:

```cpp
#include "DHT.h"
#define DHTPIN 2   
#define DHTTYPE DHT11   // DHT 11 
DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(9600); 
  dht.begin();
}

void loop() {
  delay(2000);
  float h = dht.readHumidity();
  float t = dht.readTemperature();
  if (isnan(h) || isnan(t)) {
    Serial.println("Fallo al leer el sensor DHT11");
    return;
  }
  Serial.print("Humedad: "); 
  Serial.print(h);
  Serial.print(" \t");
  Serial.print("Temperatura: "); 
  Serial.print(t);
  Serial.println(" ºC ");
}
```

El resultado se puede ver en este vídeo, simplemente soplando el vaho pasamos de 20% de humedad y 22ºC a 93% y 24ºC.

Si lo hacéis con niños, enseguida se les ocurre ponerlo en el sobaco ;)

{% youtube %}https//www.youtube.com/watch?v=gLxdSaxOJbY?rel=0{% endyoutube %}

### Programa con DHT12

La librería de este sensor es más potente y nos puede decir la sensación térmica:

```cpp
// Example sketch for DHT22 humidity - temperature sensor
// Written by cactus.io, with thanks to Adafruit for bits of their library. public domain

#include "cactus_io_DHT22.h"

#define DHT22_PIN 2     // what pin on the arduino is the DHT22 data line connected to

// For details on how to hookup the DHT22 sensor to the Arduino then checkout this page
// http://cactus.io/hookups/sensors/temperature-humidity/dht22/hookup-arduino-to-dht22-temp-humidity-sensor

// Initialize DHT sensor for normal 16mhz Arduino. 
DHT22 dht(DHT22_PIN);
// Note: If you are using a board with a faster processor than 16MHz then you need
// to declare an instance of the DHT22 using 
// DHT22 dht(DHT22_DATA_PIN, 30);
// The additional parameter, in this case here is 30 is used to increase the number of
// cycles transitioning between bits on the data and clock lines. For the
// Arduino boards that run at 84MHz the value of 30 should be about right.

void setup() {
  Serial.begin(9600); 
  Serial.println("DHT22 Humidity - Temperature Sensor");
  Serial.println("RH\t\tTemp (C)\tTemp (F)\tHeat Index (C)\t Heat Index (F)");
 
  dht.begin();
}

void loop() {
  // Reading temperature or humidity takes about 250 milliseconds!
  // Sensor readings may also be up to 2 seconds 'old' (its a very slow sensor)
  dht.readHumidity();
  dht.readTemperature();
  
  // Check if any reads failed and exit early (to try again).
  if (isnan(dht.humidity) || isnan(dht.temperature_C)) {
    Serial.println("DHT sensor read failure!");
    return;
  }
 
  Serial.print(dht.humidity); Serial.print(" %\t\t");
  Serial.print(dht.temperature_C); Serial.print(" *C\t");
  Serial.print(dht.temperature_F); Serial.print(" *F\t");
  Serial.print(dht.computeHeatIndex_C()); Serial.print(" *C\t");
  Serial.print(dht.computeHeatIndex_F()); Serial.println(" *F");
  
  // Wait a few seconds between measurements. The DHT22 should not be read at a higher frequency of
  // about once every 2 seconds. So we add a 3 second delay to cover this.
  delay(3000);
}
```

El resultado es:

![](img/img0.3.png)
