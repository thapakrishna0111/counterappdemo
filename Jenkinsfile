pipeline{
  agent any
    stages{
      stage('git checkout'){
        steps{
           git branch: 'main', url: 'https://github.com/thapakrishna0111/counter-app.git'
        }
      }
      stage('UNIT Testing'){
        steps{
           sh 'mvn test'
        }
      }
      stage('Integration Testing'){
        steps{
           sh 'mvn verify -DskipUnitTests'
        }
      }
       stage('Maven Build'){
        steps{
           sh 'mvn clean install'
        }

      stage('SonarQube Analysis'){
        steps{
           script {
             withSonarQubeEnv(credentialsId: 'sonar-api-key') {
             sh 'mvn clean package sonar:sonar'
             }
           }
        }        
      }
      stage('Sonar Qality Gate'){
        steps{
          script {
            waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api-key'
          }
        }
      }
    }
}
