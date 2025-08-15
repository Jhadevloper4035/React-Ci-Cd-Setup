pipeline {
    agent any

    options {
        // Disable the build if there are no changes in the repository
        skipDefaultCheckout true
    }

    stages {

        stage('Clean Workspace') {
            steps {
                // Clean the workspace before starting the build
                cleanWs()
            }
        }

        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                checkout scm

                // Print the current working directory
                sh 'pwd'

                // List the files in the current directory
                sh 'ls -la'
            }
        }

        stage('Build') {
            agent {
                docker {
                    image 'node:20-alpine'
                    args '-u root:root' // Optional: run as root if permissions issues
                }
            }
            steps {
                // Build the project
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm install
                    npm run build
                    ls -l
                '''
            }
        }
    }
}
