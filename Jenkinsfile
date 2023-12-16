pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building Docker Image...'
                sh 'docker build -t pokedex-app .'
            }
        }

        stage('Test') {
            steps {
                echo 'Running Tests...'
                sh 'docker-compose up -d'
                sh 'docker-compose exec app npm test'
                sh 'docker-compose down'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to Minikube...'
                sh 'minikube start'
                sh 'kubectl apply -f kubernetes-deployment.yml'
                sh 'minikube stop'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh 'docker-compose down'
            sh 'minikube stop'
        }
    }
}
