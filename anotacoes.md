
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
customer-credit-exceeded-queue
customer-credit-reserved-queue
order-queue

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