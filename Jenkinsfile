pipeline {
    agent {
        docker {
            image 'node:20-alpine'
            args '-u root:root'
        }
    }

    environment {
        NODE_ENV = 'production'
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

        stage('Lint') {
            steps {
                sh '''
                    npm run lint
                '''
            }
        }


        stage('Deploy'){
            steps{

                sh '''
                    npm install -g vercel

                    vercel --prod --token $VERCEL_TOKEN --confirm --name=CiCd 
                    echo "Deployment completed successfully"

                    '''
            }





        }


    }
}
