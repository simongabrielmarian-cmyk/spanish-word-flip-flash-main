//pipeline for a Node.js project with build, test, and deploy stages using Docker agents
// for testing purpose    

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
            steps {
                script {
                    docker.image('node:22-alpine').inside {
                        sh 'npx vitest run --reporter=verbose'
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