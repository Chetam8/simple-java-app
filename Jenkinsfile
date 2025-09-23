pipeline {
    agent any

    tools {
        maven 'Maven3'   // Make sure Maven is installed and configured in Jenkins
        jdk 'JDK17'      // Use JDK version available in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Chetam8/simple-java-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully'
        }
        failure {
            echo 'Build failed ❌'
        }
    }
}
