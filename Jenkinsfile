pipeline {
    agent any

    stages {
        stage('Start Grid') {
            steps {
                bat "docker-compose -f grid.yml up -d" // For Linux/Mac use -> sh "docker-compose up"
            }
        }

        stage('Run Tests') {
            steps {
                bat "docker-compose -f test-suites.yml up" // For Linux/Mac use -> sh "docker-compose down"
            }
        }
    }

    post {
        always {
            bat "docker-compose -f grid.yml down"
            bat "docker-compose -f test-suites.yml down"
            archiveArtifacts artifacts: 'output/flight-reservation/emailable-report.html', followSymlinks: false
            archiveArtifacts artifacts: 'output/vendor-portal/emailable-report.html', followSymlinks: false
        }
    }
}