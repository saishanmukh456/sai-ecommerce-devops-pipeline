pipeline {
    agent any

    tools {
        maven 'mymaven'
    }

    stages {
        stage('1 - Checkout') {
            steps {
                checkout scm
            }
        }

        stage('2 - Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('3 - Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('4 - Docker Build') {
            steps {
                sh 'docker build -t ecommerce-app:${BUILD_NUMBER} .'
            }
        }

        stage('5 - Deploy') {
            steps {
                sh 'docker compose down'
                sh 'docker compose up -d --build'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful'
        }
        failure {
            echo 'Pipeline failed. Check the stage logs.'
        }
    }
}
