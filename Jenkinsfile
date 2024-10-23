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
                // Checkout the specified GitHub repository
                git branch: 'main', credentialsId: '6fc544f5-c122-4514-b21b-55d7f4fcc921', url: 'https://github.com/VISHAL9736/mini-devops.git'
            }
        }

        stage('Install') {
            steps {
                // Change to the directory where package.json is located
                dir('Version 1') {  // Adjust if 'Version 1' is not the correct path
                    bat 'npm install'  // Using 'bat' for Windows
                }
            }
        }

        stage('Build') {
            steps {
                // Run the build command
                bat 'npm run build'  // Ensure this runs in the correct directory
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    // Assuming a Dockerfile exists and Docker is installed on the Jenkins agent
                    bat 'docker build -t react-quiz-app:latest .'  // Builds the Docker image
                }
            }
        }

        stage('Docker Run') {
            steps {
                script {
                    // Run the container (you can expose ports as needed)
                    bat 'docker run -d --name react-quiz-app-container -p 3000:3000 react-quiz-app:latest'  // Runs the Docker container
                }
            }
        }

        stage('Test') {
            steps {
                // Run tests after the container is running, assuming tests are integration/E2E type
                bat 'npm run test'  // Executes the test command
            }
        }
    }
}
