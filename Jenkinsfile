pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'deepanshu@gmail.com'
        USER_EMAIL = 'dipanshugarg13@gmail.com'
        AWS_CREDENTIALS = credentials('aws-credentials')
    }

    stages {
        // Stage 1: Build
        stage('Build') {
            steps {
                echo 'Building the application using Maven...'
                sh 'mvn clean package -DskipTests'
            }
        }

        // Stage 2: Unit and Integration Tests
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests with JUnit...'
                sh 'mvn test'

                echo 'Running integration tests with Selenium...'
                sh 'mvn verify'
            }
        }

        // Stage 3: Code Analysis
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code using SonarQube...'
                sh 'mvn sonar:sonar'
            }
        }

        // Stage 4: Security Scan
        stage('Security Scan') {
            steps {
                echo 'Performing security scan with OWASP Dependency Check...'
                sh 'mvn org.owasp:dependency-check-maven:check'
            }
        }

        // Stage 5: Deploy to Staging
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to AWS EC2 Staging server...'
                sh '''
                scp -i $AWS_CREDENTIALS target/my-app.jar ec2-user@staging-server:/home/ec2-user/
                ssh -i $AWS_CREDENTIALS ec2-user@staging-server 'nohup java -jar /home/ec2-user/my-app.jar > output.log 2>&1 &'
                '''
            }
        }

        // Stage 6: Integration Tests on Staging
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Selenium integration tests on Staging...'
                sh 'mvn verify -Denv=staging'
            }
        }

        // Stage 7: Deploy to Production
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to AWS EC2 Production server...'
                sh '''
                scp -i $AWS_CREDENTIALS target/my-app.jar ec2-user@production-server:/home/ec2-user/
                ssh -i $AWS_CREDENTIALS ec2-user@production-server 'nohup java -jar /home/ec2-user/my-app.jar > output.log 2>&1 &'
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
            mail to: "${USER_EMAIL}",
                 subject: "Pipeline Execution Successful",
                 body: "The entire pipeline has completed successfully."
        }
        failure {
            echo 'Pipeline failed! Check the logs for more details.'
            mail to: "${USER_EMAIL}",
                 subject: "Pipeline Execution Failed",
                 body: "The pipeline has failed. Please check the Jenkins logs for more details."
        }
    }
}
