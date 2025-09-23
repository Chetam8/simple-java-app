pipeline {
    agent any

    tools {
        maven 'Maven3'   // Make sure Jenkins has Maven installed & named "Maven3"
        jdk 'JDK11'      // Make sure Jenkins has JDK installed & named "JDK11"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Chetam8/simple-java-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
    }
}
