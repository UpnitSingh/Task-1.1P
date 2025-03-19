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
                // Example: Using Maven to build
                sh 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit and integration tests"
                // Example: Running JUnit tests
                sh 'mvn test'
            }
            post {
                always {
                    mail to: "${RECIPIENT_EMAIL}",
                         subject: "Jenkins Test Results",
                         body: "Unit & Integration tests completed. Check Jenkins logs for details."
                }
            }
        }

        stage('Code Quality Check') {
            steps {
                echo "Analyzing code quality using SonarQube"
                // Example: Running SonarQube scan
                sh 'mvn sonar:sonar'
            }
        }

        stage('Security Scan') {
            steps {
                echo "Performing security scan using OWASP Dependency Check"
                // Example: Running OWASP scan
                sh 'mvn dependency-check:check'
            }
            post {
                always {
                    mail to: "${RECIPIENT_EMAIL}",
                         subject: "Jenkins Security Scan Results",
                         body: "Security scan completed. Check Jenkins logs for details."
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to staging: ${TESTING_ENVIRONMENT}"
                // Example: Deploy to AWS EC2 (staging)
                sh 'scp target/*.jar user@staging-server:/deployments/'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on staging"
                // Example: Run Selenium or Postman API tests
                sh 'mvn verify'
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
                // Example: Deploy to AWS EC2 (production)
                sh 'scp target/*.jar user@production-server:/deployments/'
            }
        }
    }

    post {
        success {
            mail to: "${RECIPIENT_EMAIL}",
                 subject: "Jenkins Pipeline Success",
                 body: "Pipeline executed successfully! Application is now deployed."
        }
        failure {
            mail to: "${RECIPIENT_EMAIL}",
                 subject: "Jenkins Pipeline Failure",
                 body: "Pipeline execution failed. Check Jenkins logs for details."
        }
    }
}
