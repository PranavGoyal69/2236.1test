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
        always {
            script {
                // Collecting logs
                def log = currentBuild.rawBuild.getLog(100).join('\n')
                writeFile file: 'build.log', text: log
                archiveArtifacts artifacts: 'build.log'
            }
        }
        
        success {
            emailext(
                subject: 'Build Successful',
                body: """
                Build completed successfully.
                Check the logs at: ${env.BUILD_URL}/artifact/build.log
                """,
                to: 'gpranav2901@gmail.com'
            )
        }
        
        failure {
            emailext(
                subject: 'Build Failed',
                body: """
                Build failed.
                Check the logs at: ${env.BUILD_URL}/artifact/build.log
                """,
                to: 'gpranav2901@gmail.com'
            )
        }
    }
}
