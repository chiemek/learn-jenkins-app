pipeline {
    agent any

    stages {
        stage('without docker') {
            steps {
               sh 'echo "without docker"'
               sh 'ls -la'
               sh 'touch without-cotainer.txt'
            }
        }
        stage('with docker') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
               sh 'echo "with docker"'
               sh 'ls -la'
               sh 'touch with-cotainer.txt'

            }
        }
    }
}
