pipeline {
    agent any

    triggers {
        githubPush()   
    }

    stages {

        stage('Clone') {
            steps {
                git branch: 'develop', url: 'https://github.com/akito-sama/cargo-tracker.git'
            }
        }

        stage('Build & Test with Coverage') {
            steps {
                script {
                    def mvnHome = tool name: 'Maven-3.9', type: 'maven'
                    bat "\"${mvnHome}\\bin\\mvn\" clean verify"
                }
            }
        }
    }
//
    post {
        success {
            echo 'Build et analyse terminés avec succès !'
        }
        failure {
            echo 'Échec du build ou des tests.'
        }
    }
}
