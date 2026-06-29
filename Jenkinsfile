pipeline {
    agent any

    environment {
        // Replace with the exact ID of the credentials you created in Jenkins
        DOCKER_CRED = credentials('priti123') 
    }

    stages {
        stage('fetch-code') {
            steps {
                // Replace branch name (e.g., 'main') and your GitHub repository URL
                git branch: 'main', url: 'https://github.com/maurya-Priti/devops-5.git'
            }
        }

        stage('build-image') {
            steps {
                // Replace with your Docker Hub username and your desired image name
                sh "docker build -t pritimaurya/mysite:${BUILD_NUMBER} ."
            }
        }

        stage('push-image') {
            steps {
                // Replace with your Docker Hub username
                sh 'echo "$DOCKER_CRED_PSW" | docker login -u pritimaurya --password-stdin'
                
                // Replace with your Docker Hub username and image name
                sh "docker push pritimaurya/mysite:${BUILD_NUMBER}"
            }
        }
        
        stage('update-minikube') {
            steps {
                // Replace deployment name, container name, Docker Hub username, and image name
                sh "kubectl set image deployment/mysite-app mysite=pritimaurya/mysite:${BUILD_NUMBER}"
            }
        }
    }
}