pipeline {
    
 agent any 
	  	   	
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
			sh 'docker build -t spamarthy/my-java-app:0.1 .'
			}
		}

			
		stage('Push Docker Image to Docker Hub') {
	            steps {
	                script {
	                    docker.withRegistry('https://registry.hub.docker.com', 'spamarthy') {
	                        dockerImage.push()
	                    }
	                }
	            }
	        }
		
		stage ('Run a Docker container') {
			steps {
			sh 'docker run -p 5000:5000 -d spamarthy/my-java-app:${env.BUILD_NUMBER}'
			}
		}
		
		
		stage('Check Application with curl') {
   			 steps {
       				 script {
           				 sh "curl -f http://localhost:5000"  // Replace PORT and ENDPOINT
       					 }
   				 }
			}
	
	}
}

