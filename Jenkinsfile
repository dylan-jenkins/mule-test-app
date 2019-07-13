pipeline {
	agent any
	options {
		buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '2'))
		timestamps()
		disableConcurrentBuilds()
//		skipDefaultCheckout()
	}
	
	tools {
		maven  'Maven 3.5.2'
		jdk 'latest'
	}
	
	triggers {
		pollSCM('* * * * *')
	}
	stages {
		stage('Echo') {
			steps {
				bat 'echo %GIT_LOCAL_BRANCH%'
				bat 'echo %$(GIT_COMMITTER_EMAIL)%'
				bat 'echo %$(GIT_AUTHOR_EMAIL)%'
			}
		}
		stage('Test') {
			steps {
				bat 'mvn clean test'
			}
		}

		stage('Deploy') {
			environment {
				ANYPOINT_PLATFORM = credentials('anypoint.platform')
			}
			steps {
				bat 'mvn deploy -P cloudhub -Dmule.version=3.9.1 -Danypoint.username=${ANYPOINT_PLATFORM_USR} -Danypoint.password=${ANYPOINT_PLATFORM_PSW}'
			}
		}
	}
}
