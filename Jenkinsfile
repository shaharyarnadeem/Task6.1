pipeline {
    agent any

    tools {
        maven 'My Maven' // Replace with your Maven installation name in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    echo 'Building the application...'
                    // Redirect both stdout and stderr to the build.log file
                    sh 'mvn clean package > build.log 2>&1'
                }
            }
        }

        stage('Run Unit Tests') {
            steps {
                script {
                    echo 'Running unit tests...'
                    // Redirect both stdout and stderr to the build.log file
                    sh 'mvn test >> build.log 2>&1'
                }
            }
        }

        /*
        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan with OWASP Dependency-Check...'
                    sh 'mvn org.owasp:dependency-check-maven:check -Ddata.directory=dependency-check-data >> build.log 2>&1'
                }
            }
        }
        */

        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests on staging...'
                    // Redirect both stdout and stderr to the build.log file
                    echo 'Integration testing step...' >> build.log 
                }
            }
        }
    }

    post {
        success {
            script {
                archiveArtifacts artifacts: 'build.log', allowEmptyArchive: true // Archive the log file
                emailext to: 'shaharyarnadeem786@gmail.com',
                         subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                         body: "The build was successful. See details at: ${env.BUILD_URL}",
                         attachLog: true // Attach the build log to the email
            }
        }
        failure {
            script {
                archiveArtifacts artifacts: 'build.log', allowEmptyArchive: true // Archive the log file
                emailext to: 'shaharyarnadeem786@gmail.com',
                         subject: "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                         body: "The build failed. Check the logs at: ${env.BUILD_URL}",
                         attachLog: true // Attach the build log to the email
            }
        }
    }
}
