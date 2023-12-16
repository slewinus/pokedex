pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Construire l'image Docker
                sh 'docker build -t pokedex-app .'
            }
        }

        stage('Test') {
            steps {
                // Exécuter les tests ici (si disponibles)
            }
        }

        stage('Deploy') {
            steps {
                // Déployer sur Minikube
                sh 'minikube start'
                sh 'kubectl apply -f kubernetes-deployment.yml'
            }
        }
    }

    post {
        always {
            // Nettoyer après le pipeline
            sh 'minikube stop'
        }
    }
}
