pipeline {
    agent any

    stages {
        stage('Run Test') {
            steps {
                bat "docker-compose up" // For Linux/Mac use -> sh "docker-compose up"
            }
        }

        stage('Bring Grid Down') {
            steps {
                bat "docker-compose down" // For Linux/Mac use -> sh "docker-compose down"
            }
        }
    }
}