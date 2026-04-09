pipeline {
    agent any

    stages {
        stage('Install Newman') {
            steps {
                bat 'npm install -g newman newman-reporter-htmlextra'
            }
        }

        stage('Run Postman Collection') {
            steps {
                bat '''
                mkdir reports
                newman run collection.json ^
                -e LoginEnv.postman_environment.json ^
                -r cli,htmlextra ^
                --reporter-htmlextra-export reports\\newman-report.html
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'reports/*.html', fingerprint: true
        }
    }
}