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

		}
	}
		stage('Deployment') {
			parallel {
				stage ('Deploy to Staging')
			{
				steps {
					sh "scp -i /home/jenkins/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat7/webapps"
				}
			}
		stage ("Deploy to Production") {
			steps {
				sh "scp -i /home/jenkins/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat-demo.prod}:/var/lib/tomcat7/webapps"
				}
			}
		}
	}
}
}
	
