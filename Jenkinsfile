pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'Maven3'
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

        stage('CI Build') {
            steps {
                bat 'mvn clean install'
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

                // Example: Copy WAR to DEV Tomcat
                bat '''
                echo Deploying WAR to DEV...
                '''
            }
        }

        stage('Deploy to QA') {
            steps {
                echo 'Deploying to QA Environment...'

                bat '''
                echo Deploying WAR to QA...
                '''
            }
        }

        stage('Approval for Production') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    input message: 'Approve deployment to PRODUCTION?', ok: 'Deploy'
                }
            }
        }

        stage('Deploy to PRODUCTION') {
            steps {
                echo 'Deploying to PRODUCTION Environment...'

                bat '''
                echo Deploying WAR to PRODUCTION...
                '''
            }
            post {
                success {
                    echo 'Deployment on PRODUCTION is Successful'
                }
                failure {
                    echo 'Deployment Failure on PRODUCTION'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline Execution Completed'
        }
    }
}
