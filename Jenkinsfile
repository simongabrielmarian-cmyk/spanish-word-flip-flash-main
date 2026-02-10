pipeline {
    agent {
        docker {
            image 'node:22-alpine'
            args '-v $WORKSPACE:/workspace -w /workspace'
        }
    }

    options {
        ansiColor('xterm')
    }

    stages {
        stage('build') {
            steps {
                sh 'npm ci'
                sh 'npm run build'
            }
        }

        stage('unit tests') {
            steps {
                sh 'npx vitest run --reporter=verbose'
            }
        }

        stage('deploy') {
            agent {
                docker { image 'alpine' }
            }
            steps {
                echo 'Mock deployment was successful!'
            }
        }
    }
}