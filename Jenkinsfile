pipeline {
    agent any

    options {
        skipDefaultCheckout true
        timestamps()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                sh '''
                    echo "=== Current Directory ==="
                    pwd
                    echo "=== Files in Workspace ==="
                    ls -la
                '''
            }
        }

        stage('Build') {
            agent {
                docker {
                    image 'node:20-alpine'
                    args '-u root:root'
                }
            }
            steps {
                sh '''
                    echo "=== Building with Node.js ==="
                    node --version
                    npm --version
                    npm ci --only=production
                    npm run build
                '''
            }
        }

       
    }
}
