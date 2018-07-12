pipeline {
	agent any
	options {
		buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '3'))
		timestamps()
		disableConcurrentBuilds()
		skipDefaultCheckout()
	}
	
	tools {
		maven  '3.5.2'
		jdk '1.8.0_162'
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