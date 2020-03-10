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
        stage('Package Transfer') {
            steps{
                packageTransfer()
            }
        }
        stage('Post-Build') {
            steps {
                postBuild()
            }
        }
    }
}