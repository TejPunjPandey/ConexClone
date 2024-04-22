pipeline {
    agent any
    
    stages {
        stage('Initialization') {
            steps {
                script {
                    // Add any initialization tasks here
                    echo 'Initialization script running...'
                }
            }
        }
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/TejPunjPandey/ConexClone.git'
            }
        }
        stage('Set Up Node.js') {
            steps {
                tool name: 'NodeJS', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
            }
        }
        stage('Install Dependencies for backend') {
            steps {
                script {
                    try {
                        dir('backend') {
                            sh 'npm install'
                        }
                    } catch (Exception e) {
                        // Handle the error
                        echo 'Failed to install backend dependencies'
                        throw e // Re-throw the exception to mark the build as failed
                    }
                }
            }
        }
        stage('Install Dependencies for frontend') {
            steps {
                script {
                    try {
                        dir('frontend') {
                            // Copy .env file from backend to frontend directory
                            sh 'cp ../backend/.env .'
                            // Install vite before running npm install
                            sh 'npm install vite'
                            sh 'npm install'
                        }
                    } catch (Exception e) {
                        // Handle the error
                        echo 'Failed to install frontend dependencies'
                        throw e // Re-throw the exception to mark the build as failed
                    }
                }
            }
        }
       stage('Copy Build Artifacts') {
    steps {
        // Copy build artifacts from frontend dist directory to Jenkins workspace
        sh 'cp -r frontend/dist/* .'
        // Verify if the files are copied
        sh 'ls -l'
    }
}

    }
}