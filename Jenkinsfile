pipeline {

    environment {
        
        registry = "sermon99/flask-docker-jenkins-app-7"
        registryCredential = 'dockerhub_account'
        dockerImage = ''
    }
    agent any

    stages {
        stage('Cloning our Git') {
            steps {
                git 'https://sermon99@bitbucket.org/sermon99/flask-docker-jenkins-app-7.git'
                echo 'Cloning the Git..'
            }
        }
        stage('Building the image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
                
            }
        }
        stage('Deploy the image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
                echo 'Deploying....'
            }
        }
    }
}