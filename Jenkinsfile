pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  stages {
    stage('Scan') {
      steps {
        withSonarQubeEnv(installationName: 'sonarqube') { 
          echo 'Sonarqube working...'
        }
      }
    }
    stage("Install Project Dependencies") {
   steps {
       nodejs(nodeJSInstallationName: 'node'){
           sh "npm install"
           withSonarQubeEnv('sonarqube'){
           sh "npm install sonar-scanner"
           sh "npm run sonar"
           }
       }
    }
  }
}

