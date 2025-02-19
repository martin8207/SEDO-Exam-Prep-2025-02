pipeline {
    agent any
    
    environment {
        DOTNET_VERSION = '6.0'  // Specify .NET version
        SOLUTION_FILE = 'HouseRentingSystem.sln'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Setup .NET') {
            steps {
                // Install .NET SDK 6.0
                sh '''
                    wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
                    sudo dpkg -i packages-microsoft-prod.deb
                    sudo apt-get update
                    sudo apt-get install -y dotnet-sdk-6.0
                '''
            }
        }
        
        stage('Restore Dependencies') {
            steps {
                sh 'dotnet restore'
            }
        }
        
        stage('Build') {
            steps {
                sh 'dotnet build --no-restore'
            }
        }
        
        stage('Run Unit Tests') {
            steps {
                sh 'dotnet test HouseRentingSystem.UnitTests --no-build --verbosity normal'
            }
        }
    }

    post {
        always {
            // Clean workspace after build
            cleanWs()
        }
    }
}