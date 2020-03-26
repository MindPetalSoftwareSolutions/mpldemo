@Library('jenkins-shared-library@Justin-dev') _

pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                gitCheckout(
                    branch: "quality-fail",
                    url: 'https://github.com/VerticalApps-DevOps/rpa-ex.git'
                )
            }
        }
        stage('Build') {
            steps {
                pack()
            }
        }
    }
}