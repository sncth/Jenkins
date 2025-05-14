pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/jenkins-docs/simple-java-maven-app.git'
            }
        }

        stage('Serve Web Page') {
            steps {
                script {
                    // Ensure the web directory exists
                    bat 'if not exist web mkdir web'
                    writeFile file: 'web/index.html', text: '<!DOCTYPE html><html><head><title>Sample</title></head><body><h1>Hello from Jenkins!</h1></body></html>'
                    
                    // Start the Python HTTP server on port 8000 instead of 8080
                    bat 'start python -m http.server 8000 --bind 0.0.0.0 --directory web'
                }
            }
        }

        stage('Wait and Test') {
            steps {
                bat 'ping 127.0.0.1 -n 11 > nul'  // 10-second delay
                bat 'curl -v http://localhost:8000'
            }
        }
    }
}
