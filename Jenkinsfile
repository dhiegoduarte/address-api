pipeline {

  agent any

  // Set Maven as tool build
  tools {
    maven 'maven'
  }

  environment {
    //configurado no Jenkins
    DEPLOY_CREDS = credentials('mule_demo_vivo') //vivo
    // DEPLOY_CREDS = credentials('mule_demo') //dhiego
    MULE_VERSION = '4.3.0'
    WORKER = 'Micro'
    // APP_NAME='address-api' //dhiego
    APP_NAME='address-api-vivo' //vivo
    PROD_TIME = "24"
    PROD_UNIT = "HOURS" // SECONDS, MINUTES, HOURS
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

    stage('Deploy Development') {
      // environment {
      //   ENVIRONMENT = 'Development'
      // }
      steps {
          sleep(time: 3, unit: 'SECONDS') 
            // sh 'mvn -DskipTests deploy -DmuleDeploy -Danypoint.username="$DEPLOY_CREDS_USR" -Danypoint.password="$DEPLOY_CREDS_PSW"'
      }
    }

    stage('Deploy Sandbox') {
      environment {
        ENVIRONMENT = 'Sandbox'
      }
      steps {
            sh 'mvn -DskipTests deploy -DmuleDeploy -Danypoint.username="$DEPLOY_CREDS_USR" -Danypoint.password="$DEPLOY_CREDS_PSW"'
      }
    }

    stage('Deploy Production') {
      // environment {
      //   ENVIRONMENT = 'Production'
      // }
      steps {
          sleep(time: 3, unit: 'SECONDS') 
            // sh 'mvn -DskipTests deploy -DmuleDeploy -Danypoint.username="$DEPLOY_CREDS_USR" -Danypoint.password="$DEPLOY_CREDS_PSW"'
      }
    }

  }
  
}
