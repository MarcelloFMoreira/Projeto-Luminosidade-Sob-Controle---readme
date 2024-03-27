# Projeto-Luminosidade-Sob-Controle-readme

## Sobre o projeto
Esse projeto utiliza tecnologia de sensoriamento para medir a luminosidade do ambiente, oferecendo um controle preciso sobre as condições de iluminação ideais para o armazenamento de vinhos. Ao manter as condições ideais de iluminação, nosso projeto ajuda a preservar as propriedades e o sabor dos vinhos, protegendo-os da exposição excessiva à luz que pode deteriorar sua qualidade ao longo do tempo.


## Layout do circuito no tinkercad
![Layout do circuito](https://github.com/MarcelloFMoreira/Projeto-Luminosidade-Sob-Controle---readme/blob/main/Simulador%20de%20circuito%20.png)

## Equipamentos utilizados
-Arduino UNO R3.
-Placa de ensaio.
-LDR (Fotorresistor).
-Resistores.
-Leds Verde, Amarelo, Vermelho.
-Modulo de som Buzzer.
-cabos jumpers

## Code

int LEDAMARELO = 7;     // DECLARAÇÃO DO LED AMARELO
int LEDVERMELHO = 8;    // DECLARAÇÃO DO LED VERMELHO
int LEDVERDE = 13;      // DECLARAÇÃO DO LED VERDE
int BOZINA = 4;        // DECLARAÇÃO DO SISTEMA DE BOZINA
int intencidadeluz;     // DECLARAR VARIAVEL DE INTENSIDADE DA LUZ PARA POSTERIORMENTE CONVERTER DE 0 A 100

void setup () {
  Serial.begin(9600);                 // INICIANDO COMUNICAÇÃO SERIAL 
  pinMode(LEDAMARELO, OUTPUT);        // DECLARADO LED COMO DISPOSITIVO DE SAÍDA
  pinMode(LEDVERMELHO, OUTPUT);       // DECLARADO LED COMO DISPOSITIVO DE SAÍDA 
  pinMode(LEDVERDE, OUTPUT);          // DECLARADO LED COMO DISPOSITIVO DE SAÍDA 
  pinMode(BOZINA, OUTPUT);            // DECLARADO BOZINA COMO DISPOSITIVO DE SAÍDA
  pinMode(A0, INPUT);                 // DECLARANDO O LDR COMO DISPOSITIVO DE ENTRADA
}

void loop() {
  int LDR = analogRead(A0);                   // LENDO O VALOR DA PORTA ANALÓGICA (A0) DO ARDUINO, PORTA ESSA CONECTADA AO LDR NESSE EXEMPLO
  intencidadeluz = map(LDR, 0, 1023, 0, 100); // CONVERTER A LEITURA DO LDR DE 0 A 100
  Serial.println(intencidadeluz);             // APARECER NO MONITOR O VALOR DE 0  A 100

  if (intencidadeluz < 40) {
    digitalWrite(LEDVERDE, HIGH);    // LED VERDE ACENDER SE O VALOR DA LDR FOR MENOR QUE 40
  } else {
    digitalWrite(LEDVERDE, LOW);     // LED VERDE DESLIGAR SE "IF" FOR FALSO
  }

  if (intencidadeluz > 39 && intencidadeluz < 50) {
    digitalWrite(LEDAMARELO, HIGH);  // LED AMARELO ACENDER SE O VALOR DA LDR FOR MAIOR QUE 39 E MENOR QUE 50
    tone(BOZINA, 500, 1000);         // BOZINA REALIZAR EFEITO SONORO
    delay(3000);                     // TEMPO DE PAUSA DO EFEITO SONORO
  } else {
    digitalWrite(LEDAMARELO, LOW);   // LED AMARELO DESLIGAR SE "IF" FOR FALSO
    digitalWrite(BOZINA, LOW);       // BOZINA NÃO REALIZA EFEITO SONORO SE "IF" FOR FALSO
  }

  if (intencidadeluz > 49) {
    digitalWrite(LEDVERMELHO, HIGH); // LED VERMELHO ACENDER SE O VALOR DA LDR FOR MAIOR QUE 49
    tone(BOZINA, 1000);              // BOZINA REALIZAR EFEITO SONORO
    
   
  } else {
    digitalWrite(LEDVERMELHO, LOW);  // LED VERMELHO DESLIGAR SE "IF" FOR FALSO
    digitalWrite(BOZINA, LOW);       // BOZINA NÃO REALIZA EFEITO SONORO SE "IF" FOR FALSO
  }

  delay(500);
}


