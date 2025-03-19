pipeline {
    agent any
    
    environment {
        EMAIL_RECIPIENT = 'deepanshu@gmail.com'
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                //sh 'mvn clean package' // Example: using Maven for Java projects
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                //sh 'mvn test' // Runs unit and integration tests
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Performing static code analysis...'
               // sh 'sonar-scanner' // Example: SonarQube for code analysis
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                //sh 'trivy fs .' // Example: Using Trivy for security vulnerability scanning
            }
            post {
                always {
                    mail to: "${EMAIL_RECIPIENT}", 
                        subject: "Security Scan Results", 
                        body: "The security scan has completed. Check the Jenkins logs for details."
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
               // sh 'mvn verify' // Example: running verification tests
            }
            post {
                always {
                    mail to: "${EMAIL_RECIPIENT}", 
                        subject: "Integration Test Results", 
                        body: "Integration tests on staging have completed. Check Jenkins logs for details."
                }
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed! Check the logs for more details.'
        }
    }
}
