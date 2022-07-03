pipeline {
    agent any

    stages {
        stage ('Checkout') {
            steps {
                git branch: 'main', 
                url: 'https://github.com/kirillqq20/automatic_docker_release_php.git'
            }
        }

        stage ('Test') {
            steps {
                dir ('build'){
                    sh 'ls -la'
                    sh 'pwd'
                }
            }
        }

        stage ('Build') {
            steps {
                dir ('build'){
                   sh 'docker build -t kirillqq20/automatic_docker_release_php:v1 . '
                }
            }
        }

        stage ('Docker push') {
            steps {
                withDockerRegistry(credentialsId: 'Docker-hub-kirillqq20', url: 'https://index.docker.io/v1/'){
                    sh '''
                        docker push kirillqq20/automatic_docker_release_php:v1
                     '''
                }
            }
        }
        
        stage ('Delete image') {
            steps {
                sh ' docker rmi kirillqq20/automatic_docker_release_php:v1'
            }
        }
        stage ('RUN') {
            steps {
                dir ('build'){
                   sh 'docker run -it p 1122:80 kirillqq20/automatic_docker_release_php:v1'
                }
            }
        }
    }
}