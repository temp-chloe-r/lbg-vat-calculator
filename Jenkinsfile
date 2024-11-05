pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        // Get some code from a GitHub repository
        git branch: 'main', url: 'https://github.com/temp-chloe-r/lbg-vat-calculator.git'
      }
    }//end of stage checkout
    stage('Install') {
      steps {
        sh "npm install"
      }
    }
    stage('Test') {
      steps {
        sh "npm test"
      }
    }
    stage('SonarQube Analysis') {
      environment {
        scannerHome = tool 'sonarqube'
      }//end of environment
      steps {
        withSonarQubeEnv('sonarqube') {        
        sh "${scannerHome}/bin/sonar-scanner"
        }
        timeout(time: 10, unit: 'MINUTES') {
          waitForQualityGate abortPipeline: true
        }
      }
    }
  }
}
