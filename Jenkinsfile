pipeline {
    agent none

    stages {
        stage('Build and test C#') {
            agent {
                docker { image 'mcr.microsoft.com/dotnet/sdk:5.0' }
            }
            steps {
                sh 'dotnet build'
                sh 'dotnet test' 
            }
        }
        stage('Build and test Javascipt') {
            agent {
                docker { image 'node:14-alpine' }
            }
            steps{
                dir("DotnetTemplate.Web") {
                    sh 'npm install'
                    sh 'npm run build'
                    sh 'npm run lint'
                    sh 'npm t'
                }
            }
        }
    }
}