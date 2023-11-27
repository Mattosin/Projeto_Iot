#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);

int sensorPin = 2; // Pino do sensor de corrente
float sensibilidade = 0.2; // Sensibilidade do sensor (ajuste conforme o seu sensor)

void setup() {
  lcd.init();  // Inicializa o LCD com 16 colunas e 2 linhas
  lcd.backlight();
  lcd.clear();	
  lcd.print("Corrente:      A");
}

void loop() {
  int sensorValue = sensorPin;
  float corrente = (sensorValue / 1023.0) * 500.0 / sensibilidade; // Leitura da corrente em Ampere

  lcd.setCursor(10, 0); // Posicione o cursor na coluna 10 (após "Corrente: ")
  lcd.print("     "); // Limpe o valor anterior
  lcd.setCursor(10, 0);
  lcd.print(corrente , 1); // Exibe a corrente com 2 casas decimais

  delay(1000); // Aguarde um segundo antes de ler novamente
}
