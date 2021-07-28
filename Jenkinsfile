pipeline {
    agent none

    environment {
        DOTNET_CLI_HOME="/tmp/dotnet_cli_home"
    }

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
                    sh 'npm run test-with-coverage'
                }
            }
            post {
                always {
                    publishCoverage adapters: [istanbulCoberturaAdapter(path: 'DotnetTemplate.Web/coverage/cobertura-coverage.xml', thresholds: [[failUnhealthy: true, thresholdTarget: 'Line', unhealthyThreshold: 90.0, unstableThreshold: 80.0]])], sourceFileResolver: sourceFiles('NEVER_STORE')
                }
            }
        }
    }
}