pipeline {
  agent any
  stages {
    stage('Test') {
      steps {
        bat 'mvn clean test'
      }
    }

    stage('Deploy CloudHub') {
      environment {
        ANYPOINT_PLATFORM = credentials('anypoint.platform')
      }
      steps {
        bat 'mvn deploy -P cloudhub -Dmule.version=3.9.0 -Danypoint.username=${ANYPOINT_PLATFORM_USR} -Danypoint.password=${ANYPOINT_PLATFORM_PSW}'
      }
    }
  }
}