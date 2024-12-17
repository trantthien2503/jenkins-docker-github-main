pipeline {
    agent any
    environment {
        IMG_NAME = 'jenkins-docker-github-app'
        DOCKER_REPO = 'trantthien2503/mmtnc-github-jenkins-docker'
    }
    stages {
        stage('build') {
            steps {
                script {
                        sh 'docker build -t ${IMG_NAME} .'
                        sh 'docker tag ${IMG_NAME} ${DOCKER_REPO}:${IMG_NAME}'
                }
            }
        }
        stage('push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'DockerHub-LG', passwordVariable: 'password', usernameVariable: 'username')]) {
                    script {
                        sh 'echo ${password} | docker login -u ${username} --password-stdin'
                        sh 'docker push ${DOCKER_REPO}:${IMG_NAME}'
                    }
                }
            }
        }
    }
}
