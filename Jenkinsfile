pipeline {
    agent any
    environment {
        PATH = "/usr/local/bin:${env.PATH}"  // Adjust as necessary
    }
    stages {
        stage('Debug Info') {
            steps {
                sh 'echo "PATH: $PATH"'
                sh 'node -v'
                sh 'npm -v'
                sh 'git --version'
            }
        }
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        // Other stages...
    }
}
