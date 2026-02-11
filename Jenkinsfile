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
                        }       
                    }
                    steps {
                        sh 'npm ci'
                        sh 'npm run test:unit'
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
                        sh 'npm run test:e2e'
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