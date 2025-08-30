pipeline {
    agent any

    environment {
        IMAGE_NAME =" deepakk007/jenkins_build3"
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout([$class: 'GitSCM',
                          branches: [[name: '*/main']],
                          userRemoteConfigs: [[
                              url: 'https://github.com/Deepakking07/docker_jenkins1.git'
                          ]]
                ])
            } 
                    
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Login to DockerHub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'Dockerhub_credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                    }
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    sh "docker push ${IMAGE_NAME}"
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    sh "docker rmi ${IMAGE_NAME}"
                }
            }
        }
    }
}
