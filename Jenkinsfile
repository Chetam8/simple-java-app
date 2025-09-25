pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'Java17'
    }

    environment {
        JAVA_HOME = tool name: 'Java17', type: 'jdk'
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
        AWS_REGION = 'us-east-1' // change to your AWS region
        ECR_REPO = '375539415994.dkr.ecr.us-east-1.amazonaws.com/simple-repo' // replace with your ECR repo URI
        IMAGE_TAG = 'latest'
    }

    stages {
        stage('Verify Java') {
            steps {
                sh 'echo JAVA_HOME=$JAVA_HOME'
                sh 'java -version'
                sh 'mvn -v'
            }
        }

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

        // --- Docker stages ---
        stage('Docker Build') {
            steps {
                echo 'Building Docker image...'
                sh "docker build -t my-app:${IMAGE_TAG} ."
            }
        }

        stage('Docker Push to ECR') {
            steps {
                echo 'Logging into AWS ECR and pushing image...'
                sh '''
                    aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $ECR_REPO
                    docker tag my-app:${IMAGE_TAG} $ECR_REPO:${IMAGE_TAG}
                    docker push $ECR_REPO:${IMAGE_TAG}
                '''
            }
        }
    }

    post {
        success {
            echo 'Build and Docker push completed successfully'
        }
        failure {
            echo 'Build failed'
        }
    }
}
