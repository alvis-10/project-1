pipeline {
    agent any

    tools {
        nodejs 'NodeJS' // Use the name you configured in the Global Tool Configuration
    }
    
    triggers {
        pollSCM('H/2 * * * *') // Polls the SCM every 2 minutes
    }

    stages {
        stage("Clone gallery repository") {
            steps {
                git branch: 'master', url: 'https://github.com/alvis-10/project-1.git'
            }
        }

        stage('Install dependencies') {
            steps {
                script {
                        sh 'npm install'
                        error "Failed to install dependencies: ${e.message}"
                    
                }
            }
        }

        stage('Build project') {
            steps {
                script {
                        echo 'Building project...'
                        sh 'npm run build'
                        error "Build failed: ${e.message}"
                    }
                }
            }
    

        stage('Start server') {
            steps {
                script {
                        echo 'Starting server...'
                        sh 'npm start &'
                        sleep 10 // Give time for the server to start
                    } 
                        error "Failed to start server: ${e.message}"
                    }
                }
            }
            }