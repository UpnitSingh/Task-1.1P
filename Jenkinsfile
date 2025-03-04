pipeline {
    agent any

    environment {
        DIRECTORY_PATH = "https://github.com/UpnitSingh/Task-1.1P.git"
        TESTING_ENVIRONMENT = "Testing_Env"
        PRODUCTION_ENVIRONMENT = "Upnit_Singh"  
    }

    stages {
        stage('Build') {
            steps {
                echo "Fetch the source code from the directory path specified by the environment variable: ${DIRECTORY_PATH}"
                echo "Compile the code and generate any necessary artifacts"
            }
        }

        stage('Test') {
            steps {
                echo "Running unit tests"
                echo "Running integration tests"
            }
        }

        stage('Code Quality Check') {
            steps {
                echo "Checking the quality of the code"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploy the application to the testing environment specified by the environment variable: ${TESTING_ENVIRONMENT}"
            }
        }

        stage('Approval') {
            steps {
                echo "Waiting for manual approval..."
                sleep 10  // Simulate manual approval process
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying the application to the production environment: ${PRODUCTION_ENVIRONMENT}"
            }
        }
    }
}
