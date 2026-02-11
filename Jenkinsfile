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
            parallel {
                stage('Unit Tests') { 
                    agent {
                        docker {
                             image 'node:22-alpine'
                             //reuseNodeModules true
                        }       
            }
                    steps {
                        sh 'npm cache clean --force'
                        sh 'rm -rf node_modules package-lock.json'
                        sh 'npm install'
                        sh 'npm run test:unit'
                        sh 'npx vitest run --reporter=verbose'
                    }
                }
                stage('Integration Tests') {
                    agent {
                        docker {
                            image 'mcr.microsoft.com/playwright:v1.54.2-jammy'
                        }
                    }
                    steps {
                        sh 'npm ci'
                        sh 'npx playwright test'
                    }
                }
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