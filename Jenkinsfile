// this is scripted so if we dont write stages still it will work
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


// DECLARITIVE
// pipleine should have stages to be configured and then steps inside
pipeline{
	// agent any
	agent { docker { image "maven:3.6.3" } }
	environment{
		// to configure the both homes to the path
		dockerHome = tool "myDocker"
		mavenHome= tool "myMaven"
		PATH ="$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
		stage("Build"){
			steps{
				echo "mvn --version"
				sh "mvn --version"
				echo "Docker version"
				sh "docker --version"
				echo "Build"
			}
		}
		stage("Test"){
			steps{
				echo "Test"
			}
		}
		stage("Integration Test"){
			steps{
				echo "Integration Test"
			}
		}
	}
	post {
		always{
			echo "I'm awesome. I run always"
		}
		success{
			echo "Only run when its success"
		}
		failure{
			echo "I run when u fail"
		}
	}
}