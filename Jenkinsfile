//scripted stage pipelines are optional.

//Declrative
pipeline {
	agent any
	stages {
		stage('Build') {
			steps {
				echo "Build"
			}
		}
		stage('Test') {
			steps {
	            echo "Test"
			}
		}
		stage('Integration Test') {
			steps {
	            echo "Integration Test"
			}
		}
	
	} 
	
	post {
		always {
			echo 'Im Aweomse. I run Always'
		}
		success {
			echo 'I run when you are successful.'
		}
		failure {
			echo 'I run when you fail.'
		}
	}
	
}
