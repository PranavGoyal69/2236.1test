pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                // Ensure Git is available
                bat 'git --version'
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                script {
                    try {
                        // Example build command for Windows, replace with your actual build tool command
                        bat 'mvn clean install'
                    } catch (Exception e) {
                        echo "Build failed: ${e.getMessage()}"
                        currentBuild.result = 'FAILURE'
                        error("Build failed")
                    }
                }
            }
        }
        
        stage('Unit and Integration Tests') {
            when {
                expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                script {
                    try {
                        // Run tests, example for Maven, replace with your actual command
                        bat 'mvn test'
                    } catch (Exception e) {
                        echo "Tests failed: ${e.getMessage()}"
                        currentBuild.result = 'FAILURE'
                        error("Tests failed")
                    }
                }
            }
        }
        
        stage('Code Analysis') {
            when {
                expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                script {
                    try {
                        // Run code analysis tool, replace with your actual command
                        bat 'mvn sonar:sonar'
                    } catch (Exception e) {
                        echo "Code analysis failed: ${e.getMessage()}"
                        currentBuild.result = 'FAILURE'
                        error("Code analysis failed")
                    }
                }
            }
        }
        
        stage('Security Scan') {
            when {
                expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                script {
                    try {
                        // Run security scan tool, replace with your actual command
                        bat 'dependency-check.bat --scan . --format XML'
                    } catch (Exception e) {
                        echo "Security scan failed: ${e.getMessage()}"
                        currentBuild.result = 'FAILURE'
                        error("Security scan failed")
                    }
                }
            }
        }
        
        stage('Deploy to Staging') {
            when {
                expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                script {
                    try {
                        // Deploy to staging, replace with your actual command
                        bat 'deploy-to-staging.bat'
                    } catch (Exception e) {
                        echo "Staging deployment failed: ${e.getMessage()}"
                        currentBuild.result = 'FAILURE'
                        error("Staging deployment failed")
                    }
                }
            }
        }
        
        stage('Integration Tests on Staging') {
            when {
                expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                script {
                    try {
                        // Run integration tests on staging, replace with your actual command
                        bat 'run-integration-tests.bat'
                    } catch (Exception e) {
                        echo "Integration tests on staging failed: ${e.getMessage()}"
                        currentBuild.result = 'FAILURE'
                        error("Integration tests on staging failed")
                    }
                }
            }
        }
        
        stage('Deploy to Production') {
            when {
                expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                script {
                    try {
                        // Deploy to production, replace with your actual command
                        bat 'deploy-to-production.bat'
                    } catch (Exception e) {
                        echo "Production deployment failed: ${e.getMessage()}"
                        currentBuild.result = 'FAILURE'
                        error("Production deployment failed")
                    }
                }
            }
        }
    }

    post {
        always {
            script {
                // Collect and archive logs
                archiveArtifacts artifacts: '**/target/*.log', allowEmptyArchive: true
            }
        }
        success {
            emailext(
                subject: 'Build Successful',
                body: 'Build completed successfully',
                to: 'gpranav2901@gmail.com'
            )
        }
        failure {
            emailext(
                subject: 'Build Failed',
                body: 'Build failed. Please check the logs.',
                to: 'gpranav2901@gmail.com'
            )
        }
    }
}
