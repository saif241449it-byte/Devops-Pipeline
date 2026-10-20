DevOps Pipeline Demo

Project Overview

This project demonstrates an end-to-end DevOps pipeline for a Python Flask application using Git, GitHub, Jenkins, Docker, and automated testing with pytest.

Application Features

- Home page at "/"
- Health-check endpoint at "/health"
- Automated tests using pytest
- Docker image creation and container deployment
- Jenkins pipeline for continuous integration and deployment

Technologies Used

- Python
- Flask
- pytest
- Git and GitHub
- Jenkins
- Docker

Run the Application Locally

Install the dependencies:

python -m pip install -r requirements.txt

Run the application:

python app.py

Open these URLs in your browser:

- http://localhost:5000
- http://localhost:5000/health

Run Automated Tests

python -m pytest -v test_app.py

Build and Run with Docker

docker build -t devops-pipeline-demo:latest .
docker run -d --name devops-pipeline-demo -p 5000:5000 devops-pipeline-demo:latest

Jenkins Pipeline

The "Jenkinsfile" defines the stages for source-code checkout, dependency installation, automated testing, Docker image building, container deployment, and deployment verification.