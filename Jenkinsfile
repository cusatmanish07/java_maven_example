pipeline {
 agent any
 tools {
      maven 'mvn'
      jdk 'myJDk'
 }
  stages {
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
    stage('SonarQube analysis') {
        steps {
          withSonarQubeEnv(credentialsId: 'sonarqubeToken', installationName: 'sonarqube') { // You can override the credential to be used
          sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2.0.1227:sonar'
          }
        }
     }
  }
}
