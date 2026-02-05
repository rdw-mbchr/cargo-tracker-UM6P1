pipeline {
    agent any

    triggers {
        githubPush()
    }

    environment {
        // Remplacez 'sonar-token' par l'ID de vos credentials Jenkins
        SONAR_TOKEN = credentials('sonar-token')
        MAVEN_HOME = tool name: 'Maven-3.9', type: 'maven'
    }
    tools {
    git 'Default'
    }


    stages {

        stage('Clone Repository') {
            steps {
                echo "📥 Cloning repository..."
                git branch: 'develop', url: 'https://github.com/akito-sama/cargo-tracker.git'
            }
        }

        stage('Compile') {
            steps {
                echo "🔨 Compiling the project..."
                bat "\"%MAVEN_HOME%\\bin\\mvn\" clean compile"
            }
        }

        stage('Unit Tests') {
            steps {
                echo "🧪 Running unit tests..."
                bat "\"%MAVEN_HOME%\\bin\\mvn\" test"
            }
        }

        stage('Package') {
            steps {
                echo "📦 Packaging the application..."
                bat "\"%MAVEN_HOME%\\bin\\mvn\" package"
            }
        }

        stage('SonarQube Analysis') {
            steps {
                echo "🔍 Running SonarQube analysis..."
                bat "\"%MAVEN_HOME%\\bin\\mvn\" sonar:sonar -Dsonar.projectKey=CargoTracker -Dsonar.host.url=http://localhost:9000 -Dsonar.login=%SONAR_TOKEN%"
            }
        }
    }

    post {
        success {
            echo '✅ Build, tests et analyse SonarQube terminés avec succès !'
        }
        failure {
            echo '❌ Échec du build, des tests ou de l’analyse SonarQube.'
        }
    }
}
