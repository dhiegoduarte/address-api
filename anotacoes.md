# POC Vivo
https://docs.google.com/presentation/d/17wo6moggKGOv9-JpOAxVAkPnjkNRm-3u68ReBmDYb0g/edit?ts=5f15b00a#slide=id.g86704c6399_0_1

## Marcelo
## Slide 1, 2, 3, 4, 5, 6, 7

## Slide 8 - Chrome
Para os casos de uso 3 e 4, referentes a publish subscribe e SAGA, nos preparamos um cenário que vai abordar os seguintes tópicos:
Processamento assíncrono 
Mensajeria 
Controle de transação
Deploy híbrido

## Slide 9 - Chrome
O cenário implementado é a realizacao da ordem de compra de produto, através de crédito pré-pago, onde o fluxo é:

- O Microservico Orders recebe uma ordem de compra, realiza uma transacao local salvando as informações dessa ordem e publica uma mensagem de ordem criada.
- O microserviço Customer Credit consome a mensagem de ordem criada e valida se o cliente tem crédito para realizar a compra do produto. Se o cliente possuir credito suficiente, uma mensagem de credito reservado é publicada. Se o cliente não possuir credito suficiente uma mensagem de credito excedido é publicada.
- O microserviço Orders então é notificado e se o credito foi reservado com sucesso a ordem é processada ou se o credito foi excedido o rollback da ordem é executado.

Até aqui tudo bem? Alguma dúvida?

Os componentes que fazem parte dessa solução são:

## MQ - Firefox
As filas. Neste caso estamos usando o serviço de mensageria na nuvem da plataforma Anypoint mas poderiamos estar usando qualquer serviço de mensageria como Kafka por exemplo.

## Runtime manager - Firefox
E os dois microserviços que são o Orders que esta sendo executado em um servidor on-premise e o Customer credit que está sendo executado na nuvem.

Até aqui tudo bem? Alguma dúvida?

## Slide 9 - Chrome
Entao agora nos vamos demonstrar o funcionamento do cenário onde o cliente possui credito. Em um cenário real normalmente a transacoes seriam registros no banco de dados do microserviço, mas para a POC, para demonstrar de uma forma bem visual, as transacoes locais serao representadas com a geracao de um arquivo no file system.

## Postman + Finder
Orders 50, 30, 20 

Agora o cliente não tem mais credito entao a proxima ordem tera sua transacao local criada e logo em seguida com a notificacao do servico Customer Credit que o cliente possui credito excedido sera efetuado o rollback dessa transacao, ou seja, o arquivo criado será apagado.

## Postman + Finder
Orders 10

## Studio

## Slide 9 - Chrome
Com a implementacao desse cenário a gente consegue demonstrar na prática, que em uma arquitetura de microserviços com transacoes distribuidas, para garantir a consistencia da informacoes entre os diferentes microserviços, a implementacao do design pattern SAGA por coreografia pode ser utilizada.

## Slide 10 - Chrome

---

## Slide 14 - Chrome

- Continuous Integration / Integração Contínua: A integração contínua é a prática de “juntar” rapidamente o código
recém-desenvolvido ao corpo principal que será lançado.
Economizando assim muito tempo quando a equipe está pronta
para realizar uma liberação de uma nova versão. Ela é frequentemente o primeiro
passo no caminho para a maturidade do DevOps. O processo de integração contínua envolve a veri cação do código, a sua compilação
(geralmente executável binário) e a aplicação de alguns testes de
validação.

- Continuous Delivery / Entrega Contínua: A entrega contínua é uma extensão da integração contínua.
Ao executar entregas continuamente, os times adicionam
automação e testes para não apenas mesclar frequentemente o
código, mas também obtê-lo quase pronto para a implantação. Em resumo, é a prática de ter a base de código continuamente em
um estado pronto para implantação em produção pelo time de
operações.

- Continuous Deployment / Implantação Contínua: é a prática de
automatizar todo o caminho até o deploy em produção, isso sem
qualquer intervenção humana. É claro que para alcançar esse
estágio é necessário um alto nível de maturidade dos estágios
anteriores.

- DevOps / Cultura: Mudança cultural e organizacional na empresa. Normalmnte adotando a organização de times multidisciplinares, (squad), com cada profissional responsável por uma estrutura de TI, porém dedicado ao time. Exemplo: desenvolvedor, analista de testes, infraestrutura, segurança etc. 














https://fcatae.visualstudio.com/_git/sonarqube?path=%2Fazure-pipelines.yml




Feedback Diogo: 

- low-code com classes java, implementacao mista.
- perimetros de seguranca e reframe
- parte do HIP como é o server on-premise? plataforma hibrida

https://docs.mulesoft.com/mule-runtime/4.3/hadr-guide#zero-downtime-deployment-model
zero downtime deployment - deploy via pipeline ao atualizar app chamar via postman


Sonarqube
Provide a token
Analyze "address-api": 6873326e3ad404ff76e534e1960b05b0a3b1eeb4

mvn sonar:sonar -Dsonar.projectKey=address-api -Dsonar.host.url=http://52.90.15.238:9000 -Dsonar.login=6873326e3ad404ff76e534e1960b05b0a3b1eeb4

Quality profiles
Mule	
Default: MuleSoft Rules for Mule 4.x
























git hub repo dhiegoduarte / address-api / settings / webhook / http://54.164.197.208:8080/generic-webhook-trigger/invoke?token=mulesoft


pom.xml
<cloudHubDeployment>
						<uri>https://anypoint.mulesoft.com</uri>
						<muleVersion>4.3.0</muleVersion>
						<!-- Deploy User Parameter -->
						<username>${anypoint.username}</username>
						<password>${anypoint.password}</password>
						<!-- Environment Parameter -->
						<environment>Sandbox</environment>
						<applicationName>address-api</applicationName>
						<!-- <businessGroup>Mulesoft Demo</businessGroup> -->
						<businessGroupId>fe83db7a-c73a-437b-9bf1-e7ee83f4d07c</businessGroupId>
						<workerType>Micro</workerType>
						<objectStoreV2>true</objectStoreV2>
						<skipDeploymentVerification>true</skipDeploymentVerification>
					</cloudHubDeployment>
				</configuration>

Jenkinsfile


git add . && git commit -m "DevOps build" && git push -u origin master

Usuário do jenkins com roles Cloud Admin em ambos as environments.

---

Criar MQ

customer-credit-exceeded-dead-letter-queue
customer-credit-exceeded-queue
customer-credit-reserved-dead-letter-queue
customer-credit-reserved-queue
order-dead-letter-queue
order-queue

59d69ef56d2442318df28d1d7c63c0b3
Adbb61EeC57a4913B10F6B3072316B10

orders-proxy-vivo.us-e2.cloudhub.io

Import exchange

Customer credit api no cloudhub

Orders API - local muleruntime registrado no Anypoint 
cd /Users/dduarte/mule-enterprise-standalone-4.3.0/bin
./mule

Faz deploy via console anypoint

Manage API - Exchange - Orders API - implementation url com ngrok (8082)
./ngrok http localhost:8082

Marcelo: http://customer-credit-api-ws.us-e2.cloudhub.io/api/customer-credit/1
Dhiego: 


${http.port}

dhiego_mule_demo_vivo

http:
  port: "8082"




http://e7052fdd16a9.ngrok.io/api/

orders-proxy-vivo



contextualizar q precisa ter credito (customer-credit) para compra do produto (orders)


--- 




