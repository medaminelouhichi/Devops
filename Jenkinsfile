pipeline {
  agent any

  tools { maven 'maven-3' }

  triggers { pollSCM('H/2 * * * *') }

  options {
    timestamps()
    buildDiscarder(logRotator(numToKeepStr: '10'))
  }

  stages {
    stage('Build & Test') {
      steps { sh 'mvn -B clean verify' }
    }
  }

  post {
    always {
      junit allowEmptyResults: true, testResults: '**/target/surefire-reports/*.xml'
    }
    success {
      archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
    }
  }
}
