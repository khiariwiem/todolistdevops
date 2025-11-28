pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/khiariwiem/todolistdevops.git'
            }
        }

        stage('Build Docker image') {
            steps {
                sh 'docker build -t todolist-backend:jenkins .'
            }
        }

        stage('Run container (test)') {
            steps {
                sh 'docker run -d --name todolist-jenkins -p 5001:5000 todolist-backend:jenkins || true'
            }
        }
    }

    post {
        always {
            sh 'docker stop todolist-jenkins || true'
            sh 'docker rm todolist-jenkins || true'
        }
    }
}
