pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:20-alpine'
                    args '-u root:root' // Optional: run as root if permissions issues
                }
            }
            steps {

                step('clean Work Space') {
                    cleanWs()

                }

                step('build the project'){
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
}
