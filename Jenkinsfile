@Library('jenkins-shared-library@master') _

pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                gitCheckout(
                    branch: "master",
                    url: 'https://github.com/VerticalApps-DevOps/mpldemo.git'
                )
            }
        }
        stage('Orch Publish') {
            steps {
               orchPublish() 
            }
        }
        stage('Demo') {
            steps {
                sayHello()
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