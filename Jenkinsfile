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
            emailext attachLog: true, body: 'success', subject: 'the build was successful', to: 'shaharyarnadeem786@gmail.com '
                    
        }
        failure {
            emailext attachLog: true, body: 'failure', subject: 'the build failed', to: 'shaharyarnadeem786@gmail.com '
                    
            }
        }
    }

