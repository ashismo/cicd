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
		stage('Deploy to production - Approval needed') {
			steps {
				echo "Deploy to production - Approval needed......"
				timeout(time:5, unit:'DAYS') {
					input message: 'Approve PRODUCTION deployment?'
				}
				build job: 'deploy-to-production'
			}
			post {
				success {
					echo "Code deployed into production"
				}
				
				failure {
					echo "Deployment failed"
				} 
			}
		}
	}
}