pipeline {
    agent {
        docker { image 'node:14-alpine' }
    }
    stages {
        stage('Build') {
            steps {
                sh 'dotnet build'
                sh 'dotnet test' 
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