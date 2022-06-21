//AUTOMAÇÃO RESIDENCIAL - MECATRÔNICA - SISTEMA DE ALARME DE FUMAÇA, VAZAMENTO DE GÁS GLP E CHAMA

//sensor gas 
int pinSensor = A0; //Pino Sensor
int Rele = 3; //Pino Relé
int Buzzer = 13; //Pino Buzzer
int var = 0;
int ValDesarm = 20; //Variável para selecionar a quantidade de Gás/Fumaça detectada
int valor = 0;

//sensor de incendio
int Sensor = 2;
int Buzzer2 = 13; 
int Var = 0;


void setup()
{
 Serial.begin(9600); //Inicia porta Serial em 9600 baud
 pinMode(Rele, OUTPUT);
 pinMode(Buzzer, OUTPUT);
 Serial.println("CONTROLE DE FUMAÇA E VAZAMENTO DE GÁS");

//sensor de incendio

 pinMode(Buzzer2, OUTPUT);
 pinMode(Sensor, INPUT);
 Serial.begin(9600);

 
}
 
void loop()
{
 valor = analogRead(pinSensor); //Faz a leitura da entrada do sensor
 valor = map(valor, 0, 1023, 0, 100); //Faz a conversão da variável para porcentagem
 
 Serial.println(valor); //Escreve o valor na porta Serial
 if (valor>=ValDesarm){ //Condição, se valor continuar maior que ValDesarm faça:
 digitalWrite(Rele, HIGH); //Liga relé para solenóide
 digitalWrite(Buzzer, HIGH); //Dispara alarme de vazamento ou possível incêndio
 Serial.println("Alarme disparado!!!"); //Apresenta mensagem na porta serial
 delay(1000); //Tempo de disparo do alarme
 digitalWrite(Buzzer, LOW); //Desliga o alarme
 delay(2000); //Aguarda
 //Ligando o Buzzer com uma frequencia de 1500 hz.
  tone(Buzzer,1500);   
  delay(500);
   
  //Desligando o buzzer.
  noTone(Buzzer);
  delay(500);
 }else{
 digitalWrite(Rele, LOW); //Caso contrário permaneça com o relé desligado
 }
 delay(1000);

//sensor de incendio
Var=digitalRead(Sensor);
 Serial.print(Var);
 if(Var<1) 
 {

 //Ligando o buzzer com uma frequencia de 1500 hz.
  tone(Buzzer2,1500);   
  delay(500);
   
  //Desligando o buzzer.
  noTone(Buzzer2);
  delay(500);
  
 digitalWrite(Buzzer2, HIGH); 
 delay(100);
 digitalWrite(Buzzer2, LOW);
 delay(20);
 
 }
}
