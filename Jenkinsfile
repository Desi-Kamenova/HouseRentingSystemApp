pipeline {
    agent any

    stages {
        stage('Checkout code') {
            steps {
                // Checkout code from GitHub and specify the branch
                git branch: 'main', url: 'https://github.com/Desi-Kamenova/HouseRentingSystemApp.git'
            }
        }

        stage('Restoring nuget packages') {
            steps {
                bat 'dotnet restore HouseRentingSystem.sln'
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet build HouseRentingSystem.sln --configuration Release'
            }
        }

        stage('Run TestProject tests') {
            steps {
                bat 'dotnet test HouseRentingSystem.Tests/HouseRentingSystem.Tests.csproj --logger "trx;LogFileName=TestResults1.trx"' 
            }
        }

    }

    post {
        always {
            archiveArtifacts artifacts: '**/TestResults1/*.trx', allowEmptyArchive: true
            step([
                $class: 'MSTestPublisher',
                testResultsFile: '**/TestResults1/*.trx'
            ])
        }
    }
}