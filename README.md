# DHT22-CON-ULTRASONICO-CON-LCD-BIEN

Este repositorio muestra como podemos programar una ESP32 con el sensor DHT22, con sensor ultrasonico y una lcd.

# Introducción
Descripción
La Esp32 la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un sensor (DTH11) para adquirir temperatura y humedad del entorno; Cabe aclarar que esta practica se usara un simulador llamado WOKWI.

# Material Necesario
Para realizar esta practica necesitas lo siguiente

- WOKWI
- Tarjeta ESP 32
- Sensor DHT22
- sensor ultrasonico
- Display lcd


# Instrucciones
Requisitos previos
Para poder usar este repositorio necesitas entrar a la plataforma WOKWI.

Instrucciones de preparación de entorno
Abrir la terminal de programación y colocar la siguente programación:

```
//PROGRAMA COMBINADOS DHT22 CON ULTRASONICO y lcd
#include <LiquidCrystal_I2C.h> //Libreria de LCD
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
#include "DHTesp.h" //Libreria de DHT
const int Trigger = 4;   //Pin digital 4 para el Trigger del sensor
const int Echo = 2;   //Pin digital 2 para el Echo del sensor
const int DHT_PIN = 15; //pin del sensor de temperatura
DHTesp dhtSensor;
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0

}

void loop() {

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
 
  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  //delay(2000); 
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  Serial.println("---");
  delay(2000);          //Hacemos una pausa de 200ms

  lcd.clear(); 
  lcd.setCursor(3, 0); //coordenadas del LCD 
  lcd.print("MODULO V");
  lcd.setCursor(1, 1);
  lcd.print("AUTOMATIZACION");
 delay(2000);

lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("IVAN ZAGAL");
  lcd.setCursor(2, 1);
  lcd.print("ING MECANICA");
  delay(2000);

 lcd.clear(); 
  lcd.setCursor(0, 0);
  lcd.print("  Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
  delay(2000);

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Distancia: " + String(d) + "cm");
  delay(2000);

}
 

```

CARGAMOS LAS SIGUIENTES LIBRERIAS

![](https://github.com/IVANZAGAL996/DHT22-CON-ULTRASONICO-CON-LCE-BIEN/blob/main/librerias.png)

INSERTAMOS EL DHT22

![](https://github.com/IVANZAGAL996/DHT22-CON-ULTRASONICO-CON-LCE-BIEN/blob/main/dht22.png)

INSERTAMOS EL SENSOR ULTRASONICO

![](https://github.com/IVANZAGAL996/DHT22-CON-ULTRASONICO-CON-LCE-BIEN/blob/main/ultrasonico.png)

INSERTAMOS EL DISPLAY LCD

![](https://github.com/IVANZAGAL996/DHT22-CON-ULTRASONICO-CON-LCE-BIEN/blob/main/lcd.png)



REALIZAMOS LA SIGUIENTE CONEXION

![](https://github.com/IVANZAGAL996/DHT22-CON-ULTRASONICO-CON-LCE-BIEN/blob/main/diagrama%20de%20conexion.png)

INICIAMOS LA SIMULACION Y OBSRRVAREMOS LOS RESULTASDOS EN EL MONITOR SERIAL.

REULTADOS TEMPERATURA Y HUMEDAD

![](https://github.com/IVANZAGAL996/DHT22-CON-ULTRASONICO-CON-LCE-BIEN/blob/main/resultados%20temp%20y%20humedad.png)

RESULTADOS DISTANCIA

![](https://github.com/IVANZAGAL996/DHT22-CON-ULTRASONICO-CON-LCE-BIEN/blob/main/Captura%20de%20pantalla%20(101).png)


# CREDITOS
Elaborado por:
EDGAR IVAN PROSPERO ZAGAL PONCE
[GitHub](https://github.com/IVANZAGAL996/DHT22-CON-ULTRASONICO-CON-LCE-BIEN/tree/main)



