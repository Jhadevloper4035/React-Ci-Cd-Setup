pipeline {
    agent {
        docker {
            image 'node:20-alpine'
            args '-u root:root'
        }
    }

    environment {
        VERCEL_TOKEN = credentials('NEW_TOKEN')
    }

    options {
        skipDefaultCheckout true
        timestamps()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                sh 'pwd && ls -la'
            }
        }

        stage('Install & Build') {
            steps {
                sh '''
                    node --version
                    npm --version
                    npm ci
                    npm run build
                '''
            }
        }

        stage('Lint') {
            steps {
                sh 'npm run lint'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    npx vercel --prod --token $VERCEL_TOKEN --yes --name=cicd
                    echo "Deployment completed successfully"
                '''
            }
        }
    }
}
