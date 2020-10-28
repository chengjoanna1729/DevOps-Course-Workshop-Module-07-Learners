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
            environment {
                DOTNET_CLI_HOME = "/tmp/DOTNET_CLI_HOME"
            }
            steps {
                sh 'dotnet build'
                sh 'dotnet test'
            }
        }
        stage('Build and test typescript code') {
            agent {
                docker { image 'node:14-alpine' }
            }
            steps {
                sh 'cd ./DevOps-Course-Workshop-Module-07-Learners/DotnetTemplate.Web'
                sh 'npm install'
                sh 'npm run build'
                sh 'npm run lint'
                sh 'npm t'
            }
        }
    }
}