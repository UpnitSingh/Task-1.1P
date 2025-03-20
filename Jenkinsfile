pipeline {
    agent any

    environment {
        DIRECTORY_PATH = "https://github.com/UpnitSingh/Task-1.1P.git"
        TESTING_ENVIRONMENT = "Testing_Env"
        PRODUCTION_ENVIRONMENT = "Upnit_Singh"  
        RECIPIENT_EMAIL = "singhupnit@gmail.com"
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Fetching source code from: ${DIRECTORY_PATH}"
                git url: "${DIRECTORY_PATH}", branch: 'main'
            }
        }

        stage('Build') {
            steps {
                echo "Compiling the code and generating artifacts"
                
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit and integration tests"
              
            }
            post {
                always {
                    emailext subject: "Jenkins Test Results", 
                             body: "Unit & Integration tests completed. Check Jenkins logs for details.",
                             to: "${RECIPIENT_EMAIL}"
                }
            }
        }

        stage('Code Quality Check') {
            steps {
                echo "Analyzing code quality using SonarQube"
                
            }
        }

        stage('Security Scan') {
            steps {
                echo "Performing security scan using OWASP Dependency Check"
                
            }
            post {
                always {
                    emailext subject: "Jenkins Security Scan Results", 
                             body: "Security scan completed. Check Jenkins logs for details.",
                             to: "${RECIPIENT_EMAIL}"
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to staging: ${TESTING_ENVIRONMENT}"
               
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on staging"
                
            }
        }

        stage('Approval') {
            steps {
                echo "Waiting for manual approval..."
                input message: "Approve deployment to production?", ok: "Deploy"
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying application to production: ${PRODUCTION_ENVIRONMENT}"
                
            }
        }
    }

    post {
        success {
            emailext subject: "Jenkins Pipeline Success", 
                     body: "Pipeline executed successfully! Application is now deployed.",
                     to: "${RECIPIENT_EMAIL}"
        }
        failure {
            emailext subject: "Jenkins Pipeline Failure", 
                     body: "Pipeline execution failed. Check Jenkins logs for details.",
                     to: "${RECIPIENT_EMAIL}"
        }
    }
}
