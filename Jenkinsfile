pipeline {
    
 agent any 
	// agent { docker { image 'maven:3.9.6'} }
	// agent { docker { image 'node:13.8'} }
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
     	
	stages {

        stage ('Checkout') {
			steps {
			git branch : 'main' , url: 'https://github.com/psivaramps/jenkins-docker-demo.git'
			}
		}
				
		stage ('Check Docker version') {
			steps {
			sh 'docker --version'
			
			}
		}

		stage ('Build Image') {
			steps {
			//sh 'docker build -t my-java-app:0.1 .'
			script {
					dockerImage = docker.build("spamarthy/my-java-app:0.1)
				}
			}
		}

		stage ('Tag the local image') {
			steps {
			sh 'docker tag "my-java-app:0.1" spamarthy/my-java-app:0.1'
			}
		}
		
		stage ('Run a Docker container') {
			steps {
			sh 'docker run -p 5000:5000 spamarthy/my-java-app:0.1'
			}
		}
	/*	stage('Get Local Host IP') {
            		steps {
                		script {
                  		  // Get the hostname of the agent
                   		 hostname = sh(returnStdout: true, script: 'hostname -f').trim()> appip.txt
				 sh 'curl http://$(cat appip.txt):5000'
                }
            }*/

		stage('Push Docker Image') {
			steps {
				script {
					docker.withRegistry( 'https://registry.hub.docker.com', 'dockerhub' ) {
						dockerImage.push()
						dockerImage.push('latest')
					}
				}
			}
			
		}
	
	}
}

