pipeline {
    agent any

    environment {
        DISCORD_WEBHOOK_URL = "https://discord.com/api/webhooks/1336532501488734228/nJpK7glxCnvmUsVMNtbov-eEPqwwcXkg1us0Mxh08vpYF8ylkLgXflLUHU5dX_Ny1WbV"
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/your-repository.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Building project..."'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Running tests..."'
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo "Deploying application..."'
            }
        }
    }

    post {
        success {
            script {
                sh """
                curl -X POST -H 'Content-Type: application/json' \
                -d '{
                    "content": "✅ **Jenkins Build SUCCESS** for job: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    "username": "Jenkins Bot"
                }' ${DISCORD_WEBHOOK_URL}
                """
            }
        }
        failure {
            script {
                sh """
                curl -X POST -H 'Content-Type: application/json' \
                -d '{
                    "content": "❌ **Jenkins Build FAILED** for job: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    "username": "Jenkins Bot"
                }' ${DISCORD_WEBHOOK_URL}
                """
            }
        }
    }
}
