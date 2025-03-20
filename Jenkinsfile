pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Fetching source code from GitHub...'
                git 'https://github.com/UpnitSingh/Task-1.1P.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Compiling Java code...'
                bat 'javac -d out src/**/*.java'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests...'
                bat 'java -cp out org.junit.runner.JUnitCore YourTestClass'
            }
        }

        stage('Code Quality Check') {
            steps {
                echo 'Skipping Code Quality Check (Modify this step if needed)'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Skipping Security Scan (Modify this step if needed)'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Skipping Deployment (Modify this step if needed)'
            }
        }

        stage('Approval') {
            steps {
                echo 'Skipping Approval (Modify this step if needed)'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Skipping Production Deployment (Modify this step if needed)'
            }
        }
    }

    post {
        always {
            echo 'Sending email notification...'
            emailext (
                to: 'singhupnit@gmail.com',
                subject: "Jenkins Build Status: ${currentBuild.currentResult}",
                body: "The build result is: ${currentBuild.currentResult}"
            )
        }
    }
}
