pipeline {
    agent any

    environment {
        IMAGE_NAME = 'devops-pipeline-demo:latest'
        CONTAINER_NAME = 'devops-pipeline-demo'
        PORT = '5000'
        DOCKER = 'C:\\Users\\saifs\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe'
    }

    stages {
        stage('Checkout SCM') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing Python dependencies...'
                bat 'python -m pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running automated tests with pytest...'
                bat 'python -m pytest -v test_app.py'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                bat '"%DOCKER%" build -t %IMAGE_NAME% .'
            }
        }

        stage('Deploy Container') {
            steps {
                echo 'Deploying Docker container...'
                bat '"%DOCKER%" rm -f %CONTAINER_NAME% 2>nul || exit /b 0'
                bat '"%DOCKER%" run -d --name %CONTAINER_NAME% -p %PORT%:5000 %IMAGE_NAME%'
            }
        }

        stage('Verify Deployment') {
            steps {
                echo 'Checking application health...'
                bat 'powershell -NoProfile -Command "Start-Sleep -Seconds 5; $r = Invoke-RestMethod -Uri http://localhost:5000/health; if ($r.status -ne \\"healthy\\") { exit 1 }; $r | ConvertTo-Json -Compress"'
            }
        }
    }

    post {
        success {
            echo '===================================='
            echo 'DevOps Pipeline Executed Successfully!'
            echo 'Application URL: http://localhost:5000'
            echo 'Health Endpoint: http://localhost:5000/health'
            echo '===================================='
        }

        failure {
            echo 'Pipeline failed. Please review the stage logs.'
        }
    }
}