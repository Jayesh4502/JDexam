pipeline {
    agent any
 
    environment {
        IMAGE_NAME = "healthcare-app"
        CONTAINER_NAME = "healthcare-container"
        APP_PORT = "3000"  // Host port to expose
    }
 
    stages {
        stage('Clone Repo') {
            steps {
                script {
                    echo "📥 Cloning the GitHub Repository..."
                    git branch: 'main', url: 'https://github.com/Jayesh4502/JDexam.git'
                }
            }
        }
 
        stage('Build Docker Image') {
            steps {
                script {
                    echo "🐳 Building Docker Image..."
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }
 
        stage('Stop Old Container') {
            steps {
                script {
                    echo "🛑 Stopping and Removing Old Container..."
                    sh """
                        docker stop ${CONTAINER_NAME} || true
                        docker rm ${CONTAINER_NAME} || true
                    """
                }
            }
        }
 
        stage('Run Docker Container') {
            steps {
                script {
                    echo "🚀 Running Docker Container..."
                    sh "docker run -d -p ${APP_PORT}:80 --name ${CONTAINER_NAME} ${IMAGE_NAME}"
                }
            }
        }
    }
 
    post {
        success {
            echo "✅ Deployment successful! Visit: http://<your-ec2-ip>:${APP_PORT}"
        }
        failure {
            echo "❌ Deployment failed. Check logs for more details."
        }
    }
}

environment {
    IMAGE_NAME = "healthcare-app"
    CONTAINER_NAME = "healthcare-container"
    APP_PORT = "80"  // Host port
}

