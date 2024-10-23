pipeline {
    agent any

    environment {
        // Ensure npm and other binaries are found in the PATH
        PATH = "/usr/local/bin:${env.PATH}"  // Adjust as necessary
    }

    stages {
        stage('Debug Info') {
            steps {
                sh 'echo "PATH: $PATH"'  // Print the current PATH
                sh 'node -v'  // Print the Node.js version
                sh 'npm -v'   // Print the npm version
                sh 'git --version'  // Print the Git version
            }
        }
        stage('Checkout') {
            steps {
                // Checkout the code from your repository
                git branch: 'main', credentialsId: '6fc544f5-c122-4514-b21b-55d7f4fcc921', url: 'https://github.com/VISHAL9736/mini-devops.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                // Change to the directory containing package.json and install dependencies
                dir('Version 1') {
                    sh 'npm install'  // Use sh instead of bat for macOS
                }
            }
        }
        stage('Build') {
            steps {
                // Build the React application
                dir('Version 1') {
                    sh 'npm run build'  // Use sh for macOS
                }
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    // Build the Docker image, assuming a Dockerfile exists in the 'Version 1' directory
                    dir('Version 1') {
                        sh 'docker build -t react-quiz-app:latest .'  // Use sh for macOS
                    }
                }
            }
        }
        stage('Docker Run') {
            steps {
                script {
                    // Run the Docker container, exposing necessary ports
                    sh 'docker run -d --name react-quiz-app-container -p 3000:3000 react-quiz-app:latest'  // Use sh for macOS
                }
            }
        }
        stage('Test') {
            steps {
                // Run tests, assuming you have a test script in package.json
                dir('Version 1') {
                    sh 'npm run test'  // Use sh for macOS
                }
            }
        }
    }
}
