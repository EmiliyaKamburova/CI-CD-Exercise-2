pipeline {
    agent any

    tools {
        // .NET SDK installed on Jenkins agent
        dotnet 'dotnet-sdk-8.0' // change this to match your Jenkins tool name
    }

    environment {
        DOTNET_CLI_TELEMETRY_OPTOUT = '1'
    }

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Restore') {
            steps {
                sh 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                sh 'dotnet build --no-restore --configuration Release'
            }
        }

        stage('Test') {
            steps {
                sh 'dotnet test --no-build --configuration Release --verbosity normal'
            }
        }
    }

    post {
        always {
            junit '**/TestResults/*.xml' // Adjust if your test project creates XML reports
            cleanWs()
        }
    }
}
