pipeline {
    agent any
    
    options {
        ansiColor('xterm')
    }

    stages {
        stage('build') {
            agent {
                docker {
                    image 'node:22-alpine'
                }
            }
            steps {
                sh 'npm ci'
                sh 'npm run build'
            }
        }

        stage('test') {
            agent {
                docker {
                    image 'node:22-alpine'
                }
            }
            steps {
                // Unit tests with Vitest
                sh 'npm cache clean --force'
                sh 'rm -rf node_modules package-lock.json'
                sh 'npm install'
                sh 'npm run test:unit'
                sh 'npx vitest run --reporter=verbose'
            }
        }

        stage('deploy') {
            agent {
                docker {
                    image 'alpine'
                }
            }
            steps {
                // Mock deployment which does nothing
                echo 'Mock deployment was successful!'
            }
        }
    }
}