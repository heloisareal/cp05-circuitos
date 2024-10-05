# CP05 - EDGE
## Integrantes:
- Heloísa Real - 554535
- Eduardo Dallabella - 556803

## Imagem Circuito Físico
![Image (1)](https://github.com/user-attachments/assets/30bc63d8-51a2-49c1-ac89-096dd7ca7c83)
![Image (3)](https://github.com/user-attachments/assets/850b2654-646c-4d24-b379-b8f381257707)

## Código Arduino
```
#include<DHT.h>
#include<Servo.h>
#include <ArduinoJson.h>

#define DHTPIN 7
#define DHTTYPE DHT11
#define ldrPin A0

int ldrVal = 0;

DHT dht(DHTPIN, DHTTYPE);
Servo myServo;

void setup() {
  dht.begin();
  Serial.begin(9600);
}

void loop() {
  ldrVal = analogRead(ldrPin);

  float temp = dht.readTemperature();
  float umi = dht.readHumidity();

  StaticJsonDocument<100>json;

  json["LDR"] = ldrVal;

  json["Temperatura"] = temp;
  json["Umidade"] = umi;

  serializeJson(json, Serial);
  Serial.println();

  if ( Serial.available() > 0 ){
    char comando = Serial.read();

    if ( comando == '1' ){
      myServo.write(180);
    } else if ( comando == '0' ){
      myServo.write(0);
    }
  }
}
```
## Debug no Nodered
![imagem](https://github.com/user-attachments/assets/f30af7dd-2d0f-44a9-b8ce-6313dc9f3bef)

## Fluxo no Nodered
![imagem (1)](https://github.com/user-attachments/assets/632e17c7-2562-4ed7-aa45-98a48d17bb0e)

## Dashboard Nodered
![imagem (2)](https://github.com/user-attachments/assets/4ea99a07-7aed-428f-accf-f785f9bace65)

## Screenshot Hivemq
![imagem (3)](https://github.com/user-attachments/assets/8d331b37-c7b6-4d35-aef7-8eeae316e59b)



