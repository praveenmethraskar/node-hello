pipeline {
    agent any

    environment {
        IMAGE_NAME = 'node-app'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/praveenmethraskar/node-hello.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}")
                }
            }
        }

        stage('Test Docker Image') {
            steps {
                script {
                    docker.image("${IMAGE_NAME}").inside {
                        sh 'npm test'
                    }
                }
            }
        }

        stage('Deploy Docker Image') {
            steps {
                script {
                    docker.run("${IMAGE_NAME}", '-p 3000:3000')
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
