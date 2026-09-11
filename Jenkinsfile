pipeline {
    agent any

    stages {

        //This is the build stage to build the project
        
        stage('Build') {
            agent {
              docker{
                    image 'node:18-alpine'
                    reuseNode true
              }
            }
            steps {
                sh '''
                ls -la
                node --version
                npm --versions
                npm ci
                npm run build
                ls -la

                '''
               
            }
        }

        stage('Run Tests'){
            parallel{

                stage('Test1') {
            agent {
              docker{
                    image 'node:18-alpine'
                    reuseNode true
              }
            }
            
            steps {
               echo "Test stage is under go.."
               sh '''
               test -f build/index.html
               
               npm test
               '''
               
               
            }
        }

         stage('Test2') {
            agent any
            
            steps {
               echo "Test2 stage is under go.."
            
               
               
            }
        }
        }
        }

        // tHIS IS THE Test repo to test the conditions
         stage('Test') {
            agent {
              docker{
                    image 'node:18-alpine'
                    reuseNode true
              }
            }
            
            steps {
               echo "Test stage is under go.."
               sh '''
               test -f build/index.html
               
               npm test
               '''
               
               
            }
        }

        //  stage('E2E') {
        //     agent {
        //       docker{
        //             image 'node:20'
        //             reuseNode true
        //             // args '-u root:root'
        //       }
        //     }
            
        //     steps {
        //        echo "Test stage is under go.."
        //        sh '''
        //          npx playwright install chromium
        //          npm install serve
        //          node_modules/.bin/serve -s build
        //          npx playwright test
        //        '''
               
               
        //     }
        // }
    }
    //POST COMMAND

    post{
        always{
            junit 'test-results/junit.xml'
        }
    }
}
