pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Pravalikaa18/flask-app.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t pravalikaa18/flask-app:latest .'
            }
        }
        stage('Push to DockerHub') {
            steps {
                sh 'docker login -u pravalikaa18 -p Pravalika@1809'
                sh 'docker push pravalikaa18/flask-app:latest'
            }
        }
    }
}
