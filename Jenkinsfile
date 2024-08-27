pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                // Example using Maven
                sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Example using JUnit
                sh 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code...'
                // Example using SonarQube
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Example using OWASP ZAP or Snyk
                sh 'snyk test'  // Replace with OWASP ZAP or other tools if needed
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                // Example deployment to AWS EC2
                sh 'aws s3 cp target/myapp.war s3://my-staging-bucket/'
                sh 'aws deploy start-deployment --application-name MyAppStaging --deployment-group-name MyStagingGroup --s3-location bucket=my-staging-bucket,key=myapp.war'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Example using Postman or Selenium
                sh 'newman run postman_collection.json'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                // Example deployment to AWS EC2
                sh 'aws s3 cp target/myapp.war s3://my-prod-bucket/'
                sh 'aws deploy start-deployment --application-name MyAppProd --deployment-group-name MyProdGroup --s3-location bucket=my-prod-bucket,key=myapp.war'
            }
        }
    }
    
    post {
        always {
            mail to: 'developer@example.com',
                 subject: "Jenkins Pipeline - ${currentBuild.fullDisplayName}",
                 body: "Status: ${currentBuild.currentResult}\n\nLogs: ${env.BUILD_URL}console",
                 attachLog: true
        }
    }
}
