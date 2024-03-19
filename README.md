# Projeto-Luminosidade-Sob-Controle---readme

##Sobre o projeto
https://www.tinkercad.com/things/e7X3DGEGJlz-projeto-tomando-um-bom-vinho?sharecode=8zcw5fM7bqEihR8_0OuBUqnGdH8Xyher58addA0ScLg
Esse projeto propõe uma solução que garante a qualidade de armazenamento de vinho através da medição precisa da luminosidade ambiente. 

##Code
int LEDAMARELO = 7;  // DECLARAÇÃO DO LED AMARELO
int LEDVERMELHO = 8; // DECLARAÇÃO DO LED VERMELHO
int LEDVERDE = 13;   // DECLARAÇÃO DO LED VERDE
int BOZINA = 2;      // DECLARAÇÃO DO SISTEMA DE BOZINA

void setup () {
Serial.begin(9600); // INICIANDO COMUNICAÇÃO SERIAL PARA LER VALORES DO DISPOSITIVO LDR
pinMode(LEDAMARELO, OUTPUT);  // DECLARADO LED COMO DISPOSITIVO DE SÁIDA
pinMode(LEDVERMELHO, OUTPUT); // DECLARADO LED COMO DISPOSITIVO DE SÁIDA 
pinMode(LEDVERDE, OUTPUT);    // DECLARADO LED COMO DISPOSITIVO DE SÁIDA 
pinMode(BOZINA, OUTPUT);      // DECLARADO BOZINA COMO DISPOSITIVO DE SÁIDA
}

void loop() {
int LDR = analogRead (A0);
Serial.println(LDR); // LENDO O VALOR DA PORTA ANALOGICA (A0) DO ARDUINO, PORTA ESSA CONECTADA AO LDR NESSE EXEMPLO

if(LDR<320)
  digitalWrite(LEDVERDE,HIGH); // LED VERDE ACENDER SE O VALOR DA LDR FOR MENOR QUE 320
else
  digitalWrite(LEDVERDE,LOW); // LED VERDE DESLIGAR SE "IF" FOR FALSO
    
if(LDR>319 && LDR<640)
  digitalWrite(LEDAMARELO,HIGH); // LED AMARELO ACENDER SE O VALOR DA LDR FOR MAIOR QUE 319 E MENOR QUE 640 
else
  digitalWrite(LEDAMARELO,LOW); // LED AMARELO DESLIGAR SE "IF" FOR FALSO
    
if(LDR>639)
{
  digitalWrite(LEDVERMELHO,HIGH);          // LED VERMELHO ACENDER SE O VALOR DA LDR FOR MAIOR QUE 639
  tone(BOZINA, 1000, 3000); delay(5000);  //  BOZINA REALIZAR EFEITO SONORO SE O VALOR DA LDR FOR MAIOR QUE 639 
}
else
{
  digitalWrite(LEDVERMELHO,LOW);// LED VERMELHO DESLIGAR SE "IF" FOR FALSO
  digitalWrite(BOZINA,LOW);    // BOZINA NÃO REALIZA EFEITO SONORO SE "IF" FOR FALSO
} 
delay(500);
}

##Layout do circuito
![Layout do circuito](https://github.com/MarcelloFMoreira/Projeto-Luminosidade-Sob-Controle---readme/blob/main/Simulador%20de%20circuito%20.png)
