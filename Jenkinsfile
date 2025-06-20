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
                git branch: 'main', url: 'https://github.com/dinesh-shelke/fastapi_app.git'
            }
        }
        stage('Set up Python') {
            steps {
                // Install dependencies
                sh "${env.PYTHON} -m venv venv"
                sh '. venv/bin/activate && pip install --upgrade pip'
                sh '. venv/bin/activate && pip install -r requirements.txt'
                // sh 'pwd'
                // sh 'ls -la'
            }
        }
        // stage('Run Tests') {
        //     steps {
        //         // Run pytest
        //         sh '. venv/bin/activate && pytest'
        //     }
        // }
        stage('Build') {
            steps {
                // Optional: Build step, e.g., Docker build
                // sh "docker build -t your-fastapi-app ."
                sh 'kill -9 $(ps aufx | grep 428[8] | awk \'{ print $2 }\')'
                sh '. venv/bin/activate && uvicorn main:app --host 0.0.0.0 --port 4288 &'
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
