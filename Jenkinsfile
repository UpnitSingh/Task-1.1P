pipeline {
    agent any

    environment {
        DIRECTORY_PATH = "https://github.com/UpnitSingh/Task-1.1P.git"
        TESTING_ENVIRONMENT = "Testing_Env"
        PRODUCTION_ENVIRONMENT = "Upnit_Singh"
        RECIPIENT_EMAIL = "singhupnit@gmail.com"
        LOG_FILE = "jenkins-log.txt"
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
                    script {
                        writeFile file: "${LOG_FILE}", text: currentBuild.getLog(100).join("\n")
                    }
                    archiveArtifacts artifacts: "${LOG_FILE}", fingerprint: true
                    emailext subject: "Jenkins Test Results",
                             body: "Unit & Integration tests completed. Log file attached.",
                             to: "${RECIPIENT_EMAIL}",
                             attachmentsPattern: "${LOG_FILE}"
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
                    script {
                        writeFile file: "${LOG_FILE}", text: currentBuild.getLog(100).join("\n")
                    }
                    archiveArtifacts artifacts: "${LOG_FILE}", fingerprint: true
                    emailext subject: "Jenkins Security Scan Results",
                             body: "Security scan completed. Log file attached.",
                             to: "${RECIPIENT_EMAIL}",
                             attachmentsPattern: "${LOG_FILE}"
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

        stage('Deploy to Production') {
            steps {
                echo "Deploying application to production: ${PRODUCTION_ENVIRONMENT}"
            }
        }
    }

    post {
        success {
            script {
                writeFile file: "${LOG_FILE}", text: currentBuild.getLog(100).join("\n")
            }
            archiveArtifacts artifacts: "${LOG_FILE}", fingerprint: true
            emailext subject: "Jenkins Pipeline Success",
                     body: "Pipeline executed successfully! Log file attached.",
                     to: "${RECIPIENT_EMAIL}",
                     attachmentsPattern: "${LOG_FILE}"
        }
        failure {
            script {
               def log = currentBuild.rawBuild.getLog(100).join("\n")
             echo log

            }
            archiveArtifacts artifacts: "${LOG_FILE}", fingerprint: true
            emailext subject: "Jenkins Pipeline Failure",
                     body: "Pipeline execution failed. Log file attached.",
                     to: "${RECIPIENT_EMAIL}",
                     attachmentsPattern: "${LOG_FILE}"
        }
    }
}
