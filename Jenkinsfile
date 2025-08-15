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

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                sh '''
                    pwd
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
                    npm run build
                '''
            }
        }
    }
}
