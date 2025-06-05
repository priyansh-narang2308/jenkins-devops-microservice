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
	agent any
	// agent { docker { image "maven:3.6.3" } }
	environment{
		// to configure the both homes to the path
		dockerHome = tool "myDocker"
		mavenHome= tool "myMaven"
		PATH ="$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
		stage("Checkout"){
			steps{
				echo "mvn --version"
				sh "mvn --version"
				echo "Docker version"
				sh "docker version"
				echo "Build"
			}
		}
		stage("Compile"){
			steps{
				sh "mvn clean compile"
			}
		}
		stage("Test"){
			steps{
				 sh "mvn test"
			}
		}
		stage("Integration Test"){
			steps{
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		stage("Package"){
			steps{
				// this creates a jar file and and then skips all the prev tests
				sh "mvn package -DskipTests"
			}
		}
		stage("Build Docker Image"){
			steps{
				// this is DECLARITIVE way to do it 
				// "docker build -t in28min/curreny-exchange-devops:$env.BUILD_TAG"
				// this is new way 
				script{
					dockerImage = docker.build("priyansh2308/curreny-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}

		stage("Push Docker Image"){
			steps{
				script{
					docker.withRegistry("","dockerHub"){
						dockerImage.push('')
						dockerImage.push("latest")
					}
				}
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