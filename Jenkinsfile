pipeline {
    agent any
    environment {
        NAME='Jye'
        TESTING_ENVIRONMENT='TESTING_ENVIRONMENT'
        PRODUCTION_ENVIRONMENT='PRODUCTION_ENVIRONMENT'
        DIRECTORY_PATH='DIRECTORY_PATH'
    }
    stages {
        stage('1: Build') {
            steps {
                echo 'Fetch the source code from the directory path specified by the environment variable'
                echo 'Compile the code and generate any necessary artifacts'
            }
        }
        stage('2: Unit and Integration Tests') {
            steps {
                echo 'Unit tests'
                echo 'Integration tests'
            }
        }
        stage('3: Code Analysis') {
            steps {
                echo 'Ensure code meets industry standards'
            }
        }
        stage('4: Security Scan') {
            steps {
                echo 'Check the quality of the code'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy the application to a testing environment specified by the environment variable'
            }
        }
        stage('Approval') {
            steps {
                echo "waiting for approval of ${NAME}.."
                sleep 10
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Testing environment:'
                echo "${TESTING_ENVIRONMENT}"
                echo 'Production environment:'
                echo "${PRODUCTION_ENVIRONMENT}"
                echo 'Directory path:'
                echo "${DIRECTORY_PATH}"
                echo 'Finished!'
            }
        }
    }
}
