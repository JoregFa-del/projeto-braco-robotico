#include <Servo.h>

#define portaAltura 5
#define portaGarra 7
#define portaBase 9
#define portaAngulo 11

Servo garra, altura, base, angulo;

int confirma = 0;

void setup() {
  Serial.begin(9600);
  garra.attach(portaGarra);
  altura.attach(portaAltura);
  base.attach(portaBase);
  angulo.attach(portaAngulo);
  
}

void loop() {  

  if(confirma == 0){
    base.write(80);
  }
  for(int pos = 0; pos <= 110; pos++){
    angulo.write(pos);
    Serial.print("Angulo: ");
    Serial.println(pos);
    delay(25);
    if (pos >= 60 && pos <= 70){
      altura.write(pos);
      Serial.print("Altura: ");
      Serial.println(pos);
    }
    if(pos > 80) {
      garra.write(60);
    }
  }
  for(int pos = 60; pos <= 110; pos++) {
    garra.write(pos);
    delay(15);
  }
  

  delay(1000);
  
  for(int pos = 110; pos >= 0; pos--){
    angulo.write(pos);
    delay(25);
    if (pos >= 60 && pos <= 70){
      altura.write(pos);
    }
  }

  for(int pos = 80; pos >= 0; pos--) {
    base.write(pos);
    delay(10);
  }

  for (int pos = 0; pos <= 50; pos++) {
    angulo.write(pos);
    delay(25);
  }
  
  for(int pos = 110; pos >= 60; pos--) {
    garra.write(pos);
    delay(15);
  }

  for(int pos = 50; pos >= 0; pos--) {
    angulo.write(pos);
    delay(15);
  }

  for(int pos = 0; pos <= 80; pos++) {
    base.write(pos);
    delay(10);
  }
  confirma = 1;
}
