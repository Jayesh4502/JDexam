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
 
        stage('Install Dependencies') {
            steps {
                script {
                    echo "📦 Installing Application Dependencies..."
                    sh '''
                        cd ${APP_DIR}
                        if [ -f package.json ]; then
                            npm install
                        else
                            echo "⚠️ No package.json found. Skipping npm install."
                        fi
                    '''
                }
            }
        }
 
        stage('Start Application') {
            steps {
                script {
                    echo "🚀 Starting the Application..."
                    sh '''
                        cd ${APP_DIR}
                        nohup npm start --port=${APP_PORT} &
                    '''
                }
            }
        }
    }
 
    post {
        success {
            echo "✅ Application deployed successfully at: http://<your-ec2-ip>:${APP_PORT}"
        }
        failure {
            echo "❌ Deployment failed. Please check the Jenkins logs for details."
        }
    }
}
