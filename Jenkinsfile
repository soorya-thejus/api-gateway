pipeline {
    agent any
    tools {
        maven 'maven'
        jdk 'jdk-17'
    }
    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/soorya-thejus/api-gateway.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                bat "mvn clean install -DskipTests"
            }
        }
        stage('Test') {
            steps {
                bat "mvn test"
            }
        }
        stage('Deploy') {
            steps {
		bat "docker rm -f api-container"
                bat "docker rmi -f api-image"
                bat "docker build -t api-image ."
                bat "docker run -p 8090:8090 -d --name api-container api-image"
            }
        }
    }
}
