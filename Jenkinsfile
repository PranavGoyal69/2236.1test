pipeline {
    agent any
    
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                echo 'Building the code using a build automation tool (e.g., Maven)'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests and integration tests'
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Integrating a code analysis tool to analyze the code'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing a security scan on the code'
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying the application to a staging server'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on the staging environment'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying the application to a production server'
            }
        }
    }
    
    post {
        success {
            mail(
                to: 'gpranav2901@gmail.com',
                subject: 'Build Successful',
                body: 'Build completed successfully'
            )
        }
        failure {
            mail(
                to: 'gpranav2901@gmail.com',
                subject: 'Build Failed',
                body: 'Build failed'
            )
        }
    }
}
