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
                    bat 'mkdir web'
                    writeFile file: 'web/index.html', text: '<!DOCTYPE html><html><head><title>Sample</title></head><body><h1>Hello from Jenkins!</h1></body></html>'
                    bat 'start python -m http.server 8080 --directory web'
                }
            }
        }

        stage('Wait and Test') {
            steps {
                bat 'timeout /t 10'
                bat 'curl -v http://localhost:8080'
            }
        }
    }
}
