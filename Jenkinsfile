pipeline{
  agent any
  environment {
    PATH="$PATH:/opt/maven/bin"
  }
  stages{
      stage('git SCM Checkout'){
        steps{
          git branch: 'main', url: 'https://github.com/thapakrishna0111/counterappdemo.git'
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
      }
        stage('SonarQube Analysis'){
        steps{
           script {
             withSonarQubeEnv(credentialsId: 'sonar-token') {
                sh 'mvn clean package sonar:sonar'
               }
             }
           }
        }
        stage('Quality Gate Status'){
        steps{
           script {
               waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
            // waitForQualityGate abortPipeline: false, credentialsId: 'sonar-auth'
           }
        }
      }






  }
}
