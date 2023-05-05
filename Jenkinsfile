pipeline {
    agent any
    environment {
        AGENT_NAME='Jye'
        PROJECT_NAME='6.2c-Jenkins-pipeline'
        OPSYS='windows' // lower-case, always
        LINUX_PATH='/usr/lib/jenkins/'
        LINUX_EXTENSION='.sh'
        WINDOWS_PATH='C:\\Users\\Jenkins\\AppData\\Local\\Jenkins'
        WINDOWS_EXTENSION='.bat'
        TESTING_ENVIRONMENT='Private Dockerhub'
        PRODUCTION_ENVIRONMENT='Dockerhub'
        // FORTIFY_HOME='C:\\Program Files\\Fortify\\Fortify_SCA_and_Apps_*'
        SNYK_NAME='Snyk-6.2c'
        SNYK_TOKEN='7189d1af-96c2-4460-95aa-e170508bdf46'
    }
    stages {
        stage('1: Build') {
            steps {
                script {
                    if (OPSYS == "windows") {
                        echo "${OPSYS}"
                        JENKINS_HOME=WINDOWS_PATH
                        JENKINS_EXTENSION=WINDOWS_EXTENSION
                        // works on Win and Linux, '\' or '/'
                        JMETER_HOME="${JENKINS_HOME}/apache-jmeter-*/"
                        // build scripts go here
                        // we don't have any real code so there are no pom.xml files..
                        // .. for maven to use. Below is an example of what we would do.
                        // withMaven {
                        //     bat "mvn clean verify"
                        // }
                    }
                    else if (OPSYS == "linux") {
                        echo "${OPSYS}"
                        JENKINS_HOME=LINUX_PATH
                        JENKINS_EXTENSION=LINUX_EXTENSION
                        JMETER_HOME="${JENKINS_HOME}/apache-jmeter-*/"
                        // build scripts go here
                    }
                    else {
                        echo 'something went wrong! OPERATING_SYSTEM was not detected.'
                        echo 'Maybe try manually setting your OPSYS variable?'
                    }
                }
                echo JENKINS_HOME
                echo JENKINS_EXTENSION
            }
        }
        stage('2: Unit and Integration Tests') {
            steps {
                echo 'Unit tests:'
                // run jmeter against each individual file? you would need a loop.
                echo 'Integration tests:'
                // bat "${JENKINS_HOME}${JMETER_HOME}${JENKINS_EXTENSION}"
                // script {
                //     bat """set OUT=jmeter.save.saveservice.output_format
                //     set JMX=${JMETER_HOME}bin/jenkins.io.jmx
                //     set JTL=${JMETER_HOME}reports/jenkins.io.report.jtl
                //     ${JMETER_HOME}bin/jmeter -j %OUT%=xml -n -t %JMX% -l %JTL%"""
                // }
                // This is going to fail because we haven't properly set a..
                // .. test proceedure file up yet. Outside 6.2c scope I think?
            }
            post {
                success {
                    script {
                        mail to: "s222134604@gmail.com",
                        subject: "Build status successful!",
                        body: "Congratulations, build ${BUILD_NUMBER} has passed testing inspection."
                    }
                    echo 'success! email sent.'
                }
            }
        }
        stage('3: Code Analysis') {
            steps {
                echo 'Static analysis of code, provided by Fortify'
                // script {
                //     fortifyScan buildID: "${env.BRANCH_NAME}${BUILD_NUMBER}"
                //     resultsFile: "${env.BRANCH_NAME}${BUILD_NUMBER}.fpr"
                //     logFile: "${env.BRANCH_NAME}${BUILD_NUMBER}-scan.log"
                    // fortifyUpload {}
                    // but I have nowhere to upload it too!
                // }
                // I can't run this script because I don't have a Fortify subscription
            }
            post {
                success {
                    echo 'Email log file to developer for inspection'
                    echo 'Filter and include largest relevant factors in email body'
                }
            }
        }
        stage('4: Security Scan') {
            steps {
                echo 'Inspect code for security flaws, according to Synk database'
                // script {
                //     snykSecurity projectName: '${PROJECT_NAME}',
                //     severity: 'medium',
                //     snykInstallation: "${SNYK_NAME}",
                //     snykTokenId: "${SNYK_TOKEN}"
                // }
                // This script will fail because there are no detected/supported..
                // .. target files in the build folder
            }
            post {
                success {
                    script {
                        mail to: "s222134604@gmail.com",
                        subject: "Build status successful!",
                        body: "Congratulations, build ${BUILD_NUMBER} has passed security requirements."
                    }
                    echo 'success! email sent.'
                }
            }
        }
        stage('5: Deploy to staging server') {
            steps {
                echo 'uploading to dockerhub testing environment:'
                echo "${TESTING_ENVIRONMENT}"
            }
        }
        stage('6. Staging integration tests') {
            steps {
                echo "Reapplying security checks in the staging environment"
                // script {
                //     snykSecurity projectName: '${PROJECT_NAME}',
                //     severity: 'medium',
                //     snykInstallation: "${SNYK_NAME}",
                //     snykTokenId: "${SNYK_TOKEN}"
                // }
                // This script will fail because there are no detected/supported..
                // .. target files in the build folder
            }
        }
        stage('7. Deploy to production') {
            steps {
                echo "waiting for approval of ${AGENT_NAME}.."
                sleep 3
                echo 'Production environment:'
                echo "${PRODUCTION_ENVIRONMENT}"
                echo 'Finished!'
            }
        }
    }
}