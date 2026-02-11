pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'Maven3'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Deploy to DEV') {
            steps {
                echo "Deploying to DEV..."
            }
        }

        stage('Deploy to QA') {
            steps {
                echo "Deploying to QA..."
            }
        }

        stage('Approval for Production') {
            steps {
                input message: 'Approve Production Deployment?', ok: 'Deploy'
            }
        }

        stage('Deploy to PROD') {
            steps {
                echo "Deploying to PROD..."
            }
        }
    }
}
