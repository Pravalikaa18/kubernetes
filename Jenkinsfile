pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('98897e03-c137-4438-8da4-dd1f33b63fba') // You must create this in Jenkins
        KUBECONFIG_CREDENTIALS = credentials('kubeconfig') // You must create this in Jenkins
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Pravalikaa18/kubernetes.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t pravalikaa18/flask-app:latest .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'docker push pravalikaa18/flask-app:latest'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig', variable: 'KUBECONFIG_FILE')]) {
                    sh '''
                        export KUBECONFIG=$KUBECONFIG_FILE
                        kubectl apply -f deployment.yaml
                        kubectl apply -f service.yaml
                    '''
                }
            }
        }
    }
}
