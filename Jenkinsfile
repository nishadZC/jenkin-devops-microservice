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
	env {
		dockerHome= tool 'myDocker'
		mavenHome= tool 'myMaven'
		PATH = "${dockerHome}/bin:${mavenHome}/bin:${env.PATH}"
	} 
	stages{
		stage('Build') {
			steps {
				echo "Build"
				sh "docker version"
				sh "mvn --version"
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


