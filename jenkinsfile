pipeline {
    agent any

    tools {
        jdk 'JDK-17'
        maven 'Maven-3.9'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/sahil-dighe-v8/javaapp.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean compile'
            }
        }

        stage('Unit Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                bat 'if not exist deploy mkdir deploy'
                bat 'copy /Y target\\*.jar deploy\\app.jar'
                echo 'Demo deployment completed: deploy\\app.jar'
            }
        }
    }

    post {
        always {
            junit allowEmptyResults: true,
                testResults: 'target/surefire-reports/*.xml'
        }
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }
        failure {
            echo 'CI/CD Pipeline failed. Check the console output.'
        }
    }
}