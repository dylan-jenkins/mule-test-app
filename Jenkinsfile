pipeline {
	agent any
	options {
		buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '1'))
		timestamps()
		disableConcurrentBuilds()
		skipDefaultCheckout()
	}
	
	tools {
		maven  '3.5.2'
		jdk '1.8.0_162'
	}
	
	triggers {
		pollSCM('H/1 * * * *')
	}
	stages {
		stage('Test') {
			steps {
				bat 'mvn clean install'
			}
		}

		stage('Deploy') {
			environment {
				ANYPOINT_PLATFORM = credentials('anypoint.platform')
			}
			steps {
				bat 'mvn deploy -P cloudhub -Dmule.version=3.9.0 -Danypoint.username=${ANYPOINT_PLATFORM_USR} -Danypoint.password=${ANYPOINT_PLATFORM_PSW}'
			}
		}
	}
}