pipeline {
    agent any

    options {
        timestamps()
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh '/usr/share/maven/bin/mvn clean install'
            }
            post {
                success {
                    echo 'Build Successful'
                    archiveArtifacts artifacts: '**/*.war', fingerprint: true
                }
                failure {
                    echo 'Build Failed'
                }
            }
        }

        stage('Deploy to DEV') {
            steps {
                echo 'Deploying to DEV Environment...'
            }
        }

        stage('Deploy to QA') {
            steps {
                echo 'Deploying to QA Environment...'
            }
        }

        stage('Approval for Production') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    input message: 'Approve deployment to PRODUCTION?', ok: 'Deploy'
                }
            }
        }

        stage('Deploy to PROD') {
            steps {
                echo 'Deploying to PRODUCTION Environment...'
            }
        }
    }

    post {
        always {
            echo 'Pipeline Execution Completed'
        }
    }
}
