pipeline {
    agent any
    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }
    environment {
        AGENT_NAME='Jye'
        PROJECT_NAME='6.2c-Jenkins-pipeline'
        LINUX_DIRECTORY_PATH='/usr/lib/jenkins/'
        WINDOWS_DIRECTORY_PATH='C:\Users\Jenkins\AppData\Local\Jenkins'
        SNYK_NAME='Snyk-test-6.2c'
        SNYK_TOKEN='15a91d71-3e72-4997-ae13-f0705c310275'
    }
    stages {
        stage('1: Build') {
            steps {
                echo 'Fetch the source code from the directory path specified by the environment variable'
                echo 'Compile the code and generate any necessary artifacts'

                // Get some code from a GitHub repository
                git 'https://github.com/jglick/simple-maven-project-with-tests.git'
                bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
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
                snykSecurity(
                    snkyInstallation: "<%{SNYK_NAME}>",
                    snykTokenID: '<%{SNYK_TOKEN}>',
                    projectName: '%{PROJECT_NAME}',
                    failOnError
            }
        }
        stage('5: Deploy to staging server') {
            steps {
                echo "waiting for approval of ${AGENT_NAME}.."
                sleep 3
            }
        }
        stage('6. Staging integration tests') {
            steps {
                echo "Reapplying checks with security measures."
                sleep 3
            }
        }
        stage('7. Deploy to production') {
            steps {
                echo 'Testing environment:'
                echo "${TESTING_ENVIRONMENT}"
                echo 'Production environment:'
                echo "${PRODUCTION_ENVIRONMENT}"
                echo 'Finished!'
            }
        }
    }
}
