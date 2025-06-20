pipeline {
    agent any

    environment {
        // Set Python version if using pyenv or similar, or leave blank
        PYTHON = 'python3'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub
                git branch: 'main', url: 'https://github.com/your-username/your-fastapi-repo.git'
            }
        }
        stage('Set up Python') {
            steps {
                // Install dependencies
                sh "${env.PYTHON} -m venv venv"
                sh '. venv/bin/activate && pip install --upgrade pip'
                sh '. venv/bin/activate && pip install -r requirements.txt'
            }
        }
        stage('Run Tests') {
            steps {
                // Run pytest
                sh '. venv/bin/activate && pytest'
            }
        }
        stage('Build') {
            steps {
                // Optional: Build step, e.g., Docker build
                // sh "docker build -t your-fastapi-app ."
                echo 'Build step (customize as needed)'
            }
        }
    }
    post {
        always {
            junit '**/test-results.xml' // If you use pytest with junitxml output
            cleanWs()
        }
    }
}
