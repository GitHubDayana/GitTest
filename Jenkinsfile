pipeline {
    agent any

    environment {
        // Define any environment variables you need
        DOTNET_VERSION = '6.0'
        BUILD_DIR = 'build'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from your source control
                checkout scm
            }
        }

        stage('Restore') {
            steps {
                // Restore NuGet packages
                script {
                    sh 'dotnet restore'
                }
            }
        }

        stage('Build') {
            steps {
                // Build the .NET project
                script {
                    sh 'dotnet build --configuration Release'
                }
            }
        }

        stage('Test') {
            steps {
                // Run unit tests
                script {
                    sh 'dotnet test --configuration Release --no-build'
                }
            }
        }

        stage('Publish') {
            steps {
                // Publish the application
                script {
                    sh 'dotnet publish --configuration Release --output ${BUILD_DIR}'
                }
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the application to the server
                // This example assumes you’re using SCP for deployment; adjust as needed for your deployment method
                script {
                    sshagent(['deploy-key-id']) {
                        sh 'scp -r ${BUILD_DIR} user@server:/path/to/deploy'
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
