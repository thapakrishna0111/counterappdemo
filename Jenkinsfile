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

  }
}
