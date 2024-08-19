pipeline {
    agent any
    stages {
        // Stage 1: Build
        stage('Build') {
            steps {
                echo "Building the application using Maven: sh 'mvn clean package'"
                // Example build tool: Maven
            }
        }

        // Stage 2: Unit and Integration Tests
        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit and integration tests: sh 'mvn test'"
            }
            post {
                always {
                    emailext subject: "Test Stage: SUCCESS",
                        body: "The Test stage completed successfully.",
                        to: 'pm.thuytruc@gmail.com'
                }
                failure {
                    emailext (
                        subject: "Test Stage: FAILURE",
                        body: "The Test stage failed. Please check the attached log for details.",
                        to: "pm.thuytruc@gmail.com"
                    )
                }
            }
        }

        // Stage 3: Code Analysis
        stage('Code Analysis') {
            steps {
                echo "Performing code analysis: sh 'sonar-scanner'"
                // Example code analysis tool: SonarQube
            }
        }

        // Stage 4: Security Scan
        stage('Security Scan') {
            steps {
                echo "Performing security scan using OWASP ZAP: sh 'zap-cli -t http://localhost:8080'"
                // Use ZAP for security scanning
            }
            post {
                success {
                    emailext (
                        subject: "Security Scan: SUCCESS",
                        body: "The Security Scan stage completed successfully.",
                        to: "pm.thuytruc@gmail.com"
                    )
                }
                failure {
                    emailext (
                        subject: "Security Scan: FAILURE",
                        body: "The Security Scan stage failed. Please check the attached log for details.",
                        to: "pm.thuytruc@gmail.com"
                    )
                }
            }
        }

        // Stage 5: Deploy to Staging
        stage('Deploy to Staging') {
            steps {
                echo "Deploying to staging environment: sh 'aws ec2 run-instances ...'"
                // Use AWS CLI for deployment
            }
        }

        // Stage 6: Integration Tests on Staging
        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on the staging environment: Postman"
            }
        }

        // Stage 7: Deploy to Production
        stage('Deploy to Production') {
            steps {
                echo "Deploying to production: sh 'aws ec2 run-instances ...'"
                // Use AWS CLI for deployment
            }
        }
    }
}
