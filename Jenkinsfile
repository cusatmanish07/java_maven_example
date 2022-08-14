pipeline {
 agent any
 environment {
  MY_CRED = credentials ('dockerHubCred')
 }
  tools {
      maven 'mvn'
      jdk 'myJDk'
 }
  stages {
    stage('credinfo'){
       steps {
          script {
          echo "username is : $MY_CRED_USR"
          echo "password is : $MY_CRED_PSW"
          }
       }
    }

    stage('clean') {
       steps {
           script {
                sh ''' mvn clean '''
      
            }    
       }
    }
    stage('verify') {
       steps {
         script {
                 sh '''mvn verify '''
         }
       }  
    }
    stage('install') {
       steps {
         script {
                 sh '''mvn install '''
         }
       }
    }
    stage('test') {
       steps {
         script {
                 sh '''mvn test '''
         }
       }
    }
    stage('SonarQube analysis') {
        steps {
          withSonarQubeEnv(credentialsId: 'sonarqubeToken', installationName: 'sonarqube') { // You can override the credential to be used
          sh 'mvn sonar:sonar'
          }
        }
     }
  }
}
