pipeline {
    agent any

    environment {
        // Ensure the PATH is set to include any necessary locations
        PATH = "/usr/local/bin:${env.PATH}"
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
                git branch: 'main', 
                    credentialsId: '6fc544f5-c122-4514-b21b-55d7f4fcc921', 
                    url: 'https://github.com/VISHAL9736/mini-devops.git'  // Update your GitHub URL
            }
        }
        stage('Install Dependencies') {
            steps {
                dir('Version 1') {  // Adjust to the correct directory where your package.json is located
                    sh 'npm install'  // Use sh for Unix/Linux or bat for Windows
                }
            }
        }
        stage('Build') {
            steps {
                dir('Version 1') {  // Ensure this is the directory where your build script exists
                    sh 'npm run build'
                }
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    // Assuming a Dockerfile exists and Docker is installed on Jenkins agent
                    sh 'docker build -t react-quiz-app:latest .'
                }
            }
        }
        stage('Docker Run') {
            steps {
                script {
                    // Run the container (you can expose ports as needed)
                    sh 'docker run -d --name react-quiz-app-container -p 3000:3000 react-quiz-app:latest'
                }
            }
        }
        stage('Test') {
            steps {
                dir('Version 1') {  // Make sure to run tests from the correct directory
                    sh 'npm run test'
                }
            }
        }
        stage('Docker Cleanup') {
            steps {
                script {
                    // Stop and remove the container after tests
                    sh 'docker stop react-quiz-app-container'
                    sh 'docker rm react-quiz-app-container'
                }
            }
        }
    }
}
