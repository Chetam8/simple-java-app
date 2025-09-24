pipeline {
    agent any

    tools {
        maven 'Maven3'    // Matches the Maven name configured in Jenkins
        jdk 'Java17'      // Matches the JDK name you configured
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
            echo ' Build completed successfully'
        }
        failure {
            echo ' Build failed'
        }
    }
}
