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
                // Create a dummy log file
                writeFile file: 'test.log', text: 'Unit tests and integration tests completed successfully.'
            }
            post {
                always {
                    archiveArtifacts artifacts: 'test.log', allowEmptyArchive: true
                    emailext (
                        to: env.EMAIL,
                        subject: "Unit & Integration Tests Status: ${currentBuild.currentResult}",
                        body: "The Unit & Integration tests have ${currentBuild.currentResult}.\nCheck the attached log for details.",
                        attachmentsPattern: 'test.log'  
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code with SonarQube'
                // Create a dummy log for this stage
                writeFile file: 'code-analysis.log', text: 'Code analysis completed successfully.'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Scanning code for security vulnerabilities using OWASP Dependency Check'
                // Create a dummy log for this stage
                writeFile file: 'security-scan.log', text: 'Security scan completed successfully.'
            }
            post {
                always {
                    archiveArtifacts artifacts: 'security-scan.log', allowEmptyArchive: true
                    emailext (
                        to: env.EMAIL,
                        subject: "Security Scan Status: ${currentBuild.currentResult}",
                        body: "The Security scan has ${currentBuild.currentResult}.\nCheck the attached log for details.",
                        attachmentsPattern: 'security-scan.log'
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


