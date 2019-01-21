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
		stage('Deploy') {
			steps {
				echo "Deploy......"
			}
		}
	}
}