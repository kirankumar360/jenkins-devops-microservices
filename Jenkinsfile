//scripted stage pipelines are optional.

//Declrative
pipeline {
	agent any
	//agent { docker { image 'maven:3.9.9'}}
	environment {
		dockerHome = tool 'MyDocker'
		mavenHome  = tool 'MyMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('CheckOut') {
			steps {
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}
		stage('Compile') {
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
	            sh "mvn Test"
			}
		}
		stage('Integration Test') {
			steps {
	            sh "mvn failsafe:integration-test failsafe:verify"
			}
		}

		stage('Package') {
			steps {
	            sh "mvn package -DskipTests"
			}
		}

		stage ('Build Docker Image') {
			steps {
				//docker build -t dockkittu/hello-world-python:$env.BUILD_TAG
				script {
					dockerImage = docker.build("dockkittu/hello-world-python:$env.BUILD_TAG")
				}
			}
		}
		stage ('Push Docker Image') {
			steps {
				script {
					docker.withRegistry('', 'dockerhub') {
						dockerImage.Push();
						dockerImage.Push('latest');
					}
					
				}
				
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
