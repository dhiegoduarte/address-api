pipeline {

  agent any
  environment {
    //adding a comment for the commit test
    DEPLOY_CREDS = credentials('mule_demo')
    MULE_VERSION = '4.3.0'
    BG = "Mulesoft Demo"
    WORKER = "Micro"
  }
  stages {
    stage('Build') {
      steps {
            // sh 'mvn -B -U -e -V clean -DskipTests package'
            sh 'mvn clean package'
      }
    }

    stage('Deploy') {
      steps {
            // sh 'mvn -B -U -e -V clean -DskipTests package'
            sh 'mvn -DskipTests deploy -DmuleDeploy -Danypoint.username="$DEPLOY_CREDS_USR" -Danypoint.password="$DEPLOY_CREDS_PSW"'

      }
    }


    // stage('Test') {
    //   steps {
    //       bat "mvn test"
    //   }
    // }

    //  stage('Deploy Development') {
    //   environment {
    //     ENVIRONMENT = 'Sandbox'
    //     APP_NAME = '<DEV-API-NAME>'
    //   }
    //   steps {
    //         bat 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -Dcloudhub.app="%APP_NAME%" -Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.bg="%BG%" -Dcloudhub.worker="%WORKER%"'
    //   }
    // }
    // stage('Deploy Production') {
    //   environment {
    //     ENVIRONMENT = 'Production'
    //     APP_NAME = '<API-NAME>'
    //   }
    //   steps {
    //         bat 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -Dcloudhub.app="%APP_NAME%" -Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.bg="%BG%" -Dcloudhub.worker="%WORKER%"'
    //   }
    // }
  }

  tools {
    maven 'maven'
  }
}
