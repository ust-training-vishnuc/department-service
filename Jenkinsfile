pipeline {
    agent any 
    tools {
        maven 'my-maven'
        jdk 'my-jdk'
    }
    stages {        
        stage('Clone') {
            steps {
                git url: 'https://github.com/ust-training-vishnuc/department-service.git', branch: 'main'
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
                bat "docker rm -f dept-container"
                bat "docker rmi -f dept-image"
                bat "docker build -t dept-image ."
                bat "docker run -p 8081:8081 -d --name dept-container dept-image"
            }
        }
    }
}
