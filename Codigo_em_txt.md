# projeto-braco-robotico
Projeto de braço robótico para Projeto Integrador II-b


#include <Servo.h>

//Cria as portas digitias dos servos
#define servoBase 11
#define servoAngulo 9
#define servoAltura 7
#define servoGarra 5

//Fica pra depois
/*Cria as variáveis para os botões 
#define botaoPara A0
#define botaoContinua */

//Define os objetos
Servo base,altura, angulo, garra;

//Cria as variáveis para o controle do ângulo (por não ter potenciômetro, será manual, simulando uma entrada analógica)
//Valores entre 0 e 1024
int valorPotBase, valorPotAltura, valorPotAngulo;
int valorPotGarra;

//Cria as variáveis que armazenarão os valores dos ângulos de cada servos
int valorAngBase;
int valorAngAltura;
int valorAngAngulo;
int valorAngGarra;
 
void setup() {
  Serial.begin(9600); 

  //Define as portas dos servos
  base.attach(servoBase);
  altura.attach(servoAltura);
  angulo.attach(servoAngulo);
  garra.attach(servoGarra);
    
}

void loop() {
  while (true){ //Sempre entrará no while
    //Definição dos valores simulados do pontenciômetro
    valorPotBase = random(200, 400); //Base
    valorPotGarra = random(200, 400); //Altura
    valorPotAngulo = random(200, 400); //Ângulo
    valorPotAltura = random(200, 400); //Garra
    
    if ((valorPotBase || valorPotAltura || valorPotAngulo || valorPotGarra ) < 0 || (valorPotBase || valorPotAltura || valorPotAngulo || valorPotGarra ) > 1024 ) { break; } //Se os valores do potenciômetro forem diferentes da faixa permitida, sairá do while

    //Mapeamento dos valores
    valorAngBase = map(valorPotBase, 0, 1024, 0, 180);
    valorAngAngulo = map(valorPotAngulo, 0, 1024, 0, 180); 
    valorAngAltura = map(valorPotAltura, 0, 1024, 0, 180); 
    valorAngGarra = map(valorPotGarra, 0, 1024, 0, 180);

    //Envia os valores para os respectivos servos
    base.write(valorAngBase); //Base
    delay(100);
    angulo.write(valorAngAngulo); //Angulo
    delay(100);
    altura.write(valorAngAltura); //Altura
    delay(100);
    garra.write(valorAngGarra); //Garra
    delay(1000);
  }
}
