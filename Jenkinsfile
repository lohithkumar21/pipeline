pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Installing dependencies...'
                sh 'pip install -r requirements.txt'  // Install dependencies
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'python -m unittest discover -s .'  // Run tests using unittest
            }
        }
        stage('Code Quality') {
            steps {
                echo 'Running code quality checks...'
                sh 'flake8 .'  // Run flake8 for code quality checks
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh '''
                mkdir -p /tmp/python-app-deploy
                cp app.py /tmp/python-app-deploy/
                '''  // Simulate deployment by copying app.py
            }
        }
        stage('Docker Build and Deploy') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t python-app .'

                echo 'Deploying Docker container...'
                sh 'docker run -d --name python-app -p 5000:5000 python-app'  // Deploy in Docker container
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the logs for more details.'
        }
    }
}
