pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'jenkins-docker-github-app'
    }
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                script {
                    // Build Docker image
                    sh 'docker build -t ${DOCKER_IMAGE} .'
                    sh 'docker tag ${DOCKER_IMAGE} trantthien2503/mmtnc-github-jenkins-docker:${DOCKER_IMAGE}'
                }
            }
        }
        stage('Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'DockerHub-LG', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    script {
                        // Login to Docker Hub
                        sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                        // Push Docker image
                        sh 'docker push trantthien2503/mmtnc-github-jenkins-docker:jenkins-docker-github-app'
                    }
                }
            }
        }
    }
}
