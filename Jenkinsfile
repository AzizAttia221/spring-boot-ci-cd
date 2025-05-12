pipeline {
    agent any

    environment {
        // Replace with your SonarQube IP address - you'll need to get this from your environment
        SONAR_HOST_URL = 'http://YOUR_SONARQUBE_IP:9000'
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Your repository is already configured here
                git url: 'https://github.com/AzizAttia221/spring-boot-ci-cd.git', branch: 'master'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar-token') {
                    // You'll need to replace this with your SonarQube project key and token
                    sh 'mvn sonar:sonar -Dsonar.projectKey=YOUR_PROJECT_KEY -Dsonar.host.url=$SONAR_HOST_URL -Dsonar.login=YOUR_SONARQUBE_TOKEN'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t spring-boot-app:latest .'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}