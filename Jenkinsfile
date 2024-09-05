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
                    sh 'mvn clean package | tee build.log' // Save output to build.log
                }
            }
        }

        stage('Run Unit Tests') {
            steps {
                script {
                    echo 'Running unit tests...'
                    sh 'mvn test | tee test.log' // Save output to test.log
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan with OWASP Dependency-Check...'
                    sh 'mvn org.owasp:dependency-check-maven:check | tee security_scan.log' // Save output to security_scan.log
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests on staging...'
                    // Placeholder for integration tests
                    echo 'Integration testing step...'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to production environment...'
                    // Placeholder for deployment
                    echo 'Deployment step...'
                }
            }
        }
    }

    post {
        success {
            // Attach build log
            archiveArtifacts artifacts: 'build.log, test.log, security_scan.log', allowEmptyArchive: true
            
            mail to: 'shaharyarnadeem786@gmail.com',
                 subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The build was successful. See details at: ${env.BUILD_URL}",
                 attachments: 'build.log, test.log, security_scan.log'
        }
        failure {
            // Attach build log
            archiveArtifacts artifacts: 'build.log, test.log, security_scan.log', allowEmptyArchive: true

            mail to: 'shaharyarnadeem786@gmail.com',
                 subject: "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The build failed. Check the logs at: ${env.BUILD_URL}",
                 attachments: 'build.log, test.log, security_scan.log'
        }
    }
}
