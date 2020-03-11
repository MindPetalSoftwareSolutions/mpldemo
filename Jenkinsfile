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
            steps {
                script {
                    scannerHome = tool 'SonarScanner'
                }
                withSonarQubeEnv('Vertical Apps SonarQube') {
                    bat "\"${scannerHome}\\bin\\sonar-scanner.bat\" -D sonar.projectKey=${env.JOB_NAME}"
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