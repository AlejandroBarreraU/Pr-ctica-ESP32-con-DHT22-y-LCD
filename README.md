# Práctica ESP32 con DHT22 y LCD
## Introducción 
En esta práctica utilizaremos la ESP32 como entorno de adquision de datos, por lo tanto se utilizará un sensor DTH11 para obtener datos de temperatura y humedad del entorno; también una pantalla LCD para vizualizar los datos del progrema. Como dato adicional, se utilizara WOKI para asimular esta práctica.
## Material a utlizar
+ WOKWI
+ Tarjeta ESP 32
+ Sensor DHT22
+ LCD 16 x 2 (IC2)
## Programación
```
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int DHT_PIN = 15;

DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();

}

void loop() {

  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  
  lcd.setCursor(0, 0);
  lcd.print("  Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
  lcd.print("Wokwi Online IoT");

  delay(1000);
}
```
## Librerias a utilizar
1. DHT sensor library for ESPx
   
   ![](https://github.com/AlejandroBarreraU/PracticESP32conDHT22yLCD/blob/main/instalar%20librerias.png?raw=true)
2. LiquidCrystal I2C
   
   ![](https://github.com/AlejandroBarreraU/PracticESP32conDHT22yLCD/blob/main/instalar%20librerias%202.png?raw=true)
## Instrucciones 
1. Agrega el sensor DHT22.
   
   ![](https://github.com/AlejandroBarreraU/PracticESP32conDHT22yLCD/blob/main/agregar%20sensor.png?raw=true)
2. Agrega LCD.
   
   ![](https://github.com/AlejandroBarreraU/PracticESP32conDHT22yLCD/blob/main/agrear%20lcd.png?raw=true)
## Conexiones
Se realizan las conexiones como se viasualiza en la imagen.

![](https://github.com/AlejandroBarreraU/PracticESP32conDHT22yLCD/blob/main/conexiones%202.png?raw=true)
## Resultados
Una vez ejecutado el programa se mostrarán datos de temperatura y humedad en la pantalla.

![](https://github.com/AlejandroBarreraU/PracticESP32conDHT22yLCD/blob/main/resultados.png?raw=true)
## Créditos
Elaborado por el Ing. Alejandro Barrera
