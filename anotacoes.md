
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
