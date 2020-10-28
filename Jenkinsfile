pipeline {
    agent none

    stages {
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
                dir('DotnetTemplate.Web') {
                    sh 'npm install'
                    sh 'npm run build'
                    sh 'npm run lint'
                    sh 'npm t'
                }
            }
        }
    }
}