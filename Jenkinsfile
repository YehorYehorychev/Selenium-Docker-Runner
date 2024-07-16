pipeline {
    agent any

    parameters {
      choice choices: ['chrome', 'firefox'], description: 'Select the browser:', name: 'BROWSER'
    }

    stages {
        stage('Start Grid') {
            steps {
                bat "docker-compose -f grid.yml up --scale ${params.BROWSER}=2 -d" // For Linux/Mac use -> sh "docker-compose -f grid.yml up --scale ${params.BROWSER}=2 -d"
            }
        }

        stage('Run Tests') {
            steps {
                bat "docker-compose -f test-suites.yml up --pull=always" // For Linux/Mac use -> sh "docker-compose -f test-suites.yml up"
                script {
                    if (fileExists('output/vendor-portal/testng-failed.xml') || fileExists('output/vendor-portal/testng-failed.xml')) {
                        error('Failed Tests Found!')
                    }
                }
            }
        }
    }

    post {
        always {
            bat "docker-compose -f grid.yml down" // For Linux/Mac use -> sh "docker-compose -f grid.yml down"
            bat "docker-compose -f test-suites.yml down" // For Linux/Mac use -> sh "docker-compose -f test-suites.yml down"
            archiveArtifacts artifacts: 'output/flight-reservation/emailable-report.html', followSymlinks: false
            archiveArtifacts artifacts: 'output/vendor-portal/emailable-report.html', followSymlinks: false
        }
    }
}
