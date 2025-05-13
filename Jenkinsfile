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
              echo "Tested"
            }
        }

        stage('Test') {
            steps {
                // Run tests after activating virtual environment
                sh '''#!/bin/bash
                source venv/bin/activate
                pytest tests/
                '''
            }
        }

        stage('Deploy') {
            steps {
                // Docker build, stop, remove, and run the container
                sh '''#!/bin/bash
                docker build -t inventory-app .
                docker stop inventory-app || true
                docker rm inventory-app || true
                docker run -d -p 5000:5000 --name inventory-app inventory-app
                '''
            }
        }
    }
}
