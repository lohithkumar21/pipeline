pipeline {
    agent {
        docker {
            image 'python:3.9'  // Use an official Python image with pip installed
            label 'python-agent'  // Optional: Label for nodes with Python agents
        }
    }

    stages {
        stage('Build') {
            steps {
                echo 'Installing dependencies...'
                sh 'pip install -r requirements.txt'  // This will now work because Python and pip are available in the container
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'python -m unittest discover -s .'
            }
        }
        stage('Code Quality') {
            steps {
                echo 'Running code quality checks...'
                sh 'flake8 .'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh '''
                mkdir -p /tmp/python-app-deploy
                cp app.py /tmp/python-app-deploy/
                '''
            }
        }
        stage('Docker Build and Deploy') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t python-app .'

                echo 'Deploying Docker container...'
                sh 'docker run -d --name python-app -p 5000:5000 python-app'
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

