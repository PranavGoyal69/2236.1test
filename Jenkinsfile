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
                script {
                    def buildLog = ''
                    buildLog += sh(script: 'echo "Building the code using a build automation tool (e.g., Maven)"', returnStdout: true)
                    echo buildLog
                }
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                script {
                    def testLog = ''
                    testLog += sh(script: 'echo "Running unit tests and integration tests"', returnStdout: true)
                    echo testLog
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                script {
                    def analysisLog = ''
                    analysisLog += sh(script: 'echo "Integrating a code analysis tool to analyze the code"', returnStdout: true)
                    echo analysisLog
                }
            }
        }
        
        stage('Security Scan') {
            steps {
                script {
                    def securityLog = ''
                    securityLog += sh(script: 'echo "Performing a security scan on the code"', returnStdout: true)
                    echo securityLog
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                script {
                    def deployLog = ''
                    deployLog += sh(script: 'echo "Deploying the application to a staging server"', returnStdout: true)
                    echo deployLog
                }
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                script {
                    def integrationLog = ''
                    integrationLog += sh(script: 'echo "Running integration tests on the staging environment"', returnStdout: true)
                    echo integrationLog
                }
            }
        }
        
        stage('Deploy to Production') {
            steps {
                script {
                    def productionLog = ''
                    productionLog += sh(script: 'echo "Deploying the application to a production server"', returnStdout: true)
                    echo productionLog
                }
            }
        }
    }
    
    post {
        always {
            script {
                // Collecting logs
                def logs = sh(script: 'tail -n 100 ${JENKINS_HOME}/jobs/${JOB_NAME}/builds/${BUILD_NUMBER}/log', returnStdout: true)
                writeFile file: 'build.log', text: logs
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
