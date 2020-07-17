pipeline {

  agent any

  // Set Maven as tool build
  tools {
    maven 'maven'
  }

  environment {
    //adding a comment for the commit test
    DEPLOY_CREDS = credentials('mule_demo')
    MULE_VERSION = '4.3.0'
    BG = 'fe83db7a-c73a-437b-9bf1-e7ee83f4d07c'
    WORKER = 'Micro'
    APP_NAME='address-api'
    PROD_TIME = "24"
    PROD_UNIT = "HOURS" // SECONDS, MINUTES, HOURS
  }

  stages {
    stage('Build') {
      steps {
            // sh 'mvn -B -U -e -V clean -DskipTests package'
            sh 'mvn clean package'
      }
    }

    stage('Test') {
      steps {
          sh "mvn test"
      }
    }

    stage('Deploy') {
      environment {
        ENVIRONMENT = 'Sandbox'
      }
      steps {
            // sh 'mvn -B -U -e -V clean -DskipTests package'
            sh 'mvn -DskipTests deploy -DmuleDeploy -Danypoint.username="$DEPLOY_CREDS_USR" -Danypoint.password="$DEPLOY_CREDS_PSW"'
      }
    }

    // stage('Deploy Production') {
    //   environment {
    //     ENVIRONMENT = 'Production'
    //   }
    //   steps {
    //         // sh 'mvn -B -U -e -V clean -DskipTests package'
    //         sh 'mvn -DskipTests deploy -DmuleDeploy -Danypoint.username="$DEPLOY_CREDS_USR" -Danypoint.password="$DEPLOY_CREDS_PSW"'
    //   }
    // }

  }
  
}
