pipeline {
    agent any

    environment {
        SONARQUBE = 'SonarQube'
        DOCKER_IMAGE = "gowtham/myapp"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'github-creds', url: 'https://github.com/<your-username>/<your-repo>.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'sonar-scanner -Dsonar.projectKey=myapp -Dsonar.sources=.'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 5000:5000 $DOCKER_IMAGE'
            }
        }
    }
}
