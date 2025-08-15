pipeline {
    agent any 

    stages{
        stage('Build'){
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true // Reuse the node to avoid creating a new one for each stage
                }
            }
        }
    }
}