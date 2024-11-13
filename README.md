// se incluyen librerías
#include <DHT.h>
#include <LiquidCrystal.h>

// se define el pin del sensor DHT y su tipo
#define DHTPIN A0
#define DHTTYPE DHT11
DHT dht(DHTPIN, DHTTYPE);

//Inicializar el displau LDC
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

//variable de la temperatura
float temperature;

//define el pin de la peltier y umbral de tem
#define PELTIER_PIN 9
#define TEMP_THRESHOLD 4// objetivo de temperatura

void setup() {
  lcd.begin(16, 2);
  dht.begin();
  pinMode(PELTIER_PIN, OUTPUT);
}

void loop() {
 temperature = dht.readTemperature();

  //mostrar la temperatura en el LCD
  lcd.setCursor(0, 0);
  lcd.print("Temp: ");
  lcd.print(temperature);
  lcd.print(" C");

//Control de la peltier
  if (temperature < TEMP_THRESHOLD) {
    digitalWrite(PELTIER_PIN, HIGH); 
  }
 else {
    digitalWrite(PELTIER_PIN, LOW); 
  }

  delay(2000); 
}
