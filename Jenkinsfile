pipeline {
 agent any
     
  stages {
    stage('First') {
       steps {
           script {
                sh ''' echo "First stage" '''
      
            }    
       }
    }
    stage('Second') {
       steps {
         script {
                 sh '''echo "Second stage" '''
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
