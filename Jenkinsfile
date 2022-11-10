pipeline {
	agent any
	stages {
		stage('Checkout SCM') {
			steps {
				git 'https://github.com/hellogeraldblah/JenkinsDependencyCheckTest.git'
			}
		}
		stage('OWASP Dependency-Check') {
			steps {
				nodejs(nodeJSInstallationName: 'nodejs') {
					dependencyCheck(additionalArguments: '''
						--format XML \
						--prettyPrint\
						--out .
					'''
					odcInstallation: 'dependencyCheck')
				}
			}
		}
	post {
		success {
			dependencyCheckPublisher pattern: 'dependency-check-report.xml'
		}
	}
}
