// This adds install and test stages before static code analysis
pipeline {
  agent any

  stages {
    stage('Checkout') {
        steps {
          // Get some code from a GitHub repository
          git branch: 'main', url: 'https://github.com/Ben8502/lbg-vat-calculator'
        }
    }
    stage('Install') {
        steps {
            // Install the ReactJS dependencies
            sh "npm install"
        }
    }
    stage('Test') {
        steps {
          // Run the ReactJS tests
          sh "npm test"
        }
    }
    stage('SonarQube Analysis') {
      environment {
        scannerHome = tool 'sonarqube'
        }
        steps {
            withSonarQubeEnv('sonar-qube-1') {        
              sh "${scannerHome}/bin/sonar-scanner"
        }
        timeout(time: 1, unit: 'MINUTES'){
          waitForQualityGate abortPipeline: true
          }
        }
    }
  }
}
