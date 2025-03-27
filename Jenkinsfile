pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'deepanshu@gmail.com'
        USER_EMAIL = 'dipanshugarg13@gmail.com'
        AWS_CREDENTIALS = credentials('aws-credentials')
    }

    tools {
        maven 'Maven 3.8.1'  // Maven for build and testing
        jdk 'JDK 11'         // Java Development Kit
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Cloning repository from GitHub...'
                git 'https://github.com/your-repo.git'  // Replace with actual repository URL
            }
        }

        stage('Build') {
            tools {
                maven 'Maven 3.8.1'
            }
            steps {
                echo 'Building the application using Maven...'
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Unit and Integration Tests') {
            tools {
                maven 'Maven 3.8.1'
            }
            steps {
                echo 'Running unit tests with JUnit...'
                sh 'mvn test'

                echo 'Running integration tests with Selenium...'
                sh 'mvn verify'
            }
        }

        stage('Code Analysis') {
            tools {
                sonarQube 'SonarQube'  // SonarQube for code quality analysis
            }
            steps {
                echo 'Analyzing code using SonarQube...'
                sh 'mvn sonar:sonar'
            }
        }

        stage('Security Scan') {
            tools {
                dependencyCheck 'OWASP Dependency Check'  // OWASP for security scanning
            }
            steps {
                echo 'Performing security scan with OWASP Dependency Check...'
                sh 'mvn org.owasp:dependency-check-maven:check'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to AWS EC2 Staging server...'
                sh '''
                scp -i $AWS_CREDENTIALS target/my-app.jar ec2-user@staging-server:/home/ec2-user/
                ssh -i $AWS_CREDENTIALS ec2-user@staging-server 'nohup java -jar /home/ec2-user/my-app.jar > output.log 2>&1 &'
                '''
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Selenium integration tests on Staging...'
                sh 'mvn verify -Denv=staging'
            }
        }

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
