@Library('jenkins-shared-library@Justin-dev') _

pipeline {
    def cmd_exec(command) {
        return bat(returnStdout: true, script: "${command}").trim()
    }
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
                cmd_exec("\"C:\Program Files (x86)\UiPath\Studio\UiRobot.exe\" pack \"$env:WORKSPACE\project.json\" -o \"$env:JENKINS_HOME\jobs\$env:JOB_NAME\builds\$env:BUILD_NUMBER\"")
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