pipeline {

    agent any

    stages {

        stage('Run Test') {
            steps{
                bat "docker-compose up" // for Linux/Mac use -> sh "docker-compose up"
            }
        }

        stage('Bring Grid Down') {
            steps{
                bat "docker-compose down" // for Linux/Mac use -> sh "docker-compose down"
            }
        }
    }
}