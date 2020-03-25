@Library('jenkins-shared-library@Justin-dev') _

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
                sonarQubeScan()
            }
        }
        stage('Build') {
            steps {
                bat """
                    "C:\Program Files (x86)\UiPath\Studio\UiRobot.exe" pack "${env:WORKSPACE}\project.json" -o "{$env:JENKINS_HOME}\jobs\${env:JOB_NAME}\builds\${env:BUILD_NUMBER}"
                """
            }
        }
        stage('Orch Publish') {
            steps {
               orchPublish() 
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