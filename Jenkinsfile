@Library ("shared") _
pipeline {
    agent {label "vinod" }

    stages {
        
        stage('Hello') {
            steps {
                script {
                    hello()
                }
            }
        }
        stage('Git Checkout') {
            steps {
                script {
                    gitCheckout('https://github.com/rcheeez/django-notes-app.git', 'dev')
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    dockerBuild('notes-app', 'latest')
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    dockerPush('docker-creds', 'notes-app', 'latest')
                }
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying the Application..."
                sh 'docker compose up -d'
                echo "Application Deployed Successfully!"
            }
        }
    }
}
