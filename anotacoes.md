# POC Vivo

## Agenda
## Slide 1, 2, 3, 4

## API Manager
Mostrar tudo e depois ele fazer (Postman Heroku, API Manager, Policies, Postman Proxy)

### Postman Heroku

API Manager / Create new API / Dhiego Phone API / HTTP API / Endpoint with Proxy / Select if you are managing this API using Mule 4 or above. 
/ implementation https://phone-service.herokuapp.com/phonesdata / 

API Configuration 
runtime version 4.3
Proxy application name phone-proxy-dhiego

Add consumer / copiar de Proxy URL
http://phone-proxy-dhiego.us-e2.cloudhub.io
Labels: No policies

Postman Proxy copiar o endpoint e ajustar a URL do proxy

Policy Quality of Service
Rate limiting
3 por minuto
Expose headers

Testar no Postman

Apagar Rate limiting

Adicionar SLA Tiers
Free - Automatic - 1 por minuto
Gold - Automatic - 100 por minuto
Platinum - Manual - 1000 por minuto

Adicionar Rate limiting + SLA
Expose headers

Testar no Postman sem credenciais

Exchange request Access SLA Gold

Testar no Postman com credenciais

## Slide 5

## Slide 6
Custom policy response

Request Condition
#[attributes.headers['X-Mule-Demo'] != null]

HTTP Body
#[vars.payload default 'teste']

Testar no Postman com credenciais e header X-Mule-Demo

## Catae Slides 7, 8

## Slide 9 e 10

Demonstrar
## Design Center
Create API Spec / Orders Dhiego / Title: Orders / Version: 1.0 / application/json / Resources: orders / GET / Response 200 / Add Body
[
    { "order_id": "pedido-0001" },
    { "order_id": "pedido-0002" },
    { "order_id": "pedido-0003" }
]

Mocking service / Testar

Passar para Thibério: https://github.com/mule-br/workshop/blob/master/pdf/Modulo%201%20-%20Criando%20uma%20API%20no%20Design%20Center.pdf

## Slide 11

## Studio
Novo projeto api-customer from design center Customer API / delete customer-api.xml / RODAR no mule local

Open Console e testar o Customer POST 

Studio Stop server 

Adicionar conector Salesforce / Add Modules / Salesforce

Flow Get Csutomer colocar Query da sales antes do transform

sfdc:
    username: "demos+mythical_lab@mulesoft.com"
    password: "Elum1379"
    securityToken: "7ZDtkYMazEtbvgdaaPrtMGit"

Query:
SELECT Id, Name, Phone
FROM Account
WHERE BillingCountry = 'BR'

Transform apaga tudo e liga Payload com Array e
a. Id → id
b. Name → name
c. Phone → phone

RODAR no mule local

Open Console e testar o Customer GET 

---



























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