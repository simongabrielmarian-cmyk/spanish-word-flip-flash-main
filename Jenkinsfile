// Jenkinsfile: Node.js build + Vitest + Playwright pipeline using Docker

pipeline {
    // Use a single Node container for build and test stages
    agent {
        docker {
            image 'node:22-alpine'
            args '-v $WORKSPACE:/workspace -w /workspace'
        }
    }

    options {
        ansiColor('xterm')
        // Keep build logs clean
        timestamps()
    }

    environment {
        NODE_ENV = 'development'
    }

    stages {

        stage('Install dependencies') {
            steps {
                echo 'Installing Node dependencies...'
                sh 'npm ci'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'npm run build'
            }
        }

        stage('Unit Tests') {
            steps {
                echo 'Running Vitest unit tests...'
                sh 'npx vitest run --reporter=verbose'
            }
        }

        stage('E2E / Playwright Tests') {
            steps {
                echo 'Running Playwright E2E tests...'
                // Example: assumes you have a script "npm run test:e2e"
                sh 'npm run test:e2e'
            }
        }

        stage('Deploy (Mock)') {
            agent {
                docker {
                    image 'alpine'
                }
            }
            steps {
                echo 'Mock deployment step (does nothing)'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs()
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the logs above.'
        }
    }
}