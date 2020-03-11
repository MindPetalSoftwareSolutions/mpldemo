@Library('jenkins-shared-library@master') _

pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                gitCheckout(
                    branch: "master",
                    url: 'https://github.com/VerticalApps-DevOps/rpa-ex.git'
                )
            }
        }
        stage('Demo') {
            steps {
                sayHello()
            }
        }
        stage('Sonar') {
            environment {
                scannerHome = tool 'SonarScanner'
            }
            steps{
                withSonarQubeEnv('Vertical Apps SonarQube', credentialsId: 'SonarQube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
                timeout(time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        stage('Build') {
            steps {
                powershell returnStatus: true, script: '.\\build.ps1'
            }
        }
        stage('Powershell') {
            steps {
                psLibrary()
            }
        }
        stage('Orch Auth') {
            steps{
                orchAuth()
            }
        }
        stage('Post-Build') {
            steps {
                postBuild()
            }
        }
    }
}