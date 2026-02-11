pipeline {
    agent any

    tools {
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }

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
                sh 'mvn clean install'
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
                // Add your DEV deployment commands here
            }
        }

        stage('Deploy to QA') {
            steps {
                echo 'Deploying to QA Environment...'
                // Add your QA deployment commands here
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
                // Add your PROD deployment commands here
            }
            post {
                success {
                    echo 'Production Deployment Successful'
                }
                failure {
                    echo 'Production Deployment Failed'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline Execution Complete
