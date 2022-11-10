pipeline {
	agent any
	stages {
		stage('Checkout SCM') {
			steps {
				git 'https://github.com/hellogeraldblah/JenkinsDependencyCheckTest.git'
			}
		}
		stage('OWASP DependencyCheck') {
			steps {
				nodejs(nodeJSInstallationName: 'nodejs') {
				    dependencyCheck(
					additionalArguments: '''
					    --enableExperimental \
					    --disableNodeAudit \
					    --disableRetireJS \
					    --nodeAuditSkipDevDependencies \
					    --nodePackageSkipDevDependencies \
					    --format JSON \
					    --format XML \
					    --prettyPrint \
					    --out .
					''',
					stopBuild: false,
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
