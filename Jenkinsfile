pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'python3 -m venv venv && source venv/bin/activate && pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh 'source venv/bin/activate && pytest tests/'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker build -t inventory-app .
                docker stop inventory-app || true
                docker rm inventory-app || true
                docker run -d -p 5000:5000 --name inventory-app inventory-app
                '''
            }
        }
    }
}
