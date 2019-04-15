# Atividade_Trainee
Última tarefa para os participantes do processo de trainee da equipe CEFAST Aerospace
## Sistema de envio de dados
Para finalizarmos o processo de trainee, os participantes deverão simular um sistema básico de comunicação com um cubeSat **_utilizando a linguagem que preferir._**
A tarefa será repartida em partes e o cumprimento de cada uma será classificatório.Não é necessário o cumprimento de toda a tarefa.
### Enviar uma mensagem-Nivel 1
No projeto atual, a equipe está utilizando o módulo GPRS para envio e recebimento de mensagens.Um algoritmo para isso:
```
#include <SoftwareSerial.h>
 
//SIM800 TX is connected to Arduino D8
#define SIM800_TX_PIN 8
 
//SIM800 RX is connected to Arduino D7
#define SIM800_RX_PIN 7
 
//Create software serial object to communicate with SIM800
SoftwareSerial serialSIM800(SIM800_TX_PIN,SIM800_RX_PIN);
 
void setup() {
  //Begin serial comunication with Arduino and Arduino IDE (Serial Monitor)
  Serial.begin(9600);
  while(!Serial);
   
  //Being serial communication witj Arduino and SIM800
  serialSIM800.begin(9600);
  delay(1000);
   
  Serial.println("Setup Complete!");
  Serial.println("Sending SMS...");
   
  //Set SMS format to ASCII
  serialSIM800.write("AT+CMGF=1\r\n");
  delay(1000);
 
  //Send new SMS command and message number
  serialSIM800.write("AT+CMGS=\"07194XXXXX\"\r\n");
  delay(1000);
   
  //Send SMS content
  serialSIM800.write("TEST");
  delay(1000);
   
  //Send Ctrl+Z / ESC to denote SMS message is complete
  serialSIM800.write((char)26);
  delay(1000);
     
  Serial.println("SMS Sent!");
}
 
void loop() {
}
```
Percebe-se que o algoritmo prepara o comando antes de comunicar com o módulo adicionando vários aspectos sobre a mensagem:
```
//Set SMS format to ASCII
  serialSIM800.write("AT+CMGF=1\r\n");
  delay(1000);
 
  //Send new SMS command and message number
  serialSIM800.write("AT+CMGS=\"07194XXXXX\"\r\n");
  delay(1000);
```
Após essa etapa a mensagem é adicionada ao comando e é adiconando o sinal de que este está pronto para ser enviado ao módulo:
```
//Send SMS content
  serialSIM800.write("TEST");
  delay(1000);
   
  //Send Ctrl+Z / ESC to denote SMS message is complete
  serialSIM800.write((char)26);
  delay(1000);
  ```
  Nessa etapa do Sistema de comunicação de dados iremos simular isso.
  ### Deverá ser impresso no console o comando com a mensagem que seria enviado para o Monitor Serial caso o módulo estivesse conectado.
  
  ## Utilizar medicoes de algum outro componente-Nivel 2
  Comunicar com o satélite não é suficiente para as competições.O satélite deve ter várias funcionalidades para torna-lo útil na realização de missões,como medir a umidade e temperatura do ambiente,calcular a posição do sol,identificar áreas de desmatamento...
  Logo é essencial que essas informações estejam na mensagem a ser enviada.
  ### Para simular isso vocês deverão criar as funções(no código principal ou em uma biblioteca seprada) que retornam possiveis valores caso a função utilizada fosse a da biblioteca do módulo.Exemplo para o módulo acelerometro:
  ```
  x = accelero.getXRaw();
  y = accelero.getYRaw();
  z = accelero.getZRaw();
  ```
  Uma forma seria criar essas funcoes retornando possiveis valores para as variaceos dos eixos X,Y,Z.**_Instanciar uma classe que possua essas funções será um diferencial._**
  ## Salvar uma imagem codificada-Nivel 3
   ### Ler um arquivo de imagem e codifica-lo em uma string.(Dica existem varias formas de codificar uma imagem, uma delas é o base64).
  ## Enviar uma imagem codificada-Nivel 4
  ### Após codificar uma imagem, a quantidade de caracteres é exorbitante,nessa etapa voces devem pensar em uma forma de envia-la como mensagem.
  ## Criar um sistema de segurança
   ### Exigir processos de autenticação para autorizar o envio das mensagens.
  ## Criar um interface para comunicação
   ### O usuário poderá escolher o que gostaria de receber.
   **_possibilitar que a mensagem seja recebida com determinada frequencia será um diferencial_**
   
   ## A atividade será em dupla.
   Vocês serão separados em duplas.A comunicação será muito importante, além disso a metodologia da dupla(como vocês se organizaram para fazer) será questionada na entrega do trabalho.
    As duplas serão: 
   ### Dupla 1
   Samir e Isabela.
   ### Dupla 2
   Rodrigo Gomes e Pedro.
   ### Dupla 3
   Leonardo e Maria Eduarda.
   
   **A entrega deverá ser enviada para o email _sinvalvieirajunior@gmail.com_ até o dia 22/04/2019.**
  

