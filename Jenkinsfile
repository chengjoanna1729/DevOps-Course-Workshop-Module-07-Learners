pipeline {
    agent none

    stages {
        stage('Checkout code') {
            agent {
                docker { image 'node:14-alpine' }
            }
            steps {
                deleteDir()
                checkout scm
            }
        }
        stage('Build and test C# code') {
            agent {
                docker { image 'mcr.microsoft.com/dotnet/core/sdk:3.1' }
            }
            steps {
                echo 'Building..'
                sh 'dotnet build'
                echo 'Testing..'
                sh 'dotnet test'
            }
        }
    }
}