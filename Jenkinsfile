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
                // Create virtual environment and install dependencies
                sh '''#!/bin/bash
                python3 -m venv venv
                source venv/bin/activate
                pip install -r requirements.txt
                '''
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
