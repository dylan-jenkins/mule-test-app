pipeline {
	agent any
	options {
		buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '3'))
		timestamps()
		disableConcurrentBuilds()
		skipDefaultCheckout()
	}
	
	tools {
		maven  'Maven 3.5.3'
		jdk 'latest'
	}
	
	stages {
		stage('Test') {
			steps {
				withMaven () {
					bat 'mvn clean test'
				}
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