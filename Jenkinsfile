pipeline {
    agent any

    stages {
       /* stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh'''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                '''
            }
        } */

        stage ('Test'){
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm test
                '''
            }
        }

        stage ('E2E'){
            agent {
                docker {
                    image 'nmcr.microsoft.com/playwright:v1.39.0-jammy'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm install -g serve
                    server -s build
                    npx playwright test
                '''
            }
        }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
    }

