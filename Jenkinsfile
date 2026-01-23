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
                echo 'mvn clean verify'
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
