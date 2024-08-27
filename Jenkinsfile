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
                    // Replace with an actual command for OWASP Dependency-Check if needed
                    sh 'mvn org.owasp:dependency-check-maven:check'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                // Example: Deploy using a script
                sh './deploy_staging.sh'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Example: Use a placeholder for integration tests
                echo 'Integration testing step...'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment...'
                // Example: Deploy using a script
                sh './deploy_production.sh'
            }
        }
    }

    post {
        success {
            mail to: 'shaharyarnadeem786@gmail.com',
                 subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The build was successful. See details at: ${env.BUILD_URL}"
        }
        failure {
            mail to: 'shaharyarnadeem786@gmail.com',
                 subject: "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The build failed. Check the logs at: ${env.BUILD_URL}"
        }
    }
}

 
