pipeline {
    agent any
    environment {
        DIRECTORY_PATH = '' 
        TEST_ENV = 'staging'
        PROD_ENV = 'production'
        EMAIL = 'hasinduwelarathne@gmail.com'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Build the code using Maven'
                echo 'Running: mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests with JUnit'
                echo 'Running integration tests with Selenium'
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true 
                    emailext (
                        to: env.EMAIL,
                        subject: "Unit & Integration Tests Status: ${currentBuild.currentResult}",
                        body: "The Unit & Integration tests have ${currentBuild.currentResult}.\nCheck logs for details.",
                        attachmentsPattern: '**/*.log' 
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Scanning code for security vulnerabilities using OWASP Dependency Check'
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true  
                    emailext (
                        to: env.EMAIL,
                        subject: "Security Scan Status: ${currentBuild.currentResult}",
                        body: "The Security scan has ${currentBuild.currentResult}.\nCheck logs for details.",
                        attachmentsPattern: '**/*.log' 
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment'
            }
        }
    }
}

