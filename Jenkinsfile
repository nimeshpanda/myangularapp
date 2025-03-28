pipeline {
    agent any
    tools {nodejs "NODEJS"}
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
      stage('SonarQube analysis') {
  steps {
    script {
      scannerHome = tool 'SonarScanner' // Must match the name configured in Global Tool Configuration
    }
    withSonarQubeEnv('SonarQube') { // Must match the name of your SonarQube server in Configure System
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
}
        stage('Deliver') {
            steps {
                sh 'chmod -R +rwx ./jenkins/scripts/deliver.sh'
                sh 'chmod -R +rwx ./jenkins/scripts/kill.sh'
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
