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
        stage('Build') {
            steps {
                bat """
                    "C:/Program Files (x86)/UiPath/Studio/UiRobot.exe" pack "${env:WORKSPACE}/project.json" -o "${env:JENKINS_HOME}/jobs/${env:JOB_NAME}/builds/${env:BUILD_NUMBER}"
                """

            }
        }
    }
}