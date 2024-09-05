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
                    sh 'mvn clean package'
                }
            }
        }

        stage('Run Unit Tests') {
            steps {
                script {
                    echo 'Running unit tests...'
                    sh 'mvn test'
                }
            }
        }

        /*
        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan with OWASP Dependency-Check...'
                    sh 'mvn org.owasp:dependency-check-maven:check -Ddata.directory=dependency-check-data'
                }
            }
        }
        */

        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests on staging...'
                    // Add commands for integration tests if applicable
                    echo 'Integration testing step...'
                }
            }
        }
    }

    post {
        success {
            script {
                def logFile = 'build.log'
                sh "echo 'Build completed successfully' > ${logFile}" // Generate a log file for the successful build
                archiveArtifacts artifacts: "${logFile}", allowEmptyArchive: true // Archive the log file
                mail to: 'shaharyarnadeem786@gmail.com',
                     subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                     body: "The build was successful. See details at: ${env.BUILD_URL}"
            }
        }
        failure {
            script {
                def logFile = 'build.log'
                sh "echo 'Build failed' > ${logFile}" // Generate a log file for the failed build
                archiveArtifacts artifacts: "${logFile}", allowEmptyArchive: true // Archive the log file
                mail to: 'shaharyarnadeem786@gmail.com',
                     subject: "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                     body: "The build failed. Check the logs at: ${env.BUILD_URL}"
            }
        }
    }
} 
