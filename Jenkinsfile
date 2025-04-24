pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
               bat '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''             
            }
        }

        stage("Test") {
             agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                bat '''
                    test -f build/index.html
                    npm test
                '''
            }
        }
    

        stage('Deploy') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
               bat '''
                   npm install netlify-cli -g
                   netlify --version
                '''             
            }
        }

    }
    
    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}
