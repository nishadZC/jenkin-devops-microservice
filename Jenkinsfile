// Scripted Pipeline Example
// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// 	stage('Integration Test') {
// 		echo "Integration Test"
// 	}
// }

//Declarative pipeline

// pipeline {
// 	agent { docker {
// 		image 'maven:3.8.4-openjdk-17'
// 	} }
// 	stages{
// 		stage('Build') {
// 			steps {
// 				sh 'mvn --version'
// 				echo "Build"
// 			}
// 		}
// 		stage('Test') {
// 			steps {
// 				echo "Test"
// 			}
// 		}
// 		stage('Integration Test') {
// 			steps {
// 				echo "Integration Test"
// 			}
// 		}
// 	}
// 	post {
// 		always{
// 			echo "Pipeline completed"
// 		}
// 		success {
// 			echo "Pipeline succeeded"
// 		}
// 		failure {
// 			echo "Pipeline failed"
// 		}
// 	}
// }


// pipeline {
// 	agent any 
// 	stages{
// 		stage('Build') {
// 			steps {
// 				echo "Build"
// 				echo "${env.BUILD_NUMBER}"
// 				echo "${env.BUILD_ID}"
// 				echo "${env.BUILD_URL}"
// 				echo "${env.JOB_NAME}"
// 				echo "${env.WORKSPACE}"
// 				echo "${env.GIT_COMMIT}"
// 				echo "${env.GIT_BRANCH}"
// 				echo "${env.GIT_URL}"
// 				echo "${PATH}"
// 			}
// 		}
// 		stage('Test') {
// 			steps {
// 				echo "Test"
// 			}
// 		}
// 		stage('Integration Test') {
// 			steps {
// 				echo "Integration Test"
// 			}
// 		}
// 	}
// 	post {
// 		always{
// 			echo "Pipeline completed"
// 		}
// 		success {
// 			echo "Pipeline succeeded"
// 		}
// 		failure {
// 			echo "Pipeline failed"
// 		}
// 	}
// }


pipeline {
	agent any
	environment {
		dockerHome= tool 'myDocker'
		mavenHome= tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	} 
	stages{
		stage('Checkout') {
			steps {
				sh "docker version"
				sh "mvn --version"
			}
		}
		stage('Compile') {
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
				sh "mvn test"
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
		stage('Build docker image') {
			steps {
				// sh "docker build -t in28min/currency-exchange-devops:${env.BUILD_TAG}"
				script {
					dockerImage = docker.build("in28min/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push docker image') {
			steps {
				script {
					docker.withRegistry('', 'dockerhub-creds') {
						dockerImage.push()
						dockerImage.push('latest')
					}
				}
			}
		}
	}
	post {
		always{
			echo "Pipeline completed"
		}
		success {
			echo "Pipeline succeeded"
		}
		failure {
			echo "Pipeline failed"
		}
	}
}


