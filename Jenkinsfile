pipeline {
	agent any
	stages {
		stage('Init') {
			steps {
				echo "Init......"
			}
		}
		stage('Build') {
			steps {
				echo "Building......"
				sh 'mvn clean package'
			}
			post {
				success {
					echo "Archiving.............."
					archiveArtifacts artifacts: '**/target/*.war'
				}
			}
		}
		stage('Deploy to Staging') {
			steps {
				echo "Deploy to Staging......"
				build job: 'deploy-to-staging'
			}
		}
	}
}