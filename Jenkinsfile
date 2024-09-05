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

        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan with OWASP Dependency-Check...'
                    sh 'mvn org.owasp:dependency-check-maven:check'
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
            emailext to: 'shaharyarnadeem786@gmail.com', // Your email address
                     attachLog: true,
                     body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                     subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
        }
        failure {
            emailext to: 'shaharyarnadeem786@gmail.com', // Your email address
                     attachLog: true,
                     body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                     subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
        }
    }
}
