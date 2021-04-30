pipeline {
	agent any

	parameters {
		string(name: 'tomcat_dev',
		defaultValue: 'ip_staging_server',
		description: 'Staging Server')
		string(name: 'tomcat_prod',
		defaultValue: 'ip_prod_server',
		description: 'Production Server')
	}

	triggers {
		pollSCM('* * * * *')
		}

	stages {
		stage('Build') {
			steps {
				sh 'mvn clean package'
				}
			post {
				success {
					echo 'Now Archiving...'
					archiveArtifacts
			artifacts: '**/target/*.war'
			}
