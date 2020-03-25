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
                    "C:/Program Files (x86)/UiPath/Studio/UiRobot.exe" pack "C:/Program Files (x86)/Jenkins/workspace/jlea-pipeline-test/project.json" -o "C:/Program Files (x86)/Jenkins/jobs/jlea-pipeline-test/builds/${env:BUILD_NUMBER}"
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