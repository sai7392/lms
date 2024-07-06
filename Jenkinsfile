pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'free'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'sudo docker container ls'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh 'sudo docker image ls'
            }
        }
    }
}