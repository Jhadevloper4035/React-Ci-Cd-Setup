pipeline {
    agent {
        docker {
            image 'node:20-alpine'
            args '-u root:root'
        }
    }

    options {
        skipDefaultCheckout true
        timestamps()
    }

   
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

        stage('Build & Test') {
            steps {
                sh '''
                    node --version
                    npm --version
                    npm ci
                    npm test
                    npm run build
                '''
            }
        }
    }
}
