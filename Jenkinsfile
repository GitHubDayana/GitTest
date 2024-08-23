pipeline {
    agent any

    environment {
        // Define any environment variables if needed
        DOTNET_ROOT = 'C:\\Program Files\\dotnet' // Adjust this path based on your environment
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                checkout scm
            }
        }
        
        stage('Restore') {
            steps {
                script {
                    // Restore the .NET project dependencies
                    sh 'dotnet restore'
                }
            }
        }
        
        stage('Build') {
            steps {
                script {
                    // Build the .NET project
                    sh 'dotnet build --configuration Release'
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    // Run the tests
                    sh 'dotnet test --no-build --verbosity normal'
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    // Publish the project to a folder
                    sh 'dotnet publish --configuration Release --output ./publish'
                }
            }
        }
    }

    post {
        success {
            echo 'Build and deployment succeeded!'
        }
        
        failure {
            echo 'Build or deployment failed!'
        }
        
        always {
            cleanWs()
        }
    }
}
