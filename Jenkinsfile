pipeline {

  agent any

  // Set Maven as tool build
  tools {
    maven 'maven'
  }

  environment {
    //adding a comment for the commit test
    DEPLOY_CREDS = credentials('mule_demo_vivo') //vivo
    // DEPLOY_CREDS = credentials('mule_demo') //dhiego
    MULE_VERSION = '4.3.0'
    // BG = 'fe83db7a-c73a-437b-9bf1-e7ee83f4d07c' //dhiego
    BG = 'aa909b7f-1f46-4ad6-a3ce-7ab7676aa5f8' //vivo
    WORKER = 'Micro'
    // APP_NAME='address-api' //dhiego
    APP_NAME='address-api-vivo' //vivo
    PROD_TIME = "24"
    PROD_UNIT = "HOURS" // SECONDS, MINUTES, HOURS
    URL_SONAR = "http://52.90.15.238:9000"
    LOGIN_SONAR = "6873326e3ad404ff76e534e1960b05b0a3b1eeb4"
  }

  stages {
    stage('Build') {
      steps {
            sh 'mvn clean package'
      }
    }

    stage('Test') {
      steps {
          sh "mvn test"
      }
    }

    stage('Code Quality') {
      steps {
          sh 'mvn sonar:sonar -Dsonar.projectKey=address-api -Dsonar.host.url="$URL_SONAR" -Dsonar.login="$LOGIN_SONAR"'
      }
    }

    stage('Deploy') {
      environment {
        ENVIRONMENT = 'Sandbox'
      }
      steps {
            sh 'mvn -DskipTests deploy -DmuleDeploy -Danypoint.username="$DEPLOY_CREDS_USR" -Danypoint.password="$DEPLOY_CREDS_PSW"'
      }
    }

  }
  
}