pipeline {
    agent any

    stages {
        stage('Checkout from GitHub') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/psivaramps/jenkins-docker-demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("spamarthy/my-java-app:${env.BUILD_NUMBER}")
                }
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
        stage('Check Application with curl') {
            steps {
                script {
                    sh "curl -f http://localhost:5000"  // Replace PORT and ENDPOINT
        }
    }
}
    }
}
