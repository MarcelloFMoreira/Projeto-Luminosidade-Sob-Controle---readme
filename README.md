# Projeto-Luminosidade-Sob-Controle-readme

## Sobre o projeto
Esse projeto utiliza tecnologia de sensoriamento para medir a luminosidade do ambiente, oferecendo um controle preciso sobre as condições de iluminação ideais para o armazenamento de vinhos. Ao manter as condições ideais de iluminação, nosso projeto ajuda a preservar as propriedades e o sabor dos vinhos, protegendo-os da exposição excessiva à luz que pode deteriorar sua qualidade ao longo do tempo.


## Layout do circuito no tinkercad
Link para visualização direto do software tinkercad: https://www.tinkercad.com/things/e7X3DGEGJlz-projeto-luminosidade-sob-controle
![Layout do circuito](https://github.com/MarcelloFMoreira/Projeto-Luminosidade-Sob-Controle---readme/blob/main/Simulador%20de%20circuito%20.png)

## Equipamentos utilizados
-Arduino UNO R3.
-Placa de ensaio.
-LDR (Fotorresistor).
-Resistores.
-Leds Verde, Amarelo, Vermelho.
-Modulo de som Buzzer.
-cabos jumpers

![Layout do circuito](https://github.com/MarcelloFMoreira/Projeto-Luminosidade-Sob-Controle---readme/blob/main/Equipamentos%20utilizados.jpeg)

## Code

int LEDAMARELO = 7;     // DECLARAÇÃO DO LED AMARELO
int LEDVERMELHO = 8;    // DECLARAÇÃO DO LED VERMELHO
int LEDVERDE = 13;      // DECLARAÇÃO DO LED VERDE
int BUZINA = 4;         // DECLARAÇÃO DO SISTEMA DE BUZINA
int intencidadeluz;     // DECLARAR VARIAVEL DE INTENSIDADE DA LUZ PARA POSTERIORMENTE CONVERTER DE 0 A 100

void setup() {
  Serial.begin(9600);                 // INICIANDO COMUNICAÇÃO SERIAL 
  pinMode(LEDAMARELO, OUTPUT);        // DECLARADO LED COMO DISPOSITIVO DE SAÍDA
  pinMode(LEDVERMELHO, OUTPUT);       // DECLARADO LED COMO DISPOSITIVO DE SAÍDA 
  pinMode(LEDVERDE, OUTPUT);          // DECLARADO LED COMO DISPOSITIVO DE SAÍDA 
  pinMode(BUZINA, OUTPUT);            // DECLARADO BUZINA COMO DISPOSITIVO DE SAÍDA
  pinMode(A0, INPUT);                 // DECLARANDO O LDR COMO DISPOSITIVO DE ENTRADA
}

void loop() {
  int LDR = analogRead(A0);                   
  intencidadeluz = map(LDR, 49, 969, 0, 100); 
  Serial.println(intencidadeluz);             

  digitalWrite(LEDVERDE, intencidadeluz < 40); // Ligar LED verde se a intensidade da luz for menor que 40

  if (intencidadeluz >= 40 && intencidadeluz < 50) {
    digitalWrite(LEDAMARELO, HIGH);  
    tone(BUZINA, 500); // Produzir som com frequência de 500 Hz
    delay(1000); // Aguardar 1 segundo
    noTone(BUZINA); // Desligar som
  } else {
    digitalWrite(LEDAMARELO, LOW);   
  }

  if (intencidadeluz >= 50) {
    digitalWrite(LEDVERMELHO, HIGH); 
    tone(BUZINA, 1000); // Produzir som com frequência de 1000 Hz
  } else {
    digitalWrite(LEDVERMELHO, LOW);  
    noTone(BUZINA); // Desligar som
  }

  delay(500);
}

## Funcionalidade do circuito na prática

https://github.com/MarcelloFMoreira/Projeto-Luminosidade-Sob-Controle---readme/assets/161846509/1c62a4c1-777d-4172-b651-c15abb6553da

