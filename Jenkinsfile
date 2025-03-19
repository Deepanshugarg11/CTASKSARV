pipeline {
    agent any
    
    // Environment variables
    environment {
        EMAIL_RECIPIENT = 'deepanshu@gmail.com'  // Email for security scan and other important notifications
        USER_EMAIL = 'dipanshugarg13@gmail.com' // User email to receive step completion notifications
    }
    
    stages {
        // Stage 1: Build
        stage('Build') {
            steps {
                echo 'Building the application...' // Log message for build step
            }
            post {
                always {
                    // Send email notification after the build step
                    mail to: "${USER_EMAIL}",
                         subject: "Build Stage Completed",
                         body: "The build stage has completed. Check Jenkins logs for details."
                }
            }
        }
        
        // Stage 2: Unit and Integration Tests
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...' // Log message for test step
            }
            post {
                always {
                    // Send email notification after unit and integration tests
                    mail to: "${USER_EMAIL}",
                         subject: "Unit and Integration Tests Completed",
                         body: "The unit and integration tests have completed. Check Jenkins logs for details."
                }
            }
        }
        
        // Stage 3: Code Analysis
        stage('Code Analysis') {
            steps {
                echo 'Performing static code analysis...' // Log message for code analysis step
            }
            post {
                always {
                    // Send email notification after code analysis
                    mail to: "${USER_EMAIL}",
                         subject: "Code Analysis Completed",
                         body: "The code analysis stage has completed. Check Jenkins logs for details."
                }
            }
        }
        
        // Stage 4: Security Scan
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...' // Log message for security scan step
            }
            post {
                always {
                    // Send email notification after security scan
                    mail to: "${USER_EMAIL}",
                         subject: "Security Scan Completed",
                         body: "The security scan has completed. Check the Jenkins logs for details."
                }
            }
        }
        
        // Stage 5: Deploy to Staging
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...' // Log message for staging deployment step
            }
            post {
                always {
                    // Send email notification after deploying to staging
                    mail to: "${USER_EMAIL}",
                         subject: "Deployment to Staging Completed",
                         body: "Deployment to the staging environment has completed. Check Jenkins logs for details."
                }
            }
        }
        
        // Stage 6: Integration Tests on Staging
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...' // Log message for integration tests on staging step
            }
            post {
                always {
                    // Send email notification after integration tests on staging
                    mail to: "${USER_EMAIL}",
                         subject: "Integration Tests on Staging Completed",
                         body: "Integration tests on staging have completed. Check Jenkins logs for details."
                }
            }
        }
        
        // Stage 7: Deploy to Production
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...' // Log message for production deployment step
            }
            post {
                always {
                    // Send email notification after deploying to production
                    mail to: "${USER_EMAIL}",
                         subject: "Deployment to Production Completed",
                         body: "Deployment to production has completed. Check Jenkins logs for details."
                }
            }
        }
    }
    
    // Post actions after all stages
    post {
        success {
            // Success notification after pipeline completion
            echo 'Pipeline executed successfully!'
            mail to: "${USER_EMAIL}",
                 subject: "Pipeline Execution Successful",
                 body: "The entire pipeline has completed successfully."
        }
        failure {
            // Failure notification if any stage fails
            echo 'Pipeline failed! Check the logs for more details.'
            mail to: "${USER_EMAIL}",
                 subject: "Pipeline Execution Failed",
                 body: "The pipeline has failed. Please check the Jenkins logs for more details."
        }
    }
}
