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
                    sh 'mvn clean package > build.log 2>&1' // Redirect output to build.log
                }
            }
        }

        stage('Run Unit Tests') {
            steps {
                script {
                    echo 'Running unit tests...'
                    sh 'mvn test >> build.log 2>&1' // Append output to build.log
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan with OWASP Dependency-Check...'
                    sh 'mvn org.owasp:dependency-check-maven:check >> build.log 2>&1' // Append output to build.log
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests on staging...'
                    echo 'Integration testing step...' >> build.log 2>&1 // Append output to build.log
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to production environment...'
                    echo 'Production deployment step...' >> build.log 2>&1 // Append output to build.log
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'build.log', allowEmptyArchive: true // Archive the log file
        }
        success {
            mail to: 'shaharyarnadeem786@gmail.com',
                 subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The build was successful. See details at: ${env.BUILD_URL}",
                 attachments: 'build.log' // Attach the log file
        }
        failure {
            mail to: 'shaharyarnadeem786@gmail.com',
                 subject: "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The build failed. Check the logs at: ${env.BUILD_URL}",
                 attachments: 'build.log' // Attach the log file
        }
    }
}
