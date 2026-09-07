pipeline {
    agent any

    stages {
        stage('Without docker') {
            steps {
                sh '''
                echo 'Without docker'
                ls -la
                touch container-no.txt
                '''
               
            }
        }
        stage('With docker') {
            agent {
              docker{
                    image 'node:18-alpine'
              }
            }
            steps {
                sh '''
                echo 'With using docker version'
                ls -la
                touch container-yes.txt
                #npm --version
                '''
               
            }
        }
    }
}
