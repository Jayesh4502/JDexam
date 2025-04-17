pipeline {
    agent any
 
    environment {
        APP_DIR = "healthcare-app"
        APP_PORT = "3000"
    }
 
    stages {
        stage('Clone Repository') {
            steps {
                script {
                    echo "📥 Cloning the GitHub Repository..."
                    git branch: 'main', url: 'https://github.com/Jayesh4502/JDexam.git'
                }
            }
        }
 
        stage('Install http-server') {
            steps {
                script {
                    echo "⚙️ Installing http-server (if not already present)..."
                    sh '''
                        if ! command -v http-server > /dev/null; then
                            npm install -g http-server
                        fi
                    '''
                }
            }
        }
 
        stage('Start Static Server') {
            steps {
                script {
                    echo "🚀 Starting static site with http-server..."
                    sh '''
                        cd ${APP_DIR}
                        nohup http-server -p ${APP_PORT} &
                    '''
                }
            }
        }
    }
 
    post {
        success {
            echo "✅ Static website hosted successfully at: http://<your-ec2-ip>:${APP_PORT}"
        }
        failure {
            echo "❌ Deployment failed. Please check Jenkins logs."
        }
    }
}
