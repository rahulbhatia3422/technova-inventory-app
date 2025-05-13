pipeline {
    agent any
    stages {
        stage('Checkout') { steps { checkout scm } }
        stage('Build') { steps { sh 'pip install -r requirements.txt' } }
        stage('Test') { steps { sh 'python -m pytest tests/' } }
        stage('Deploy') { steps {
            sh 'docker build -t inventory-app .'
            sh 'docker stop inventory-app || true'
            sh 'docker run --rm -d -p 5000:5000 --name inventory-app inventory-app'
        } }
    }
}
